# Print link level header

"`-e`" option can be used to print link level header, e.g., `MAC` address. Compare the output without & with "`-e`":  

	# tcpdump
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on enp0s3, link-type EN10MB (Ethernet), capture size 262144 bytes
	08:49:05.566481 IP 192.168.35.211.ssh > 10.217.133.165.62575: Flags [P.], seq 3495460430:3495460538, ack 1684770413, win 317, length 108
	08:49:05.566644 IP 192.168.35.211.ssh > 10.217.133.165.62575: Flags [P.], seq 108:144, ack 1, win 317, length 36
	08:49:05.566759 IP 192.168.35.211.ssh > 10.217.133.165.62575: Flags [P.], seq 144:260, ack 1, win 317, length 116
	08:49:05.566851 IP 192.168.35.211.ssh > 10.217.133.165.62575: Flags [P.], seq 260:296, ack 1, win 317, length 36
	......

	# tcpdump -e
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on enp0s3, link-type EN10MB (Ethernet), capture size 262144 bytes
	08:52:14.998750 08:00:27:70:9e:7a (oui Unknown) > 00:1e:bd:de:67:00 (oui Unknown), ethertype IPv4 (0x0800), length 162: 192.168.35.211.ssh > 10.217.133.165.62575: Flags [P.], seq 3496206666:3496206774, ack 1684770961, win 317, length 108
	08:52:14.998897 08:00:27:70:9e:7a (oui Unknown) > 00:1e:bd:de:67:00 (oui Unknown), ethertype IPv4 (0x0800), length 90: 192.168.35.211.ssh > 10.217.133.165.62575: Flags [P.], seq 108:144, ack 1, win 317, length 36
	08:52:14.999088 08:00:27:70:9e:7a (oui Unknown) > 00:1e:bd:de:67:00 (oui Unknown), ethertype IPv4 (0x0800), length 170: 192.168.35.211.ssh > 10.217.133.165.62575: Flags [P.], seq 144:260, ack 1, win 317, length 116
