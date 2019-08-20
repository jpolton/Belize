

First need to get the Input and Start_Files to build the config::

	cd $WDIR
	cp INPUTS
	cp START_FILES

To find specific longitudes or latitudes you can::

	ipython
	from netCDF4 import Dataset
	import numpy as np
	fn = 'coordinates_ORCA_R12.nc'
	nc_fid = Dataset(fn,'r')
	lat = nc_fid.variables['nav_lat'][:]
	lon = nc_fid.variables['nav_lon'][:]
	np.abs(lon[1000,:] - 20.0).argmin()
	np.abs(lon[1000,:] - 65.0).argmin()
	np.abs(lat[:,4225] - -5.0).argmin()
	np.abs(lat[:,4225] - -38.0).argmin()

For this example, we are using the interval i = 3695:4225 and j = 1000:1434 which is around 20E-65E and 38S-5S. To obtain coords for this domain a namelist file is required::

	cd $TDIR/NESTING
	nano namelist.input

	&input_output
	    iom_activated = true
	/
	&coarse_grid_files
	    parent_coordinate_file = 'coordinates_ORCA_R12.nc'
	/
	&bathymetry
	/
	&nesting
	    imin = 3685
	    imax = 4225
	    jmin = 1000
	    jmax = 1434
	    rho  = 1
	    rhot = 1
	    bathy_update = false
	/
	&vertical_grid
	/
	&partial_cells
	/
	&nemo_coarse_grid
	/
	&forcing_files
	/
	&interp
	/
	&restart
	/
	&restart_trc
	/	

The coordinates file now needs to built. Move to the TOOL directory::

	cd $TDIR
	./maketools -n NESTING

This will have built some executables in the NESTING subdirectory::
	
	cd NESTING

The ORCA R12 netcdf now needs to be linked in::

	ln -s $INPUTS/coordinates_ORCA_R12.nc $TDIR/NESTING/.

The tool then needs to be executed::

	./agrif_create_coordinates.exe

This will produce the following in the terminal::
	
	root@d8f6bc244d55:/SRC/NEMOGCM/TOOLS/NESTING# ./agrif_create_coordinates.exe 
	  
	 Reading coordinates file: coordinates_ORCA_R12.nc
	  
	  
	 Size of the High resolution grid:          544  x          438
	  
	  
	 Writing coordinates file: 1_coordinates_ORCA_R12.nc
	  
	 Child domain position : 
	 latmin =  -38.022836661633150     
	 latmax =  -5.0766774048039940     
	 lonmin =   20.000000000000000     
	 lonmax =   64.916666666666572  

And create a coordinates file (need to install ncdump package first)::
	
	apt-get install netcdf-bin

	ncdump -h 1_coordinates_ORCA_R12.nc
	netcdf \1_coordinates_ORCA_R12 {
	dimensions:
		x = 544 ;
		y = 438 ;
	variables:
		float nav_lon(y, x) ;
			nav_lon:units = "degrees_east" ;
			nav_lon:valid_min = 19.83333f ;
			nav_lon:valid_max = 65.08334f ;
			nav_lon:long_name = "Longitude" ;
		float nav_lat(y, x) ;
			nav_lat:units = "degrees_north" ;
			nav_lat:valid_min = -38.15401f ;
			nav_lat:valid_max = -4.910644f ;
			nav_lat:long_name = "Latitude" ;
		double glamt(y, x) ;
			glamt:missing_value = 1.e+20f ;
		double glamu(y, x) ;
			glamu:missing_value = 1.e+20f ;
		double glamv(y, x) ;
			glamv:missing_value = 1.e+20f ;
		double glamf(y, x) ;
			glamf:missing_value = 1.e+20f ;
		double gphit(y, x) ;
			gphit:missing_value = 1.e+20f ;
		double gphiu(y, x) ;
			gphiu:missing_value = 1.e+20f ;
		double gphiv(y, x) ;
			gphiv:missing_value = 1.e+20f ;
		double gphif(y, x) ;
			gphif:missing_value = 1.e+20f ;
		double e1t(y, x) ;
			e1t:missing_value = 1.e+20f ;
		double e1u(y, x) ;
			e1u:missing_value = 1.e+20f ;
		double e1v(y, x) ;
			e1v:missing_value = 1.e+20f ;
		double e1f(y, x) ;
			e1f:missing_value = 1.e+20f ;
		double e2t(y, x) ;
			e2t:missing_value = 1.e+20f ;
		double e2u(y, x) ;
			e2u:missing_value = 1.e+20f ;
		double e2v(y, x) ;
			e2v:missing_value = 1.e+20f ;
		double e2f(y, x) ;
			e2f:missing_value = 1.e+20f ;

This needs to be copied to the $INPUTS directory:

	cp 1_coordinates_ORCA_R12.nc $INPUTS/coordinates.nc
