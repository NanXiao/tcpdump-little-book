# List and set data link type

"`-L/--list-data-link-types`" option is used to list available data link types:  

	# tcpdump -L
	Data link types for enp0s3 (use option -y to set):
	  EN10MB (Ethernet)
	  DOCSIS (DOCSIS) (printing not supported)

Beware that the output may be different if the interface works in different modes (e.g., monitor mode or not).  

As prompted, "`-y datalinktype/--linktype=datalinktype`" option can be used to set data link type to capture packets:  

	# tcpdump -y EN10MB