# Don't print domain name qualification of host names  

"`-N`" option tells `tcpdump` not print domain name qualification of host names. Compare following outputs:

(1) Without "`-N`":  

	# tcpdump port 80
	......
	09:28:16.590166 IP 192.168.35.211.36662 > sin10s07-in-f100.1e100.net.http: Flags [S], seq 3705499091, win 29200, options [mss 1460,sackOK,TS val 3283951004 ecr 0,nop,wscale 7], length 0
	09:28:16.593198 IP sin10s07-in-f100.1e100.net.http > 192.168.35.211.36662: Flags [S.], seq 3497055131, ack 3705499092, win 60192, options [mss 1380,sackOK,TS val 340557822 ecr 3283951004,nop,wscale 8], length 0
	09:28:16.593222 IP 192.168.35.211.36662 > sin10s07-in-f100.1e100.net.http: Flags [.], ack 1, win 229, options [nop,nop,TS val 3283951007 ecr 340557822], length 0
	09:28:16.593652 IP 192.168.35.211.36662 > sin10s07-in-f100.1e100.net.http: Flags [P.], seq 1:142, ack 1, win 229, options [nop,nop,TS val 3283951007 ecr 340557822], length 141: HTTP: GET / HTTP/1.1
	......

(2) With "`-N`" ("`1e100.net`" is not outputted):  

	# tcpdump -N port 80
	......
	09:16:10.543488 IP 192.168.35.211.36610 > sin10s07-in-f4.http: Flags [S], seq 3887934852, win 29200, options [mss 1460,sackOK,TS val 3283224957 ecr 0,nop,wscale 7], length 0
	09:16:10.546542 IP sin10s07-in-f4.http > 192.168.35.211.36610: Flags [S.], seq 1285438159, ack 3887934853, win 60192, options [mss 1380,sackOK,TS val 2475082608 ecr 3283224957,nop,wscale 8], length 0
	09:16:10.546577 IP 192.168.35.211.36610 > sin10s07-in-f4.http: Flags [.], ack 1, win 229, options [nop,nop,TS val 3283224960 ecr 2475082608], length 0
	09:16:10.547079 IP 192.168.35.211.36610 > sin10s07-in-f4.http: Flags [P.], seq 1:142, ack 1, win 229, options [nop,nop,TS val 3283224961 ecr 2475082608], length 141: HTTP: GET / HTTP/1.1
	......
