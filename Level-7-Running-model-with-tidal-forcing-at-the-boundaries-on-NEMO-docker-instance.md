Copy files to EXP directory::

	cd $EXP
	cp $INPUTS/bathy_meter.nc $EXP/.
	cp $INPUTS/coordinates.nc $EXP/.
	cp $INPUTS/coordinates.bdy.nc $EXP/.

Link to the tide data:

	ln -s $INPUTS $EXP/bdydta

Edit the namelist_cfg file::

	!-----------------------------------------------------------------------
	&namrun        !   parameters of the run
	!-----------------------------------------------------------------------
	  cn_exp      =  "AMMSURGE"  !  experience name
	  nn_it000    = 1   !  first time step
	  nn_itend    =  43200    !  last  time step (for dt = 6 min, 240*dt = 1 day)
	  nn_date0    =  20130101 !  date at nit_0000 (format yyyymmdd) used if ln_rstart=F or (ln_rstart=T and nn_rstctl=0 or 1)
	  nn_time0    =       0   !  initial time of day in hhmm
	  nn_leapy    =       1   !  Leap year calendar (1) or not (0)
	  ln_rstart   =  .false.  !  start from rest (F) or from a restart file (T)
	    nn_euler    =    1            !  = 0 : start with forward time step if ln_rstart=T
	    nn_rstctl   =    2            !  restart control ==> activated only if ln_rstart=T
	    !                             !    = 0 nn_date0 read in namelist ; nn_it000 : read in namelist
	    !                             !    = 1 nn_date0 read in namelist ; nn_it000 : check consistancy between namelist and restart
	    !                             !    = 2 nn_date0 read in restart  ; nn_it000 : check consistancy between namelist and restart
	    cn_ocerst_in    = "AMMSURGE_00043920_restart"   !  suffix of ocean restart name (input)
	    cn_ocerst_indir = "./Restart_files"         !  directory from which to read input ocean restarts
	    cn_ocerst_out   = "restart"   !  suffix of ocean restart name (output)
	    cn_ocerst_outdir= "./Restart_files"         !  directory in which to write output ocean restarts
	  nn_istate   =       0   !  output the initial state (1) or not (0)
	  nn_stock    =   43200    !  frequency of creation of a restart file (modulo referenced to 1)
	  nn_write    =   43200    !  frequency of write in the output file   (modulo referenced to nit000)
	/
	!-----------------------------------------------------------------------
	&namcfg        !   parameters of the configuration
	!-----------------------------------------------------------------------
	   ln_read_cfg = .true.   !  (=T) read the domain configuration file
	                          !  (=F) user defined configuration  ==>>>  see usrdef(_...) modules
	   cn_domcfg = "domain_cfg"         ! domain configuration filename
	/
	!-----------------------------------------------------------------------
	&namdom        !   space and time domain (bathymetry, mesh, timestep)
	!-----------------------------------------------------------------------
	   ln_2d        = .true.  !  (=T) run in 2D barotropic mode (no tracer processes or vertical diffusion)
	   rn_rdt      =   360.    !  time step for the dynamics (and tracer if nn_acc=0)
	/

	!-----------------------------------------------------------------------
	&namtsd    !   data : Temperature  & Salinity
	!-----------------------------------------------------------------------
	   ln_tsd_init   = .false.   !  Initialisation of ocean T & S with T &S input data (T) or not (F)
	   ln_tsd_tradmp = .false.   !  damping of ocean T & S toward T &S input data (T) or not (F)
	/
	!-----------------------------------------------------------------------
	&namsbc        !   Surface Boundary Condition (surface module)
	!-----------------------------------------------------------------------
	   nn_fsbc     = 1         !  frequency of surface boundary condition computation
	                           !     (also = the frequency of sea-ice model call)
	   ln_usr = .true.
	   ln_blk =  .false.
	   ln_apr_dyn  = .false.    !  Patm gradient added in ocean & ice Eqs.   (T => fill namsbc_apr )
	   nn_ice      = 0         !  =0 no ice boundary condition   ,
	   ln_rnf      = .false.   !  Runoffs                                   (T => fill namsbc_rnf)
	   ln_ssr      = .false.   !  Sea Surface Restoring on T and/or S       (T => fill namsbc_ssr)
	   ln_traqsr   = .false.   !  Light penetration in the ocean            (T => fill namtra_qsr)
	   nn_fwb      = 0         !  FreshWater Budget: =0 unchecked
	/
	!-----------------------------------------------------------------------
	&namsbc_usr  !   namsbc_surge   surge model fluxes
	!-----------------------------------------------------------------------
	   ln_use_sbc  = .false.    ! (T) to turn on surge fluxes (wind and pressure only)
	                            ! (F) for no fluxes (ie tide only case)

	!
	!              !  file name                    ! frequency (hours) ! variable  ! time interp. !  clim  ! 'yearly'/ ! weights  ! rotation !
	!              !                               !  (if <0  months)  !   name    !   (logical)  !  (T/F) ! 'monthly' ! filename ! pairing  !
	   sn_wndi     = 'windspd_u_amm7'              ,       1           ,'x_wind',   .true.     , .false. , 'daily'  ,'' , ''
	   sn_wndj     = 'windspd_v_amm7'              ,       1           ,'y_wind',   .true.     , .false. , 'daily'  ,'' , ''
	   cn_dir      = './fluxes/'          !  root directory for the location of the bulk files
	   rn_vfac     = 1.                   !  multiplicative factor for ocean/ice velocity
	                                      !  in the calculation of the wind stress (0.=absolute winds or 1.=relative winds)
	   rn_charn_const = 0.0275
	/
	!-----------------------------------------------------------------------
	&namtra_qsr    !   penetrative solar radiation
	!-----------------------------------------------------------------------
	   ln_traqsr   = .false.   !  Light penetration (T) or not (F)
	   nn_chldta   =      0    !  RGB : Chl data (=1) or cst value (=0)
	/
	!-----------------------------------------------------------------------
	&namsbc_apr    !   Atmospheric pressure used as ocean forcing or in bulk
	!-----------------------------------------------------------------------
	!          !  file name  ! frequency (hours) ! variable  ! time interp. !  clim  ! 'yearly'/ ! weights  ! rotation ! land/sea mask !
	!          !             !  (if <0  months)  !   name    !   (logical)  !  (T/F) ! 'monthly' ! filename ! pairing  ! filename      !
	   sn_apr= 'pressure_amm7',        1         ,   'air_pressure_at_sea_level' ,    .true.    , .false., 'daily'   ,  ''      ,   ''     ,  ''
	   cn_dir      = './fluxes/'!  root directory for the location of the bulk files
	   rn_pref     = 101200.    !  reference atmospheric pressure   [N/m2]/
	   ln_ref_apr  = .false.    !  ref. pressure: global mean Patm (T) or a constant (F)
	   ln_apr_obc  = .true.     !  inverse barometer added to OBC ssh data
	/
	!-----------------------------------------------------------------------
	&namlbc        !   lateral momentum boundary condition
	!-----------------------------------------------------------------------
	!   rn_shlat    =     0     !  shlat = 0  !  0 < shlat < 2  !  shlat = 2  !  2 < shlat
	                           !  free slip  !   partial slip  !   no slip   ! strong slip
	/

	!-----------------------------------------------------------------------
	&nam_tide      !   tide parameters
	!-----------------------------------------------------------------------
	   ln_tide     = .true.
	   rdttideramp =    1.
	   clname(1)     =   'M2'   !  name of constituent
	   clname(2)     =   'S2'
	   clname(3)     =   'K2'
	/
	!-----------------------------------------------------------------------
	&nambdy        !  unstructured open boundaries
	!-----------------------------------------------------------------------
	   ln_bdy     = .true.
	   nb_bdy         = 1                    !  number of open boundary sets
	   cn_coords_file = 'bdydta/coordinates.bdy.nc' !  bdy coordinates files
	   cn_dyn2d       = 'flather'            !
	   nn_dyn2d_dta   =  2                   !  = 0, bdy data are equal to the initial state
	                                         !  = 1, bdy data are read in 'bdydata   .nc' files
	                                         !  = 2, use tidal harmonic forcing data from files
	                                         !  = 3, use external data AND tidal harmonic forcing
	   cn_tra        =  'frs'                !
	   nn_tra_dta    =  0                    !  = 0, bdy data are equal to the initial state
	                                         !  = 1, bdy data are read in 'bdydata   .nc' files
	   nn_rimwidth   = 1                    !  width of the relaxation zone
	/
	!-----------------------------------------------------------------------
	&nambdy_tide     ! tidal forcing at open boundaries
	!-----------------------------------------------------------------------
	   filtide      = 'bdydta/ACCORD_bdytide_rotT_'         !  file name root of tidal forcing files
	   ln_bdytide_2ddta = .false.
	/
	!-----------------------------------------------------------------------
	&nambfr        !   bottom friction
	!-----------------------------------------------------------------------
	   nn_bfr      =    2      !  type of bottom friction :   = 0 : free slip,  = 1 : linear friction
	                           !                              = 2 : nonlinear friction
	   rn_bfri2    =    2.4e-3 !  bottom drag coefficient (non linear case)
	   rn_bfeb2    =    0.0e0  !  bottom turbulent kinetic energy background  (m2/s2)
	   ln_loglayer =   .false. !  loglayer bottom friction (only effect when nn_bfr = 2)
	   rn_bfrz0    =    0.003  !  bottom roughness (only effect when ln_loglayer = .true.)
	/
	!-----------------------------------------------------------------------
	&nambbc        !   bottom temperature boundary condition
	!-----------------------------------------------------------------------
	   ln_trabbc   = .false.   !  Apply a geothermal heating at the ocean bottom
	/
	!-----------------------------------------------------------------------
	&nambbl        !   bottom boundary layer scheme
	!-----------------------------------------------------------------------
	   nn_bbl_ldf  =  0      !  diffusive bbl (=1)   or not (=0)
	/
	!-----------------------------------------------------------------------
	&nameos        !   ocean physical parameters
	!-----------------------------------------------------------------------
	   ln_teos10   = .true.         !  = Use TEOS-10 equation of state
	/
	!-----------------------------------------------------------------------
	&namdyn_vor    !   option of physics/algorithm (not control by CPP keys)
	!-----------------------------------------------------------------------
	   ln_dynvor_een = .true.  !  energy & enstrophy scheme
	/
	!-----------------------------------------------------------------------
	&namdyn_hpg    !   Hydrostatic pressure gradient option
	!-----------------------------------------------------------------------
	   ln_hpg_zps  = .false.   !  z-coordinate - partial steps (interpolation)
	   ln_hpg_sco  = .true.    !  s-coordinate (Standard Jacobian scheme)
	/
	!-----------------------------------------------------------------------
	&namdyn_spg    !   surface pressure gradient   (CPP key only)
	!-----------------------------------------------------------------------
	   ln_dynspg_ts = .true.    ! split-explicit free surface
	   ln_bt_auto =    .true.           !  Set nn_baro automatically to be just below
	                                       !  a user defined maximum courant number (rn_bt_cmax)
	/
	!-----------------------------------------------------------------------
	&namdyn_ldf    !   lateral diffusion on momentum
	!-----------------------------------------------------------------------
	   !                       !  Type of the operator :
	   ln_dynldf_blp  =  .true.   !  bilaplacian operator
	   ln_dynldf_lap    =  .false.  !  bilaplacian operator
	   !                       !  Direction of action  :
	   ln_dynldf_lev  =  .true.   !  iso-level
	                           !  Coefficient
	   rn_ahm_0     = 60.0      !  horizontal laplacian eddy viscosity   [m2/s]
	   rn_bhm_0     = -1.0e+9   !  horizontal bilaplacian eddy viscosity [m4/s]
	/
	!-----------------------------------------------------------------------
	&namzdf        !   vertical physics
	!-----------------------------------------------------------------------
	   rn_avm0     =   0.1e-6  !  vertical eddy viscosity   [m2/s]          (background Kz if not "key_zdfcst")
	   rn_avt0     =   0.1e-6  !  vertical eddy diffusivity [m2/s]          (background Kz if not "key_zdfcst")
	   ln_zdfevd   = .false.   !  enhanced vertical diffusion (evd) (T) or not (F)
	   nn_evdm     =    1      !  evd apply on tracer (=0) or on tracer and momentum (=1)
	/
	!-----------------------------------------------------------------------
	&nam_diaharm   !   Harmonic analysis of tidal constituents ('key_diaharm')
	!-----------------------------------------------------------------------
	    nit000_han = 1     ! First time step used for harmonic analysis
	    nitend_han = 43200     ! Last time step used for harmonic analysis
	    nstep_han  = 5         ! Time step frequency for harmonic analysis
	    tname(1)   = 'M2'      ! Name of tidal constituents
	    tname(2)   = 'S2'
	    tname(3)   = 'K2'
	/
	!-----------------------------------------------------------------------
	&namwad       !   Wetting and Drying namelist
	!-----------------------------------------------------------------------
	   ln_wd = .false.   !: key to turn on/off wetting/drying (T: on, F: off)
	   rn_wdmin1=0.1     !: minimum water depth on dried cells
	   rn_wdmin2 = 0.01  !: tolerrance of minimum water depth on dried cells
	   rn_wdld   = 20.0  !: land elevation below which wetting/drying will be considered
	   nn_wdit   =   10  !: maximum number of iteration for W/D limiter
	/

Edit the following in namelist_cfg to define the surge boundaries::

	!-----------------------------------------------------------------------
	&namsbc
	!-----------------------------------------------------------------------
	  ln_usr = .true.
	  ln_apr_dyn = .true.

	!-----------------------------------------------------------------------
	&namsbc_usr
	!-----------------------------------------------------------------------
	  ln_use_sbc = .true.
	  !              !  file name                    ! frequency (hours) ! variable  ! time interp. !  clim  ! 'yearly'/ ! weights  ! rotation ! land/sea mask !
	  !              !                               !  (if <0  months)  !   name    !   (logical)  !  (T/F) ! 'monthly' ! filename ! pairing  ! filename      !
	     sn_wndi     = 'EAfrica_u10'              ,       1           ,'u10',   .false.     , .false. , 'week_mon'  ,'weights_bicubic_u10' , '' , ''
	     sn_wndj     = 'EAfrica_v10'              ,       1           ,'v10',   .false.     , .false. , 'week_mon'  ,'weights_bicubic_v10' , '' , ''
	  !   sn_wndi     = 'EAfrica_u10'              ,       1           ,'u10',   .false.     , .false. , 'monthly'  ,'weights_bicubic_u10' , '' , ''
	  !   sn_wndj     = 'EAfrica_v10'              ,       1           ,'v10',   .false.     , .false. , 'monthly'  ,'weights_bicubic_v10' , '' , ''

	!-----------------------------------------------------------------------
	&namsbc_apr
	!-----------------------------------------------------------------------
	  !          !  file name  ! frequency (hours) ! variable  ! time interp. !  clim  ! 'yearly'/ ! weights  ! rotation ! land/sea mask !
	  !          !             !  (if <0  months)  !   name    !   (logical)  !  (T/F) ! 'monthly' ! filename ! pairing  ! filename      !
	     sn_apr= 'EAfrica_msl',        1         ,   'msl' ,    .false.    , .false., 'week_mon'   ,  'weights_bicubic_msl'      ,   ''     ,  ''
	  !   sn_apr= 'EAfrica_msl',        1         ,   'msl' ,    .false.    , .false., 'monthly'   ,  'weights_bicubic_msl'      ,   ''     ,  ''