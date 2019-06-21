# Load SMI MIB module

If `tcpdump` is built with [libsmi](https://www.ibr.cs.tu-bs.de/projects/libsmi/) support, "`-m module`" option can be used to load `MIB` module (code is [here](https://github.com/the-tcpdump-group/tcpdump/blob/f4ebd6cda863de6de39e3fdf4b065df06c99650d/netdissect.c#L122)):  

	int
	nd_load_smi_module(const char *module, char *errbuf, size_t errbuf_size)
	{
	#ifdef USE_LIBSMI
		if (smiLoadModule(module) == 0) {
			nd_snprintf(errbuf, errbuf_size, "could not load MIB module %s",
			    module);
			return (-1);
		}
		nd_smi_module_loaded = 1;
		return (0);
	#else
		nd_snprintf(errbuf, errbuf_size, "MIB module %s not loaded: no libsmi support",
		    module);
		return (-1);
	#endif
	}