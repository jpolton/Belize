## First section covers how to build and run a NEMO tide and surge model in a docker container

### Topics covered:

* Setup and build XIOS and NEMO on a docker image
* Create 12th degree coordinates file for desired region
* Generate bathymetry file for this region
* Generate a domain configuration file suitable for surge model
* Generate tide boundary conditions
* Generate wind and pressure boundary conditions
* Run with tides and surges forcing

## Second section covers how to build and use operational components to run the NEMO model on a daily basis and provide storm surge warnings..

### Topics covered:
* Setup a docker container with the right dependancies
* Setup and install the nowcast system
* Adapt to suit our requirements