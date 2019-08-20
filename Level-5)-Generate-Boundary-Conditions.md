Now we need to install PyNEMO, this is a boss level!!

First we need to install miniconda::

	$ cd $WDIR
	$ mkdir CONDA
	$ apt-get install bzip2
	$ apt-get install wget
	$ export DATA1=/$WDIR/CONDA
	$ export MINICONDA_INSTALLER=http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
	$ wget -q ${MINICONDA_INSTALLER} -O ${DATA1}/miniconda.sh
	$ bash ${DATA1}/miniconda.sh -b -p ${DATA1}/miniconda
	$ export CONDA_BIN=${DATA1}/miniconda/bin
	$ echo export PATH=${CONDA_BIN}:\${PATH} >> ${HOME}/.bashrc
	$ source ~/.bashrc #(ACTIVATE!!!)

Then a virtual python environment to run NRCT needs to be created (this has hasn't worked on the docker image, it seems due to Apple machines not having case sensitive file systems!) Have moved to Livljobs4

Update: Now redoing the recipe in a docker on a DEBIAN virtual machine, will see if this works::	

	conda create --name nrct_env scipy numpy matplotlib basemap netcdf4=1.3.1 libgfortran
	source activate nrct_env

Install the conda NRCT packages::

	conda install -c https://conda.anaconda.org/conda-forge seawater=3.3.4 # Note had to add https path
	conda install -c https://conda.anaconda.org/srikanthnagella thredds_crawler
	conda install -c https://conda.anaconda.org/srikanthnagella pyjnius

Install java environment::

	apt-get install default-jre

Location of libjvm.so file::

	/usr/lib/jvm/java-7-openjdk-amd64/jre/lib/amd64/server

Now I need to add this location/path as an environment variable::

	cd $WORK/$USER
	export LD_LIBRARY_PATH=/usr/lib/jvm/java-7-openjdk-amd64/jre/lib/amd64/server:$LD_LIBRARY_PATH

Then I need to clone the following bitbucket repo::
	apt-get install git
	git clone https://github.com/jdha/PyNEMO.git 


Now NRCT needs to be installed::

	cd $WORK/$USER/PyNEMO
	touch DESCRIPTION.rst #currently need to create an empty rst file for this to work
	python setup.py build
	python setup.py install

Six files are required by NRCT::

	namelist.bdy
	inputs_src.ncml
	inputs_dst.ncml
	mask_src.nc
	mesh_hgr_src.nc
	mesh_zgr_src.nc

These can be copied from start_files if required::

	cd $INPUTS
	cp $START_FILES/NRCT/* .

	pynemo -s namelist.bdy
