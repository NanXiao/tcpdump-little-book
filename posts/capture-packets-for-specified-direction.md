# Capture packets for specified direction

"`-Q direction/--direction=direction`" option is used to restrict capturing packets for specified direction. The value of `direction` can be `in`, `out` or `inout`, and `tcpdump` calls [pcap_setdirection](https://www.tcpdump.org/manpages/pcap_setdirection.3pcap.html) API to set direction. E.g. capture packets received by interface:  

	# tcpdump -Q in
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on enp0s3, link-type EN10MB (Ethernet), capture size 262144 bytes
	09:13:52.631770 IP 10.217.133.114.51763 > 192.168.35.211.ssh: Flags [.], ack 3460532592, win 16178, length 0
	09:13:52.631787 IP 10.217.133.114.51763 > 192.168.35.211.ssh: Flags [.], ack 153, win 16140, length 0
	09:13:52.640961 IP dns.scei.a-star.edu.sg.domain > 192.168.35.211.39882: 29830 NXDomain 0/0/0 (45)
	09:13:52.642229 IP dns.scei.a-star.edu.sg.domain > 192.168.35.211.40155: 65204 NXDomain 0/1/0 (95)
	......