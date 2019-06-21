# tcpdump-little-book

[Tcpdump](https://www.tcpdump.org/) is a powerful command line tool to analyze network packets on `Unix-like` Operating Systems; it is indispensable for debugging network related issues. Run `tcpdump` in your terminal:  

	# tcpdump
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on enp0s25, link-type EN10MB (Ethernet), capture size 262144 bytes
	08:57:41.148740 IP6 fe80::846b:2555:fb41:1fa8.dhcpv6-client > ff02::1:2.dhcpv6-server: dhcp6 solicit
	08:57:41.208960 IP archlinux.ssh > 10.217.133.206.55977: Flags [P.], seq 687245846:687246034, ack 4010852751, win 501, length 188
	......

Without any options and expression, `tcpdump` works in a live-capture mode (the source code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/e6eab7bccfbf8fe9c386e16a9c5441e7a57066ae/tcpdump.c#L2024)):  

	......
			/*
			 * We're doing a live capture.
			 */
			if (device == NULL) {
				/*
				 * No interface was specified.  Pick one.
				 */
	#ifdef HAVE_PCAP_FINDALLDEVS
				/*
				 * Find the list of interfaces, and pick
				 * the first interface.
				 */
				if (pcap_findalldevs(&devlist, ebuf) == -1)
					error("%s", ebuf);
				if (devlist == NULL)
					error("no interfaces available for capture");
				device = strdup(devlist->name);
				pcap_freealldevs(devlist);
	#else /* HAVE_PCAP_FINDALLDEVS */
				/*
				 * Use whatever interface pcap_lookupdev()
				 * chooses.
				 */
				device = pcap_lookupdev(ebuf);
				if (device == NULL)
					error("%s", ebuf);
	#endif
			}
	......

Depends on whether `HAVE_PCAP_FINDALLDEVS` macro is defined, `tcpudmp` will pick a "default" network interface to do capture work. Interesting, right? Since all is set, let's begin this whirlwind tour of `tcpdump`.  

P.S., this manual refers code and documents heavily from [tcpdump](https://www.tcpdump.org/) website, and kudos to `tcpdump` guys! If the small booklet gives you some help, please give it a star in [github](https://github.com/NanXiao/tcpdump-little-book). :-)
	 
