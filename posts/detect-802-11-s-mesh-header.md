# Detect 802.11s mesh header

"`-H`" option is used to detect `802.11s` mesh headers. The related code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/50f375f9f1444e744d6e4b117940f0a7c9dd8c23/print-802_11.c#L2049):  

	......
	if (ndo->ndo_Hflag && FC_TYPE(fc) == T_DATA &&
	    DATA_FRAME_IS_QOS(FC_SUBTYPE(fc))) {
		if(!ND_TTEST_1(p + hdrlen)) {
			nd_print_trunc(ndo);
			return hdrlen;
		}
		meshdrlen = extract_mesh_header_length(ndo, p + hdrlen);
		hdrlen += meshdrlen;
	} else
		meshdrlen = 0;
	......