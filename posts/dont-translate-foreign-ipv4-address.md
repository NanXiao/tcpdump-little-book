# Don't translate foreign IPv4 address

"`-f`" option tells `tcpdump` not translate foreign `IPv4` address. Use `tcpdump` to monitor packets from port `80`:  

	# tcpdump port 80
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on enp0s3, link-type EN10MB (Ethernet), capture size 262144 bytes

Open another terminal and run following command:  

	# wget google.com
	--2019-06-04 08:37:09--  http://google.com/
	Resolving google.com... 74.125.130.102, 74.125.130.113, 74.125.130.139, ...
	Connecting to google.com|74.125.130.102|:80... connected.
	HTTP request sent, awaiting response... 301 Moved Permanently
	......

In the first terminal, `tcpdump` will print following output:  

	......
	08:37:09.815811 IP 192.168.35.211.41580 > sb-in-f102.1e100.net.http: Flags [S], seq 1939117813, win 29200, options [mss 1460,sackOK,TS val 229353835 ecr 0,nop,wscale 7], length 0
	08:37:09.819276 IP sb-in-f102.1e100.net.http > 192.168.35.211.41580: Flags [S.], seq 1065852934, ack 1939117814, win 60192, options [mss 1380,sackOK,TS val 2316592675 ecr 229353835,nop,wscale 8], length 0
	08:37:09.819307 IP 192.168.35.211.41580 > sb-in-f102.1e100.net.http: Flags [.], ack 1, win 229, options [nop,nop,TS val 229353838 ecr 2316592675], length 0
	08:37:09.819738 IP 192.168.35.211.41580 > sb-in-f102.1e100.net.http: Flags [P.], seq 1:138, ack 1, win 229, options [nop,nop,TS val 229353839 ecr 2316592675], length 137: HTTP: GET / HTTP/1.1
	......

If using "`-f`" option ("`tcpdump -f port 80`"), `IP` addresses will be printed instead:  

	......
	08:37:49.861210 IP 192.168.35.211.48270 > 74.125.130.139.http: Flags [S], seq 177134859, win 29200, options [mss 1460,sackOK,TS val 1024480880 ecr 0,nop,wscale 7], length 0
	08:37:49.865430 IP 74.125.130.139.http > 192.168.35.211.48270: Flags [S.], seq 711300604, ack 177134860, win 60192, options [mss 1380,sackOK,TS val 3503207327 ecr 1024480880,nop,wscale 8], length 0
	08:37:49.865459 IP 192.168.35.211.48270 > 74.125.130.139.http: Flags [.], ack 1, win 229, options [nop,nop,TS val 1024480884 ecr 3503207327], length 0
	......

