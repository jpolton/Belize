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