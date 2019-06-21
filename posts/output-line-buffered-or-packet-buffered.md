# Output line-buffered or packet-buffered

"`-l`" option is used to specify output line-buffered. On `Unix-like` Operating Systems, `setvbuf()` or `setlinebuf()` will be used (code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/f4ebd6cda863de6de39e3fdf4b065df06c99650d/tcpdump.c#L1647)):  

			......
			case 'l':
	#ifdef _WIN32
				/*
				 * _IOLBF is the same as _IOFBF in Microsoft's C
				 * libraries; the only alternative they offer
				 * is _IONBF.
				 *
				 * XXX - this should really be checking for MSVC++,
				 * not _WIN32, if, for example, MinGW has its own
				 * C library that is more UNIX-compatible.
				 */
				setvbuf(stdout, NULL, _IONBF, 0);
	#else /* _WIN32 */
	#ifdef HAVE_SETLINEBUF
				setlinebuf(stdout);
	#else
				setvbuf(stdout, NULL, _IOLBF, 0);
	#endif
	#endif /* _WIN32 */
				break;
			......

`tcpdump` can also output packet-buffered through "`-U/--packet-buffered`" option and call [pcap_dump_flush](https://www.tcpdump.org/manpages/pcap_dump_flush.3pcap.html) API.