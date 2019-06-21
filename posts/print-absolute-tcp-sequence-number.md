# Print absolute TCP sequence number

"`-S/--absolute-tcp-sequence-numbers`" option tells `tcpdump` print absolute, rather than relative, `TCP` sequence numbers. Compare following outputs from same `TCP` connection:  

(1) Without `-S` option:  

	# tcpdump 
	......
	09:37:43.143719 IP 192.168.35.211.ssh > 10.217.133.114.52037: Flags [P.], seq 108:144, ack 1, win 317, length 36
	09:37:43.143813 IP 192.168.35.211.ssh > 10.217.133.114.52037: Flags [P.], seq 144:260, ack 1, win 317, length 116
	09:37:43.143893 IP 192.168.35.211.ssh > 10.217.133.114.52037: Flags [P.], seq 260:296, ack 1, win 317, length 36
	09:37:43.145503 IP 10.217.133.114.52037 > 192.168.35.211.ssh: Flags [.], ack 108, win 16244, length 0
	......

(2) With `-S` option:  

	# tcpdump -S
	......
	09:38:05.358828 IP 192.168.35.211.ssh > 10.217.133.114.52037: Flags [P.], seq 3717608601:3717608709, ack 3451729629, win 317, length 108
	09:38:05.359036 IP 192.168.35.211.ssh > 10.217.133.114.52037: Flags [P.], seq 3717608709:3717608745, ack 3451729629, win 317, length 36
	09:38:05.359171 IP 192.168.35.211.ssh > 10.217.133.114.52037: Flags [P.], seq 3717608745:3717608861, ack 3451729629, win 317, length 116
	......
