# Print undecoded NFS handles

"`-u`" option is used to print undecoded `NFS` handles, and the code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/33152db7441fcd8fcc39bf129b5d3ebef97726ec/print-nfs.c#L893):  

	......
	if (ndo->ndo_uflag) {
		u_int i;
		char const *sep = "";

		ND_PRINT(" fh[");
		for (i=0; i<len; i++) {
			/*
			 * This displays 4 bytes in big-endian byte
			 * order.  That's as good a choice as little-
			 * endian, as there's no guarantee that the
			 * server is big-endian or little-endian or
			 * that the file handle contains 4-byte
			 * integral fields, and is better than "the
			 * byte order of the host running tcpdump", as
			 * the latter means that different hosts
			 * running tcpdump may show the same file
			 * handle in different ways.
			 */
			ND_PRINT("%s%x", sep, GET_BE_U_4(dp + i));
			sep = ":";
		}
		ND_PRINT("]");
		return;
	}
	......