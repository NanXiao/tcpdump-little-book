# Specify network interfaces

"`-D/--list-interfaces`" option is used to show available network interfaces:  

	# tcpdump -D
	1.enp0s3 [Up, Running]
	2.lo [Up, Running, Loopback]
	3.any (Pseudo-device that captures on all interfaces) [Up, Running]
	4.nflog (Linux netfilter log (NFLOG) interface) [none]
	5.nfqueue (Linux netfilter queue (NFQUEUE) interface) [none]

"`-i/--interface`" option is used to specify the listening interface. If not specified, interface with the lowest index excluding `loopback` is picked (i.e., `enp0s3`). If the traffic through all interfaces need to captured, "`any`" should be the name of interface:  

	# tcpdump -i any
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on any, link-type LINUX_SLL (Linux cooked), capture size 262144 bytes
	......
	17:08:43.333868 IP 192.168.35.211.ssh > 10.217.133.165.49880: Flags [P.], seq 54874791:54874899, ack 1667749708, win 317
	, length 108
	17:08:43.333962 IP 192.168.35.211.ssh > 10.217.133.165.49880: Flags [P.], seq 108:144, ack 1, win 317, length 36
	17:08:43.334044 IP 192.168.35.211.ssh > 10.217.133.165.49880: Flags [P.], seq 144:260, ack 1, win 317, length 116
	17:08:43.334125 IP 192.168.35.211.ssh > 10.217.133.165.49880: Flags [P.], seq 260:296, ack 1, win 317, length 36
	
Or use index instead:  

	# tcpdump -i 3