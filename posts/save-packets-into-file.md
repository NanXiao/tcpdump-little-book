# Save packets into file

"`-w file`" option is used to save capture packets into a file instead of printing them in standard output:  

	# tcpdump -w enp0s3.pcap
	tcpdump: listening on enp0s3, link-type EN10MB (Ethernet), capture size 262144 bytes
	^C7 packets captured
	9 packets received by filter
	0 packets dropped by kernel

If printing packet is also needed when saving to file, "`--print`" optin can help:  

	# tcpdump --print -w enp0s3.pcap
	tcpdump: listening on enp0s3, link-type EN10MB (Ethernet), snapshot length 262144 bytes
	09:27:48.456071 IP 192.168.35.211.ssh > 10.217.133.114.63884: Flags [P.], seq 485718701:485718745, ack 2592535797, win 317, length 44
	09:27:48.456311 IP 192.168.35.211.ssh > 10.217.133.114.63884: Flags [P.], seq 44:104, ack 1, win 317, length 60
	......
		
The file can be read through "`-r`" option:  

	$ tcpdump -r enp0s3.pcap
	reading from file enp0s3.pcap, link-type EN10MB (Ethernet)
	09:27:48.456071 IP 192.168.35.211.ssh > 10.217.133.114.63884: Flags [P.], seq 485718701:485718745, ack 2592535797, win 317, length 44
	09:27:48.456311 IP 192.168.35.211.ssh > 10.217.133.114.63884: Flags [P.], seq 44:104, ack 1, win 317, length 60
	......


If there are multiple files to read, create a new file to store paths for these files (one per line), then use "`-V`" option to read them:  

	# tcpdump -w enp0s3_0.pcap
	......
	# tcpdump -w enp0s3_1.pcap
	......
	# cat pcap_file.txt
	enp0s3_0.pcap
	enp0s3_1.pcap
	# tcpdump -V pcap_file.txt
	reading from file enp0s3_0.pcap, link-type EN10MB (Ethernet)
	11:33:35.806380 IP 192.168.35.211.ssh > 10.217.133.114.62443: Flags [P.], seq 1938680568:1938680612, ack 2008981114, win 317, length 44
	11:33:35.806574 IP 192.168.35.211.ssh > 10.217.133.114.62443: Flags [P.], seq 44:160, ack 1, win 317, length 116
	11:33:35.806710 IP 192.168.35.211.ssh > 10.217.133.114.62443: Flags [P.], seq 160:196, ack 1, win 317, length 36
	11:33:35.807941 IP 10.217.133.114.62443 > 192.168.35.211.ssh: Flags [.], ack 44, win 16316, length 0
	11:33:35.808168 IP 10.217.133.114.62443 > 192.168.35.211.ssh: Flags [.], ack 196, win 16278, length 0
	11:33:35.890102 STP 802.1d, Config, Flags [none], bridge-id 8000.00:09:e8:e0:1e:97.8083, length 43
	11:33:36.629550 IP 192.168.35.145.45715 > 239.255.255.250.ssdp: UDP, length 166
	11:33:37.631041 IP 192.168.35.145.45715 > 239.255.255.250.ssdp: UDP, length 166
	reading from file enp0s3_1.pcap, link-type EN10MB (Ethernet)
	11:33:41.703389 IP 192.168.35.211.ssh > 10.217.133.114.62443: Flags [P.], seq 1040:1084, ack 497, win 317, length 44
	11:33:41.703663 IP 192.168.35.211.ssh > 10.217.133.114.62443: Flags [P.], seq 1084:1200, ack 497, win 317, length 116
	11:33:41.703802 IP 192.168.35.211.ssh > 10.217.133.114.62443: Flags [P.], seq 1200:1236, ack 497, win 317, length 36
	11:33:41.705086 IP 10.217.133.114.62443 > 192.168.35.211.ssh: Flags [.], ack 1084, win 16425, length 0
	......
