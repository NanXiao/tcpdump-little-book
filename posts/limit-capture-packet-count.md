# Limit capture packet count

"`-c count`" will limit the number of capture packets. E.g.:  

	# tcpdump -c 1
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on enp0s25, link-type EN10MB (Ethernet), capture size 262144 bytes
	16:45:56.920115 IP archlinux.ssh > 10.218.200.25.59436: Flags [P.], seq 1560371666:1560371854, ack 3724900894, win 501, length 188
	1 packet captured
	4 packets received by filter
	0 packets dropped by kernel

`tcpdump` exited after only capturing `1` packet. This feature is implemented by setting `cnt` argument of `pcap_loop` function:  

	......
	case 'c':
		cnt = atoi(optarg);
		if (cnt <= 0)
			error("invalid packet count %s", optarg);
		break;
	......
	status = pcap_loop(pd, cnt, callback, pcap_userdata);
	......
