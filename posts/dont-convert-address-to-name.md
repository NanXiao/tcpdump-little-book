# Don't convert address to name

"`-n`" option tells `tcpdump` not convert address to name. Compare following outputs:  

(1) Without "`-n`":    

	# tcpdump port 80
	......
	17:55:23.767010 IP 192.168.35.211.42314 > sa-in-f106.1e100.net.http: Flags [S], seq 754374479, win 29200, options [mss 1460,sackOK,TS val 3390348087 ecr 0,nop,wscale 7], length 0
	17:55:23.773385 IP sa-in-f106.1e100.net.http > 192.168.35.211.42314: Flags [S.], seq 3627421307, ack 754374480, win 62392, options [mss 1430,sackOK,TS val 1694624530 ecr 3390348087,nop,wscale 8], length 0
	17:55:23.773420 IP 192.168.35.211.42314 > sa-in-f106.1e100.net.http: Flags [.], ack 1, win 229, options [nop,nop,TS val 3390348093 ecr 1694624530], length 0
	17:55:23.773921 IP 192.168.35.211.42314 > sa-in-f106.1e100.net.http: Flags [P.], seq 1:142, ack 1, win 229, options [nop,nop,TS val 3390348094 ecr 1694624530], length 141: HTTP: GET / HTTP/1.1
	......

(2) With `-n` (No name resolution, only `IP` addresses are printed):  

	# tcpdump port 80
	......
	17:54:53.516004 IP 192.168.35.211.42310 > 74.125.200.106.80: Flags [S], seq 3573100071, win 29200, options [mss 1460,sackOK,TS val 3390317836 ecr 0,nop,wscale 7], length 0
	17:54:53.519718 IP 74.125.200.106.80 > 192.168.35.211.42310: Flags [S.], seq 1387207616, ack 3573100072, win 62392, options [mss 1430,sackOK,TS val 2574277547 ecr 3390317836,nop,wscale 8], length 0
	17:54:53.519746 IP 192.168.35.211.42310 > 74.125.200.106.80: Flags [.], ack 1, win 229, options [nop,nop,TS val 3390317839 ecr 2574277547], length 0
	17:54:53.520500 IP 192.168.35.211.42310 > 74.125.200.106.80: Flags [P.], seq 1:142, ack 1, win 229, options [nop,nop,TS val 3390317840 ecr 2574277547], length 141: HTTP: GET / HTTP/1.1
	......
