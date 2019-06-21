# Show help & version info

Like other commands in `Unix-like` Operating Systems, "`-h/--help`" prints help information:  

	# tcpdump -h
	tcpdump version 4.9.2
	libpcap version 1.9.0-PRE-GIT (with TPACKET_V3)
	LibreSSL 2.8.3
	Usage: tcpdump [-aAbdDefhHIJKlLnNOpqStuUvxX#] [ -B size ] [ -c count ]
	                [ -C file_size ] [ -E algo:secret ] [ -F file ] [ -G seconds ]
	                [ -i interface ] [ -j tstamptype ] [ -M secret ] [ --number ]
	                [ -Q in|out|inout ]
	                [ -r file ] [ -s snaplen ] [ --time-stamp-precision precision ]
	                [ --immediate-mode ] [ -T type ] [ --version ] [ -V file ]
	                [ -w file ] [ -W filecount ] [ -y datalinktype ] [ -z postrotate-command ]
	                [ -Z user ] [ expression ]

While `--version` shows `tcpdump`'s version:  

	# tcpdump --version
	tcpdump version 4.9.2
	libpcap version 1.9.0-PRE-GIT (with TPACKET_V3)
	LibreSSL 2.8.3

