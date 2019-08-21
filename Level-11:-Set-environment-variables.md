The nowcast system uses several environment variables to pass configuration information into the system::

	* NOWCAST_ENV: the path to the nowcast-env conda environment
	* NOWCAST_CONFIG: the directory in which the system configuration files are stored
	* NOWCAST_YAML: the path and name of the nowcast system configuration file
	* NOWCAST_LOGS: the directory in which the system log files are stored

To ensure that these environment variables are set at all times when we are working with the nowcast system we use the conda environment activate/deactivate hooks feature.
The environment variables are set upon activation of the nowcast-env environment by creating an activate hook shell script in ${NOWCAST_ENV}/etc/conda/activate.d/::

	$ mkdir -p ${NOWCAST_ENV}/etc/conda/activate.d
	$ cat << EOF > ${NOWCAST_ENV}/etc/conda/activate.d/envvars.sh
	export NOWCAST_SYS=/SRC
	export NOWCAST_ENV=$NOWCAST_SYS/nowcast-env
	export NOWCAST_CONFIG=$NOWCAST_SYS/config
	export NOWCAST_YAML=$NOWCAST_SYS/config/nowcast.yaml
	export NOWCAST_LOGS=$NOWCAST_SYS/logging/nowcast
	EOF

Deletion of the environment variables upon deactivation of the environment is done by creating a deactivate hook shell script in ${NOWCAST_ENV}/etc/conda/deactivate.d/::

	$ mkdir -p ${NOWCAST_ENV}/etc/conda/deactivate.d
	$ cat << EOF > ${NOWCAST_ENV}/etc/conda/deactivate.d/envvars.sh
	unset NOWCAST_SYS
	unset NOWCAST_ENV
	unset NOWCAST_CONFIG
	unset NOWCAST_YAML
	unset NOWCAST_LOGS
	EOF

Now the environment shoud set and unset when loggin in and out.