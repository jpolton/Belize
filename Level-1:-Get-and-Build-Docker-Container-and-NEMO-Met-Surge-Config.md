I used this tutorial created by Pierre DERIAN with some changes to reflect the relevent revison of XIOS2 and the metoffice surge nemo code (different to main trunk) Derian's git hub is here https://github.com/pderian/NEMOGCM-Docker

Follow the steps below as there is some differences to Pierre's method.
Create workdirectory e.g. mkdir $HOME/nemo-nowcast-docker::

	mkdir $HOME/nemo-nowcast-docker
	cd $HOME/nemo-nowcast-docker

Git clone Pierre's github repository in a directory structure::

	mkdir SRC; cd SRC
	mkdir pderian; cd pderian
	git clone https://github.com/pderian/NEMOGCM-Docker .

Checkout NEMO code and XIOS code into directories at same level as NEMO-Docker::

	cd $HOME/nemo-nowcast-docker/SRC
	svn co -r 9709 http://forge.ipsl.jussieu.fr/nemo/svn/branches/UKMO/dev_r8814_surge_modelling_Nemo4/NEMOGCM NEMOGCM
	svn co -r 1229 http://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/trunk xios-2.0_r1229
	ln -s xios-2.0_r1229/ XIOS2

This should result in four folders with the NEMO code in one folder, and xios2.0 code in another (with a sym link to the xios-2.0 folder as XIOS2) and the pderian folder. Copy the arch files that came from Pierre's github.::

	cd $HOME/nemo-nowcast-docker/SRC
	cp pderian/arch_NEMOGCM/arch* NEMOGCM/ARCH; cp pderian/arch_XIOS/arch* XIOS2/arch

Edit the DEBIAN arch file to point to XIOS2 not XIOS::

  	nano $HOME/nemo-nowcast-docker/SRC/NEMOGCM/ARCH/arch-DEBIAN.fcm
	...
	%XIOS_HOME           /SRC/XIOS2

The docker image can now be built, (currently use pierre's orginal dockerfile but will be modified to simplify the set up in the future.)::

	cd pderian
	cd Docker
	docker build -t nemo/compiler .

You may need to add the user to the docker group::

	$ sudo usermod -aG docker $USER

You will need to log out and then back in.

The image can now be run, the path to SRC needs to be absolute, so switch
``/Users/jeff`` to the output of "echo $HOME"::

	docker run -v /Users/jeff/nemo-nowcast-docker/SRC:/SRC -t -i nemo/compiler /bin/bash

This should result in the container running and the terminal will move to the container e.g. (root@"container id"#) XIOS can now be compiled::

	cd SRC
	cd XIOS2
	./make_xios --dev --netcdf_lib netcdf4_seq --arch DEBIAN

This should successfully build and result in an executable in the XIOS
 directories. Some environmental variables need to be defined (this can't be
  done until inside the container)::

	export CONFIG=<config_name>
	export WORK=/SRC
	export WDIR=/SRC
	export INPUTS=$WDIR/INPUTS
	export START_FILES=$WDIR/START_FILES
	export CDIR=$WDIR/NEMOGCM/CONFIG
	export TDIR=$WDIR/NEMOGCM/TOOLS
	export EXP=$CDIR/$CONFIG/EXP00

NEMO can now be built::

	cd $CDIR
	./makenemo -n $CONFIG -m DEBIAN clean

Answer yes to the first question (OPA_SRC), no to all the others.

the XIOS_server.exe can now be linked::

	ln -s  $WDIR/xios-2.0_r1080/bin/xios_server.exe $EXP/xios_server.exe

Check the compile flags (In nano: Ctrl-O to save. Ctrl-X to quit)::

	nano $CONFIG/cpp_$CONFIG.fcm
	bld::tool::fppkeys  key_nosignedzero key_diainstant key_mpp_mpi key_iomput

Then build NEMO again::

	./makenemo -n $CONFIG -m DEBIAN
