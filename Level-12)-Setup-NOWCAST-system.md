$ cd $NOWCAST_CONFIG
	$ vi circus_logger.yaml

Edit the filename to match the logging directory setup. i.e.  /SRC/logging/nowcast/circus.log::

	$ :w
	$ :q

The nowcast.yaml now needs to commented out so that it matches the toy example. e.g. comment all the extra logging, workers and message registry. The sleep worker from the toy example needs to be added. Example added below:


The example workers need to be copied across, from NEMO_Nowcast to the nowcast module in GoMSS.::

	$ mv NEMO_Nowcast/nemo_nowcast/workers/sleep.py /SRC/GoMSS_Nowcast/nowcast/workers/

The important one is the sleep worker as the YAML file currently only references this worker. (Rest commented out)

Finally the nextworker.py file needs a definition of what to do after receiving a message from the sleep worker. (Currently nothing but usually would start the next worker)
This is added to the start of the networkers python script, before the first def defining the download weather worker::

	def after_sleep(msg, config, checklist):
	    """Calculate the list of workers to launch after the sleep example worker
	    ends.

	    :arg msg: Nowcast system message.
	    :type msg: :py:func:`collections.namedtuple`

	    :arg config: :py:class:`dict`-like object that holds the nowcast system
	                 configuration that is loaded from the system configuration
	                 file.
	    :type config: :py:class:`nemo_nowcast.config.Config`

	    :arg dict checklist: System checklist: data structure containing the
	                         present state of the nowcast system.

	    :returns: Sequence of :py:class:`nemo_nowcast.worker.NextWorker` instances
	              for worker(s) to launch next.
	    :rtype: list
	    """
	    next_workers = {
	        'crash': [],
	        'failure': [],
	        'success': []#NextWorker('nemo_nowcast.workers.awaken')],
	    }
	    return next_workers[msg.type]

currently required to downgrade a package as its not compatable with the current environment.::

    $ conda install tornado=4.5.3


The circus system can now be started, it should give debug info then start listening. (A warning due to there being no checklist from previous runs etc)::

	$ circusd $NOWCAST_CONFIG/circus.ini

The terminal will look like this::

	(/SRC/nowcast-env) root@eaac2b585334:/SRC# circusd $NOWCAST_CONFIG/circus.ini
	2018-06-01 11:53:58 circus[74] [INFO] Starting the stats streamer
	2018-06-01 11:53:58,347 INFO [message_broker] running in process 72
	2018-06-01 11:53:58,354 INFO [message_broker] read config from /SRC/config/nowcast.yaml
	2018-06-01 11:53:58,355 INFO [message_broker] writing logging messages to local file system
	2018-06-01 11:53:58,355 INFO [message_broker] worker socket bound to port 4344
	2018-06-01 11:53:58,355 INFO [message_broker] manager socket bound to port 4343
	2018-06-01 11:53:58,355 INFO [manager] running in process 71
	2018-06-01 11:53:58,356 INFO [manager] read config from /SRC/config/nowcast.yaml
	2018-06-01 11:53:58,356 INFO [manager] writing logging messages to local file system
	2018-06-01 11:53:58,357 INFO [manager] next workers module loaded from nowcast.next_workers
	2018-06-01 11:53:58,357 INFO [manager] connected to localhost port 4343
	2018-06-01 11:53:58,357 WARNING [manager] checklist load failed:
	Traceback (most recent call last):
	  File "/SRC/NEMO_Nowcast/nemo_nowcast/manager.py", line 243, in _load_checklist
	    with open(checklist_file, 'rt') as f:
	FileNotFoundError: [Errno 2] No such file or directory: '/SRC/logging/nowcast/nowcast_checklist.yaml'
	2018-06-01 11:53:58,359 WARNING [manager] running with empty checklist
	2018-06-01 11:53:58,359 DEBUG [manager] listening...
	2018-06-01 11:53:58,361 INFO [scheduler] running in process 73
	2018-06-01 11:53:58,361 INFO [scheduler] read config from /SRC/config/nowcast.yaml
	2018-06-01 11:53:58,361 INFO [scheduler] writing logging messages to local file system	

See the management processes (requires new terminal)::

	$circus-top

To get a bash shell in a running docker container the following command is required::

	docker exec -it <container name> /bin/bash

Control the processes::

	$circusctl
	$ help (gives all the options, list, stats etc)

Kill the circus::

	$circusctl quit
	Returns ‘ok’

To test the sleep worker, move to the workers directory (turns out this is not needed, worker commands can be made anywhere in docker container file system)::

	$ cd /SRC/GoMSS_Nowcast/nowcast/workers
	$ python -m nowcast.workers.sleep $NOWCAST_YAML

The output in the terminal will look like this::

	2018-06-01 11:57:53,586 INFO [sleep] running in process 109
	2018-06-01 11:57:53,587 INFO [sleep] read config from /SRC/config/nowcast.yaml
	2018-06-01 11:57:53,587 INFO [sleep] writing log messages to local file system
	2018-06-01 11:57:53,587 INFO [sleep] connected to localhost port 4344
	2018-06-01 11:57:58,588 INFO [sleep] slept for 5 seconds
	2018-06-01 11:57:58,590 DEBUG [sleep] sent message: (success) sleep worker slept well
	2018-06-01 11:57:58,595 DEBUG [sleep] received message from manager: (ack) message acknowledged
	2018-06-01 11:57:58,595 DEBUG [sleep] shutting down

Showing that the sleep worker, starts, reads its config, writes a log, sleeps for 5 seconds, sends success message and then gets an acknowledgement from the manager before shutting down.

The manger console prints the following::

	2018-05-02 11:58:57,514 DEBUG [manager] received message from sleep: (success) sleep worker slept well
	2018-05-02 11:58:57,515 INFO [manager] checklist updated with [sleepyhead] items from sleep worker
	2018-05-02 11:58:57,523 DEBUG [manager] listening...

Showing it has received the message from the worker, updated its checklist and then gone back to listening.

To start the circus manager without needing a terminal open it can be started as a Daemon as follows::

	$circusd --daemon $NOWCAST_CONFIG/circus.ini

This wiki shows how to get a basic nowcast system up and running on a docker container, however this is largely redundant as the current docker image has this built in. This method will be required if a completly new configuration/workspace is required.









