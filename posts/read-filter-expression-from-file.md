# Read filter expression from file

The filter expression can be read from file. E.g.:  

	# cat filter
	port 80

"`-F file`" option can be used to read filter from file instead of command line:  

	# tcpdump -F filter
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on enp0s3, link-type EN10MB (Ethernet), capture size 262144 bytes
	......

The code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/511915bef7e4de2f31b8d9f581b4a44b0cfbcf53/tcpdump.c#L2144):  

	......
	if (infile)
		cmdbuf = read_infile(infile);
	else
		cmdbuf = copy_argv(&argv[optind]);
	......

