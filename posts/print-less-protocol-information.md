# Print less protocol information

"`-q`" option makes `tcpdump` output quickly, i.e., print less protocol information:  

	# tcpdump -q
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on enp0s3, link-type EN10MB (Ethernet), capture size 262144 bytes
	09:20:24.150525 IP 192.168.35.211.ssh > 10.217.133.114.51763: tcp 108
	09:20:24.150678 IP 192.168.35.211.ssh > 10.217.133.114.51763: tcp 36
	09:20:24.150791 IP 192.168.35.211.ssh > 10.217.133.114.51763: tcp 116
	09:20:24.150883 IP 192.168.35.211.ssh > 10.217.133.114.51763: tcp 36
	09:20:24.152401 IP 10.217.133.114.51763 > 192.168.35.211.ssh: tcp 0
	09:20:24.152426 IP 10.217.133.114.51763 > 192.168.35.211.ssh: tcp 0
	09:20:24.351448 IP 10.217.133.114.51763 > 192.168.35.211.ssh: tcp 0
	......