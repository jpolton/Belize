Start up the container with the run command (if you shut the container down)::

	docker start "container id"

Now we need to install miniconda, this will allow us to set up and curate python environments etc.

	$ export WDIR=/SRC
	$ export DATA1=$WDIR/CONDA
	$ MINICONDA_INSTALLER=http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
	$ wget -q ${MINICONDA_INSTALLER} -O ${DATA1}/miniconda.sh
	$ bash ${DATA1}/miniconda.sh -b -p ${DATA1}/miniconda
	$ export CONDA_BIN=${DATA1}/miniconda/bin
	$ echo export PATH=${CONDA_BIN}:\${PATH} >> ${HOME}/.bashrc

To make the path changes made in the last command update::

	source ~/.bashrc

Now we need to clone the Nowcast Repo's that we will be using::
	
	cd $WDIR
	hg clone https://bitbucket.org/43ravens/nemo_nowcast NEMO_Nowcast
    hg clone https://bitbucket.org/gomss-nowcast/gomss_nowcast GoMSS_Nowcast
    hg clone https://bitbucket.org/salishsea/nemo-cmd NEMO-Cmd

Now we need to set some environment variables::

	$ export CONDA=${CONDA_BIN}/conda
	$ export NOWCAST_SYS=/SRC
	$ export NOWCAST_ENV=${NOWCAST_SYS}/nowcast-env
	$ export PIP=${NOWCAST_ENV}/bin/pip

Now we need to create the nowcast conda python environment::
	
	 ${CONDA} create --channel defaults --channel gomss-nowcast --channel conda-forge \
	 --prefix ${NOWCAST_ENV} python=3 pip \
	 arrow attrs bottleneck circus dask pynco pyyaml pyzmq requests schedule \
	 xarray
	$ ${PIP} install raven python-hglib
	$ echo source activate ${NOWCAST_ENV} >> ${HOME}/.bashrc

The to activate the environment reload the bashrc file, (the environment will automatically load when logging in from now on)::

	source ~/.bashrc

Now the actual nowcast packages need installing::

	${PIP} install --editable NEMO-Cmd
	${PIP} install --editable NEMO_Nowcast
	${PIP} install --editable GoMSS_Nowcast

**Note:** GoMSS_Nowcast installs with an error as it can’t find the pynco package. This is currently resolved by commenting out line 51 of the GoMSS_Nowcast/setup.py files so that it now longer trys to install it. The pynco functionality can be replicated using the python subprocess module to execute the relevant NCO commands. (Not sure how important this is yet)

Now we need to create directories to store log files, very important to be able to debug and identifiy any issues.::

	mkdir $WDIR/logging
	mkdir $WDIR/logging/nowcast

Config files that define the system need to be created (copied from GoMSS repo)::

	$ cd GoMSS_Nowcast
	$ cp config/. $NOWCAST_SYS