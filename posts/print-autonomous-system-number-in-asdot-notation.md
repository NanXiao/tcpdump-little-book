# Print Autonomous System Number in ASDOT notation

The `ASN` (Autonomous System Number, and you can think it as port number) will be outputted in `ASPLAIN` format by default. However, if `-b` option is specified (code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/0636ecf91357b749370170716e0c4cd494bcea84/tcpdump.c#L1522)):  

		......
		case 'b':
			++ndo->ndo_bflag;
			break;
		......

The `ASN` will be displayed in `ASDOT` notation when the number is bigger than `65535` (code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/0636ecf91357b749370170716e0c4cd494bcea84/print-bgp.c#L522)):  


	static char *
	as_printf(netdissect_options *ndo,
	          char *str, int size, u_int asnum)
	{
		if (!ndo->ndo_bflag || asnum <= 0xFFFF) {
			snprintf(str, size, "%u", asnum);
		} else {
			snprintf(str, size, "%u.%u", asnum >> 16, asnum & 0xFFFF);
		}
		return str;
	}
