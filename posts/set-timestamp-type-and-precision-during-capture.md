# Set timestamp type and precision during capture

"`-J/--list-time-stamp-types`" option is used to list timestamp types that interface supports:  

	$ tcpdump -J
	Time stamp types for enp0s3 (use option -j to set):
	  host (Host)
	  adapter_unsynced (Adapter, not synced with system time)

As prompted, "`-j tstamp_type/--time-stamp-type=tstamp_type`" option can be used to set timestamp type. Now `5` types are supported: `host`, `host_lowprec`, `host_hiprec`, `adapter` and `adapter_unsynced` (please refer [pcap-tstamp](https://www.tcpdump.org/manpages/pcap-tstamp.7.html)).  

The timestamp precision can be set in microsecond resolution ("`--time-stamp-precision=macro/--macro`") or nanosecond resolution ("`--time-stamp-precision=nano/--nano`"):  

	# tcpdump --time-stamp-precision=nano
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on enp0s3, link-type EN10MB (Ethernet), snapshot length 262144 bytes
	17:53:08.669795918 IP 192.168.35.211.ssh > 10.217.133.115.56843: Flags [P.], seq 2946671030:2946671138, ack 2526798027, win 317, length 108
	17:53:08.670069187 IP 192.168.35.211.ssh > 10.217.133.115.56843: Flags [P.], seq 108:144, ack 1, win 317, length 36
	17:53:08.670174142 IP 192.168.35.211.ssh > 10.217.133.115.56843: Flags [P.], seq 144:204, ack 1, win 317, length 60
	17:53:08.670267764 IP 192.168.35.211.ssh > 10.217.133.115.56843: Flags [P.], seq 204:272, ack 1, win 317, length 68
	17:53:08.670356638 IP 192.168.35.211.ssh > 10.217.133.115.56843: Flags [P.], seq 272:340, ack 1, win 317, length 68
	17:53:08.670435999 IP 192.168.35.211.ssh > 10.217.133.115.56843: Flags [P.], seq 340:376, ack 1, win 317, length 36
	......
	
The actual precision of timestamp depends on the Operating System and hardware.