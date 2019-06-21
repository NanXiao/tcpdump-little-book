# Set capture buffer size

"`-B buffer_size/--buffer-size=buffer_size`" option can be used to change capture buffer size (code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/cfc663988081e9ed293d46de626b1f98e91b2de5/tcpdump.c#L1526)):  

	......
	#if defined(HAVE_PCAP_CREATE) || defined(_WIN32)
			case 'B':
				Bflag = atoi(optarg)*1024;
				if (Bflag <= 0)
					error("invalid packet buffer size %s", optarg);
				break;
	#endif /* defined(HAVE_PCAP_CREATE) || defined(_WIN32) */
	......
The unit is `KiB`. `pcap_set_buffer_size()` is called  to set buffer size (code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/cfc663988081e9ed293d46de626b1f98e91b2de5/tcpdump.c#L1315)):  

	......
	if (Bflag != 0) {
		status = pcap_set_buffer_size(pc, Bflag);
		if (status != 0)
			error("%s: Can't set buffer size: %s",
			    device, pcap_statustostr(status));
	}
	......

On Windows, a special processing is needed (code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/cfc663988081e9ed293d46de626b1f98e91b2de5/tcpdump.c#L2101)):  

	......
	#if !defined(HAVE_PCAP_CREATE) && defined(_WIN32)
			if(Bflag != 0)
				if(pcap_setbuff(pd, Bflag)==-1){
					error("%s", pcap_geterr(pd));
				}
	#endif /* !defined(HAVE_PCAP_CREATE) && defined(_WIN32) */
	......