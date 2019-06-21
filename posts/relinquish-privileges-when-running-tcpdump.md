# Relinquish privileges when running tcpdump

In some scenarios, when `tcpdump` is running as `root`, after opening the capture device or input savefile, but before opening any savefiles for output, "`-Z user/--relinquish-privileges=user`" option can be used to switch to another user and drop privileges. E.g.:  

	# sudo tcpdump -Z nan
	dropped privs to nan
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	......
