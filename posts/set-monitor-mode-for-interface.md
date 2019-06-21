# Set monitor mode for interface

"`-I/--monitor-mode`" option is used to put network interface in "monitor mode" through [pcap_set_rfmon](https://www.tcpdump.org/manpages/pcap_set_rfmon.3pcap.html) API (code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/a64580025249644dbae9fa03efc14e811fcac49b/tcpdump.c#L1305)):  

	......
	if (Iflag) {
		status = pcap_set_rfmon(pc, 1);
		if (status != 0)
			error("%s: Can't set monitor mode: %s",
			    device, pcap_statustostr(status));
	}
	......

Definitely, the interface should support "monitor mode" first, otherwise, following error message will be outputted:  

	# tcpdump -I
	tcpdump: enp0s3: That device doesn't support monitor mode
