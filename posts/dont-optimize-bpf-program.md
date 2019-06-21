# Don't optimize BPF program

"`-O/--no-optimize`" tells `tcpdump` not optimize generated `BPF` program, and this options just sets `optimize`'s value to `0` in [pcap_compile](https://www.tcpdump.org/manpages/pcap_compile.3pcap.html) function.