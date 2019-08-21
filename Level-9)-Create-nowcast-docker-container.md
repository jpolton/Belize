I adapted the tutorial provided by Pierre Derian, he wrote a docker file that would run NEMO, the NOWCAST system has a much simplier set of requirements I wrote the file below::

	#### Installs the framework for the NEMO Nowcast system #####
	#############################################################
	FROM debian:jessie
	MAINTAINER Thomas Prime, thopri@noc.ac.uk

	### dependancies for nowcast
	# bash, svn, mercurical, git, ssh
	# nano and vim are useful to edit files etc
	ENV PACKAGES_NOWCAST="subversion git mercurial ssh wget bzip2" \
	PACKAGES_USER="nano vim"
	## first update then install
	RUN apt-get update -y && \
	apt-get install -y --no-install-recommends ${PACKAGES_NOWCAST} ${PACKAGES_USER}

This will build a docker container with Debian Jessie with bash, svn, mwecurical, git and ssh. There are also the editors nano and vim. Other packages are required but these will be install manually for now. To use this dockerfile::

	mkdir nowcast-docker (I created this in my home directory)
	export WDIR=/home/$USER/nowcast-docker/ (this may be different for different architechtures)
	cd nowcast-docker
	mkdir Docker
	cd Docker
	nano Dockerfile
	paste in above and save
	docker build -t nowcast/build .

Now we need a folder to hold the nowcast system and to run it, the path to the SRC folder must be explicit::

	cd $WDIR
	mkdir SRC
	docker run -v $WDIR/SRC:/SRC -t -i nowcast/build /bin/bash

Now there should end up at the container shell prompt::

	root@3ad565a55648:/#
