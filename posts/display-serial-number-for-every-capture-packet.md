# Display serial number for every capture packet

"`-#/--number`" option is used to display serial number for every capture packet:  

	# tcpdump -# > log.txt
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on enp0s3, link-type EN10MB (Ethernet), capture size 262144 bytes
	1  09:45:29.712740 IP 192.168.35.211.ssh > 10.217.133.114.51554: Flags [P.], seq 2582118158:2582118266, ack 3041963369, win 317, length 108
    2  09:45:29.712927 IP 192.168.35.211.ssh > 10.217.133.114.51554: Flags [P.], seq 108:144, ack 1, win 317, length 36
    3  09:45:29.713078 IP 192.168.35.211.ssh > 10.217.133.114.51554: Flags [P.], seq 144:260, ack 1, win 317, length 116
    4  09:45:29.713275 IP 192.168.35.211.ssh > 10.217.133.114.51554: Flags [P.], seq 260:296, ack 1, win 317, length 36
	......