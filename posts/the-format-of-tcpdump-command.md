# The format of tcpdump command

`Tcpdump`'s format is like following:  

	# tcpdump [options] [expression]

`Tcpdump` only captures packets whose content satisfy `expression` (the format of `expression` is defined [here](https://www.tcpdump.org/manpages/pcap-filter.7.html)). E.g., dump all `HTTP` protocol packets:   

	# tcpdump port 80
	14:59:05.989545 IP 192.168.35.211.53160 > 172.217.194.138.http: Flags [S], seq 3145761683, win 29200, options [mss 1460,sackOK,TS val 4055365378 ecr 0,nop,wscale 7], length 0
    14:59:05.994196 IP 172.217.194.138.http > 192.168.35.211.53160: Flags [S.], seq 1475154793, ack 3145761684, win 62392, options [mss 1430,sackOK,TS val 3581048241 ecr 4055365378,nop,wscale 8], length 0
    14:59:05.994235 IP 192.168.35.211.53160 > 172.217.194.138.http: Flags [.], ack 1, win 229, options [nop,nop,TS val 4055365383 ecr 3581048241], length 0
    ......
	^C
	32 packets captured
	36 packets received by filter
	4 packets dropped by kernel

For every packet, the format is timestamp since midnight followed by packet information. In previous example, the first packet is an `IP` protocol message: protocol, source address, destination address and `TCP SYN` parameters:  

	......
	14:59:05.989545 IP 192.168.35.211.53160 > 172.217.194.138.http: Flags [S], seq 3145761683, win 29200, options [mss 1460,sackOK,TS val 4055365378 ecr 0,nop,wscale 7], length 0
	......

After inputting "`Ctrl+C`" to terminate the `tcpdump` process, it also showed statistics of packets:  

	......
	32 packets captured
	36 packets received by filter
	4 packets dropped by kernel


This info is printed by [info](https://github.com/the-tcpdump-group/tcpdump/blob/65969779d7bfc916dbedc32fbcc8dbb49a4a19de/tcpdump.c#L2637) function:  

	static void
	info(int verbose)
	{
		struct pcap_stat stats;
	
		/*
		 * Older versions of libpcap didn't set ps_ifdrop on some
		 * platforms; initialize it to 0 to handle that.
		 */
		stats.ps_ifdrop = 0;
		if (pcap_stats(pd, &stats) < 0) {
			(void)fprintf(stderr, "pcap_stats: %s\n", pcap_geterr(pd));
			infoprint = 0;
			return;
		}
	
		if (!verbose)
			fprintf(stderr, "%s: ", program_name);
	
		(void)fprintf(stderr, "%u packet%s captured", packets_captured,
		    PLURAL_SUFFIX(packets_captured));
		if (!verbose)
			fputs(", ", stderr);
		else
			putc('\n', stderr);
		(void)fprintf(stderr, "%u packet%s received by filter", stats.ps_recv,
		    PLURAL_SUFFIX(stats.ps_recv));
		if (!verbose)
			fputs(", ", stderr);
		else
			putc('\n', stderr);
		(void)fprintf(stderr, "%u packet%s dropped by kernel", stats.ps_drop,
		    PLURAL_SUFFIX(stats.ps_drop));
		if (stats.ps_ifdrop != 0) {
			if (!verbose)
				fputs(", ", stderr);
			else
				putc('\n', stderr);
			(void)fprintf(stderr, "%u packet%s dropped by interface\n",
			    stats.ps_ifdrop, PLURAL_SUFFIX(stats.ps_ifdrop));
		} else
			putc('\n', stderr);
		infoprint = 0;
	}

"packets captured" records the packets received and processed by `tcpdump`. There are also "packets received by filter", "packets dropped by kernel" and "packets dropped by interface" statistics. These items are fetched through [pcap_stats](https://www.tcpdump.org/manpages/pcap_stats.3pcap.html) API and depend on the underlying Operating System, so I would not elaborate them here. 