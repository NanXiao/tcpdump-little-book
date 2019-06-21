# Rotate capture files

To rotate capture files, "`-C file_size`" (the unit is `MB`, i.e., `1,000,000` Bytes) option can be used to set the size of rotation file:  
	
	# tcpdump -w enp0s3.pcap -C 1

Otherwise the files can be rotated based on time (seconds) through "`-G seconds`" option:  

	# tcpdump -w enp0s3_%F_%T.pcap -G 3
	tcpdump: listening on enp0s3, link-type EN10MB (Ethernet), capture size 262144 bytes
	^C10 packets captured
	12 packets received by filter
	0 packets dropped by kernel
	# ls -lt *.pcap
	-rw-r--r-- 1 root root 100 Jun  6 09:13 enp0s3_2019-06-06_09:13:28.pcap
	-rw-r--r-- 1 root root 176 Jun  6 09:13 enp0s3_2019-06-06_09:13:24.pcap
	-rw-r--r-- 1 root root 746 Jun  6 09:13 enp0s3_2019-06-06_09:13:21.pcap

For time format, this [page](http://www.cplusplus.com/reference/ctime/strftime/) gives a reference.  

If some operations need to be done with saved files, "`-z postrotate-command`" option can be used. E.g., compress the rotated file:  

	# tcpdump -w enp0s3_%F_%T.pcap -G 3 -z gzip
	tcpdump: listening on enp0s3, link-type EN10MB (Ethernet), capture size 262144 bytes
	^C22 packets captured
	24 packets received by filter
	0 packets dropped by kernel
	# ls *.gz
	enp0s3_2019-06-21_13:37:29.pcap.gz  enp0s3_2019-06-21_13:37:37.pcap.gz  enp0s3_2019-06-21_13:37:43.pcap.gz
	enp0s3_2019-06-21_13:37:34.pcap.gz  enp0s3_2019-06-21_13:37:40.pcap.gz

BTW, there is another "`-W filecount`" option which can be used in conjunction with "`-C`" or "`-G`" option to limit the number of files.