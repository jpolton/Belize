For GEBCO bathymetry data, head to the BODC website and download the desired domain. For this work, we use 1-minute 2D dataset (2008) It is no longer possible to download subsets of this dataset so the whole domain needs to be downloaded and subset manually.
	
	$ apt-get update
	$ apt-get install cdo
	$ cdo sellonlatbox,lon1,1on2,kat1,lat2 GRIDONE_2D.nc gebco_subset.nc

This produces a cropped bathy file that can be used by the weighting tools.

	cp gebco_subset.nc $INPUTS/.

Copy over the namelist from startfiles to allow bathymetry to be reshaped.

	cp $START_FILES/namelist_reshape_bilin_gebco $INPUTS/.

Check that the lat and lon variables are the same as in the nc GEBCO file. (I had to change them)

	nano namelist_reshape_bilin_gebco
	&grid_inputs
	    input_file = 'gebco_in.nc'
	    nemo_file = 'coordinates.nc'
	    datagrid_file = 'remap_data_grid_gebco.nc'
	    nemogrid_file = 'remap_nemo_grid_gebco.nc'
	    method = 'regular'
	    input_lon = 'lon'
	    input_lat = 'lat'
	    nemo_lon = 'glamt'
	    nemo_lat = 'gphit'
	    nemo_mask = 'none'
	    nemo_mask_value =  0
	    input_mask = 'none'
	    input_mask_value = 0
	...
	&interp_inputs
    	input_file = "gebco_in.nc"
    	...
    	input_name = "elevation"

Now the land elevations need to be flattened, and also make the depths positve (need to install nco ppackage)::

	apt-get install nco
	cd $INPUTS
	ncap2 -s 'where(elevation > 0) elevation=0' gebco_subset.nc tmp.nc
	ncflint --fix_rec_crd -w -1.0,0.0 tmp.nc tmp.nc gebco_in.nc
	rm tmp.nc

This will generate an nc file called gebco_in.nc Now anonther tool needs to be built::

	cd $TDIR
	./maketools -n WEIGHTS
	cd $INPUTS 

This should make the executables we needs to map bathymetry to grid and generate remap_nemo_grid_gebco.nc and remap_data_grid_gebco.nc files.::

	$TDIR/WEIGHTS/scripgrid.exe namelist_reshape_bilin_gebco

Execute script to generate data_nemo_bilin_gebco.nc file::

	$TDIR/WEIGHTS/scrip.exe namelist_reshape_bilin_gebco

Execute script to generate bath_meter.nc file::

	$TDIR/WEIGHTS/scripinterp.exe namelist_reshape_bilin_gebco

Level 4) Generate a domain configuration file
---------------------------------------------

Now a domain_cfg.nc file that describes the vertical grid of the model is required. For previous versions of NEMO this would of been part of the main namelist_cfg.

Copy the files from the last level::

	cp $INPUTS/coordinates.nc $TDIR/DOMAINcfg/.
	cp $INPUTS/bathy_meter.nc $TDIR/DOMAINcfg/.

Now the main namelist_cfg file in the DOMAINcfg directory needs to be edited as per the below, in this case we are using a 3 level s-coordinate set up. **NOTE**: the dimensions need to match the area being simulated the values below are for area around Madagascar.::

	!-----------------------------------------------------------------------
	&namrun        !   parameters of the run
	!-----------------------------------------------------------------------
	  nn_no       =       0   !  job number (no more used...)
	  cn_exp      =  "domaincfg"  !  experience name
	  nn_it000    =       1   !  first time step
	  nn_itend    =      75   !  last  time step (std 5475)
	/
	!-----------------------------------------------------------------------
	&namcfg        !   parameters of the configuration
	!-----------------------------------------------------------------------
	  !
	  ln_e3_dep   = .false.   ! =T : e3=dk[depth] in discret sens.
	  !                       !      ===>>> will become the only possibility in v4.0
	  !                       ! =F : e3 analytical derivative of depth function
	  !                       !      only there for backward compatibility test with v3.6
	  !                       !
	  cp_cfg      =  "orca"   !  name of the configuration
	  jp_cfg      =      12   !  resolution of the configuration
	  jpidta      =     544   !  1st lateral dimension ( >= jpi ) (For different regions this should be edited)
	  jpjdta      =     438   !  2nd    "         "    ( >= jpj ) (For different regions this should be edited)
	  jpkdta      =      3    !  number of levels      ( >= jpk )
	  jpiglo      =     544   !  1st dimension of global domain --> i =jpidta (For different regions this should be edited)
	  jpjglo      =     438   !  2nd    -                  -    --> j  =jpjdta (For different regions this should be edited)
	  jpizoom     =       1   !  left bottom (i,j) indices of the zoom
	  jpjzoom     =       1   !  in data domain indices
	  jperio      =       0   !  lateral cond. type (between 0 and 6)
	/
	!-----------------------------------------------------------------------
	&namzgr        !   vertical coordinate
	!-----------------------------------------------------------------------
	  ln_zco      = .false.   !  z-coordinate - full    steps
	  ln_zps      = .false.   !  z-coordinate - partial steps
	  ln_sco      = .true.   !  s- or hybrid z-s-coordinate
	  ln_isfcav   = .false.   !  ice shelf cavity
	  ln_linssh   = .false.   !  linear free surface
	/
	!-----------------------------------------------------------------------
	&namzgr_sco    !   s-coordinate or hybrid z-s-coordinate
	!-----------------------------------------------------------------------
	  ln_s_sh94   = .true.    !  Song & Haidvogel 1994 hybrid S-sigma   (T)|
	  ln_s_sf12   = .false.   !  Siddorn & Furner 2012 hybrid S-z-sigma (T)| if both are false the NEMO tanh stretching is applied
	  ln_sigcrit  = .false.   !  use sigma coordinates below critical depth (T) or Z coordinates (F) for Siddorn & Furner stretch
	                          !  stretching coefficients for all functions
	  rn_sbot_min =   6.0     !  minimum depth of s-bottom surface (>0) (m)
	  rn_sbot_max =   7000.0  !  maximum depth of s-bottom surface (= ocean depth) (>0) (m)
	  rn_hc       =   0.0     !  critical depth for transition to stretched coordinates
	         !!!!!!!  Envelop bathymetry
	  rn_rmax     =   0.3     !  maximum cut-off r-value allowed (0<r_max<1)
	         !!!!!!!  SH94 stretching coefficients  (ln_s_sh94 = .true.)
	  rn_theta    =   20.0    !  surface control parameter (0<=theta<=20)
	  rn_bb       =   0.8     !  stretching with SH94 s-sigma
	/
	!-----------------------------------------------------------------------
	&namdom        !   space and time domain (bathymetry, mesh, timestep)
	!-----------------------------------------------------------------------
	  nn_msh      =    0      !  create (=1) a mesh file or not (=0)
	  rn_rdt      =   360.     !  time step for the dynamics (and tracer if nn_acc=0)
	  ppglam0     =  999999.0             !  longitude of first raw and column T-point (jphgr_msh = 1)
	  ppgphi0     =  999999.0             ! latitude  of first raw and column T-point (jphgr_msh = 1)
	  ppe1_deg    =  999999.0             !  zonal      grid-spacing (degrees)
	  ppe2_deg    =  999999.0             !  meridional grid-spacing (degrees)
	  ppe1_m      =  999999.0             !  zonal      grid-spacing (degrees)
	  ppe2_m      =  999999.0             !  meridional grid-spacing (degrees)
	  ppsur       =  999999.0             !  ORCA r4, r2 and r05 coefficients
	  ppa0        =  999999.0             ! (default coefficients)
	  ppa1        =  999999.0             !
	  ppkth       =      23.563           !
	  ppacr       =       9.0             !
	  ppdzmin     =       6.0             !  Minimum vertical spacing
	  pphmax      =    5720.              !  Maximum depth
	  ldbletanh   =  .FALSE.              !  Use/do not use double tanf function for vertical coordinates
	  ppa2        =  999999.              !  Double tanh function parameters
	  ppkth2      =  999999.              !
	  ppacr2      =  999999.
	/
	!-----------------------------------------------------------------------
	&nameos        !   ocean physical parameters
	!-----------------------------------------------------------------------
	  ln_teos10   = .true.         !  = Use TEOS-10 equation of state
	/

Now we need to build the domaincfg tool and to do that we need to use an arch file linked to XIOS1 rather than XIOS2 that is used by NEMO version 4.0. So first co out the XIOS1.0 required (take note of the revision used)::

	cd $WDIR
	svn co ​-r 703 http://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/branchs/xios-1.0 xios-1.0
	ln -s xios-1.0 XIOS1
	cd XIOS1
	cp /SRC/pderian/arch_XIOS/arch* /SRC/XIOS1/arch
	rename arch files (maynot be needed but is useful to differentiate from ones in the XIOS2 folder)
	mv arch-DEBIAN.env arch-DEBIAN1.env
	mv arch-DEBIAN.fcm arch-DEBIAN1.fcm
	mv arch-DEBIAN.path arch-DEBIAN1.path

	./make_xios --dev --netcdf_lib netcdf4_seq --arch DEBIAN1

Once built we need to make a new NEMO ARCH file that links to it.::

	cp /SRC/pderian/arch_NEMOGCM/arch-DEBIAN.fcm SRC/NEMOGCM/ARCH/arch-DEBIAN1.fcm
	cd /SRC/NEMOGCM/ARCH
	nano arch-DEBIAN1.fcm
	edit %XIOS_HOME           /SRC/XIOS2 to
	%XIOS_HOME           /SRC/XIOS1
	exit and save

Now when declaring the ARCH file XIOS2.0 can be used (DEBIAN) or XIOS1.0 (DEBIAN1). Tool can be built as follows::

	cd $TDIR
	./maketools -m DEBIAN1 -n DOMAINcfg clean
	./maketools -m DEBIAN1 -n DOMAINcfg

In the DOMAINcfg folder there should now be a make_domain_cfg.exe file. The executable can now be run::

	cd $TDIR/DOMAINcfg
	./make_domain_cfg.exe

This produces a report in the terminal::

	 WARNING: factorisation of number of PEs failed
	        : using grid of            1  x 1
	-> report :  Performance report : total time spent for XIOS : 3.91006e-05 s
	-> report :  Performance report : time spent for waiting free buffer : 0 s
	-> report :  Performance report : Ratio : 0 %
	-> report :  Performance report : This ratio must be close to zero. Otherwise it may be usefull to increase buffer size or numbers of server
	-> report :  Memory report : Current buffer_size : 50000000
	-> report :  Memory report : Minimum buffer size required : 0
	-> report :  Memory report : increasing it by a factor will increase performance, depending of the volume of data wrote in file at each time step of the file

Now we need to copy it to the EXP directory and also change permissions so it can be read by others.::

	chmod a+rx $TDIR/DOMAINcfg/domain_cfg.nc
	apt-get install rsync
	rsync -uvt $TDIR/DOMAINcfg/domain_cfg.nc $EXP/.
	cp $TDIR/DOMAINcfg/domain_cfg.nc INPUTS/.

Now the boundary conditions need to be created using PyNEMO