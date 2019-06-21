# Capture packets in immediate mode

"`--immediate-mode`" option is used to make packets are delivered to `tcpdump` immediately once they arrive, rather than being buffered for efficiency. This is the default behavior when printing dissected packets to the standard output and the standard output is a terminal (code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/f4ebd6cda863de6de39e3fdf4b065df06c99650d/tcpdump.c#L1920)):  

	......
	#ifdef HAVE_PCAP_SET_IMMEDIATE_MODE
		/*
		 * If we're printing dissected packets to the standard output
		 * and the standard output is a terminal, use immediate mode,
		 * as the user's probably expecting to see packets pop up
		 * immediately.
		 *
		 * XXX - set the timeout to a lower value, instead?  If so,
		 * what value would be appropriate?
		 */
		if ((WFileName == NULL || print) && isatty(1))
			immediate_mode = 1;
	#endif
	......

[pcap_set_immediate_mode](https://www.tcpdump.org/manpages/pcap_set_immediate_mode.3pcap.html) API is used to set immediate mode.
   

