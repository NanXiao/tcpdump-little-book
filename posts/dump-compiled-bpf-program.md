# Dump compiled BPF program

The `expression` part (please refer [The format of tcpdump command](the-format-of-tcpdump-command.md)) will be compiled into [BPF](https://en.wikipedia.org/wiki/Berkeley_Packet_Filter) program before processing (code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/master/tcpdump.c#L2152)):  

	......
	if (pcap_compile(pd, &fcode, cmdbuf, Oflag, netmask) < 0)
		error("%s", pcap_geterr(pd));
	if (dflag) {
		bpf_dump(&fcode, dflag);
		pcap_close(pd);
		free(cmdbuf);
		pcap_freecode(&fcode);
		exit_tcpdump(S_SUCCESS);
	}
	......

"`-d`" option can be used to control how to display compiled `BPF` program.

a) In human readable format (like assembly code):  

	# tcpdump -d port 80
	(000) ldh      [12]
	(001) jeq      #0x86dd          jt 2    jf 10
	(002) ldb      [20]
	(003) jeq      #0x84            jt 6    jf 4
	(004) jeq      #0x6             jt 6    jf 5
	(005) jeq      #0x11            jt 6    jf 23
	(006) ldh      [54]
	(007) jeq      #0x50            jt 22   jf 8
	(008) ldh      [56]
	(009) jeq      #0x50            jt 22   jf 23
	(010) jeq      #0x800           jt 11   jf 23
	(011) ldb      [23]
	(012) jeq      #0x84            jt 15   jf 13
	(013) jeq      #0x6             jt 15   jf 14
	(014) jeq      #0x11            jt 15   jf 23
	(015) ldh      [20]
	(016) jset     #0x1fff          jt 23   jf 17
	(017) ldxb     4*([14]&0xf)
	(018) ldh      [x + 14]
	(019) jeq      #0x50            jt 22   jf 20
	(020) ldh      [x + 16]
	(021) jeq      #0x50            jt 22   jf 23
	(022) ret      #262144
	(023) ret      #0

b) In `C` program fragment format:  

	# tcpdump -dd port 80
	{ 0x28, 0, 0, 0x0000000c },
	{ 0x15, 0, 8, 0x000086dd },
	{ 0x30, 0, 0, 0x00000014 },
	{ 0x15, 2, 0, 0x00000084 },
	{ 0x15, 1, 0, 0x00000006 },
	{ 0x15, 0, 17, 0x00000011 },
	{ 0x28, 0, 0, 0x00000036 },
	{ 0x15, 14, 0, 0x00000050 },
	{ 0x28, 0, 0, 0x00000038 },
	{ 0x15, 12, 13, 0x00000050 },
	{ 0x15, 0, 12, 0x00000800 },
	{ 0x30, 0, 0, 0x00000017 },
	{ 0x15, 2, 0, 0x00000084 },
	{ 0x15, 1, 0, 0x00000006 },
	{ 0x15, 0, 8, 0x00000011 },
	{ 0x28, 0, 0, 0x00000014 },
	{ 0x45, 6, 0, 0x00001fff },
	{ 0xb1, 0, 0, 0x0000000e },
	{ 0x48, 0, 0, 0x0000000e },
	{ 0x15, 2, 0, 0x00000050 },
	{ 0x48, 0, 0, 0x00000010 },
	{ 0x15, 0, 1, 0x00000050 },
	{ 0x6, 0, 0, 0x00040000 },
	{ 0x6, 0, 0, 0x00000000 },

c) In raw number format:  

	# tcpdump -ddd port 80
	24
	40 0 0 12
	21 0 8 34525
	48 0 0 20
	21 2 0 132
	21 1 0 6
	21 0 17 17
	40 0 0 54
	21 14 0 80
	40 0 0 56
	21 12 13 80
	21 0 12 2048
	48 0 0 23
	21 2 0 132
	21 1 0 6
	21 0 8 17
	40 0 0 20
	69 6 0 8191
	177 0 0 14
	72 0 0 14
	21 2 0 80
	72 0 0 16
	21 0 1 80
	6 0 0 262144
	6 0 0 0

	

