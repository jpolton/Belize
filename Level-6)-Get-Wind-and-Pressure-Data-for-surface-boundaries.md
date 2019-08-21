First we need data, current example uses some 2010 data from the ERA5 dataset that has been downloaded from ECMWF or Copernicus? These are large files so a subset needs to be extracted. It needs to be slightly larger than the domain of the model.::

	ncea -d latitude,-39.0,-4.0 -d longitude,19.0,66.0 /START_FILES/Forcing/msl_2010.nc EAfrica_msl_2010.nc
	ncea -d latitude,-39.0,-4.0 -d longitude,19.0,66.0 /START_FILES/Forcing/u10_2010.nc EAfrica_u10_2010.nc
	ncea -d latitude,-39.0,-4.0 -d longitude,19.0,66.0 /START_FILES/Forcing/v10_2010.nc EAfrica_v10_2010.nc	

Now a time period needs to be extracted from this data, a 2 weekly period which coincides with a tropical depression in the vincity. An example of this is 21 Jan 10 to 3 Feb 10. To do this requires a python script that calculates the indices required::

	ipython

	import netCDF4 as nc
	import numpy as np
	from datetime import datetime

	ncfile = nc.Dataset('/work/anwise/DATA/ERA5/EAfrica_msl_2010.nc', 'r')
	time = ncfile.variables['time']
	dates = nc.num2date(time[:], time.units, time.calendar)

	# print index of date (year,month,day,hour,min) in time array
	idx = np.argwhere(dates==datetime(2010,1,21,0,0))
	idx
	time[idx]
	dates[idx].strftime("%T %A %d. %B %Y")
	ncfile.close()

Now with the indices calculated, the 2 weeks of data can be extracted from the datasets (the output names are required by NEMO)::

	ncea -d time,480,647 EAfrica_msl_2010.nc EAfrica_msl_y2010m01d21.nc
	ncea -d time,648,815 EAfrica_msl_2010.nc EAfrica_msl_y2010m01d28.nc

	ncea -d time,480,647 EAfrica_u10_2010.nc EAfrica_u10_y2010m01d21.nc
	ncea -d time,648,815 EAfrica_u10_2010.nc EAfrica_u10_y2010m01d28.nc

	ncea -d time,480,647 EAfrica_v10_2010.nc EAfrica_v10_y2010m01d21.nc
	ncea -d time,648,815 EAfrica_v10_2010.nc EAfrica_v10_y2010m01d28.nc

These files now need to be copied over to the Docker instance of NEMO::

	cp $INPUTS/EAfrica_* /SRC/INPUTS/.

Surface Boundary conditions can now be generated.

We need some files from the START_FILES folder::

	cp $START_FILES/namelist_reshape_bilin_atmos $INPUTS/.
	cp $START_FILES/namelist_reshape_bicubic_atmos $INPUTS/.

Then a bash script is required to process and generate the weighted bicubic file::

	vim make_weights_bicubic.sh

	#!/bin/bash
	# Within the bilinear and bicubic namelists ensure that:
	# 1. the name of the data input_file is correct
	# 2. the name of the NEMO coordinate file for nemo_file is correct
	# 3. the input_lon, input_lat, nemo_lon, nemo_lat variables
	#    correspond to the approriate fields in your input_file and nemo_file

	/SRC/NEMOGCM/TOOLS/WEIGHTS/scripgrid.exe namelist_reshape_bilin_atmos
	/SRC/NEMOGCM/TOOLS/WEIGHTS/scrip.exe namelist_reshape_bilin_atmos
	/SRC/NEMOGCM/TOOLS/WEIGHTS/scripshape.exe namelist_reshape_bilin_atmos
	/SRC/NEMOGCM/TOOLS/WEIGHTS/scrip.exe namelist_reshape_bicubic_atmos
	/SRC/NEMOGCM/TOOLS/WEIGHTS/scripshape.exe namelist_reshape_bicubic_atmos

	rm remap_nemo_grid_atmos.nc
	rm remap_data_grid_atmos.nc
	rm data_nemo_bilin_atmos.nc
	rm weights_bilinear_atmos.nc
	rm data_nemo_bicubic_atmos.nc	

We will run this script file 3 times, once for msl, once for u10 and once for v10. Each time before running the script change some things in the 2 namelist files::

	1. input_file must be set to one of the 6 data files e.g. EAfrica_msl_y2010m01d21.nc
	(I changed each time to one of the two msl, u10 and v10 input files)
	2. nemo_file must be set to the NEMO coordinate file we created eariler
	3. input_lon, input_lat, nemo_lon, nemo_lat must be set to match what is used in the input_file and nemo_file respectively
	4. In namelist_reshape_bicubic_atmos only, under &shape_inputs section, rename output_file to e.g. EAfrica_msl_weights_bicubic.nc
	
Run the script::

	./make_weights_bicubic.sh

I found I had to enter the name of the namelist file for each of the 5 exe in the script file. Make sure to enter them the correct number of times! bilin 3 times then bicubic twice. This will have created a weight file. Change namelist as above for msl,u10,v10 and repeat.
Should now have 3 files EAfrica_msl_weights_bicubic.nc, EAfrica_u10_weights_bicubic.nc and EAfrica_v10_weights_bicubic.nc.
Copy the data and weight files to experiment directory::

	mkdir $EXP/fluxes
	cp EAfrica_* $EXP/fluxes/

