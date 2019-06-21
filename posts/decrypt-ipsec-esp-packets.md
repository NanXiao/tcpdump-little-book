# Decrypt IPSec ESP packets  

"`-E spi@ipaddr algo:secret ...`" can be used to decrypt `IPSec ESP` packets. Because this option involves secret key, it should only be used in debugging purpose. `Tcpdump` needs to be compiled with cryptography enabled (there is an [example](https://lists.freebsd.org/pipermail/freebsd-questions/2014-March/256538.html) about how to use this option).