# Print verbose output

There are `3` options which are used to display verbose output: `-v`, `-vv` and `-vvv` (The more `v`, the more detailed information). E.g.:  

	# tcpdump -v
	......
	11:11:35.272933 IP (tos 0x48, ttl 64, id 31847, offset 0, flags [DF], proto TCP (6), length 84)
    192.168.35.211.ssh > 10.217.133.114.62443: Flags [P.], cksum 0x750d (incorrect -> 0x0700), seq 1935872656:1935872700, ack 2008969174, win 317, length 44
	......