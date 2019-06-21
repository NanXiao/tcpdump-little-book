# Parse and print packets

`-A` option can be used to print packets in `ASCII` format. E.g., show contents of web pages:  

	# tcpdump -A port 80
	......
	15:37:32.623887 IP sin10s02-in-f14.1e100.net.http > archlinux.40742: Flags [.], ack 138, win 240, options [nop,nop,TS val 1699492976 ecr 4020616092], length 0
	E..4.%..x......N
	....P.&..6.b*;............
	eL4p....
	15:37:32.628640 IP sin10s02-in-f14.1e100.net.http > archlinux.40742: Flags [P.], seq 1:529, ack 138, win 240, options [nop,nop,TS val 1699492981 ecr 4020616092], length 528: HTTP: HTTP/1.1 301 Moved Permanently
	E..D.'..x......N
	....P.&..6.b*;.....h......
	eL4u....HTTP/1.1 301 Moved Permanently
	Location: http://www.google.com/
	Content-Type: text/html; charset=UTF-8
	Date: Fri, 03 May 2019 07:37:32 GMT
	Expires: Sun, 02 Jun 2019 07:37:32 GMT
	Cache-Control: public, max-age=2592000
	Server: gws
	Content-Length: 219
	X-XSS-Protection: 0
	X-Frame-Options: SAMEORIGIN
	
	<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
	<TITLE>301 Moved</TITLE></HEAD><BODY>
	<H1>301 Moved</H1>
	The document has moved
	<A HREF="http://www.google.com/">here</A>.
	</BODY></HTML>
	......

There is also a group of "`-x/-xx/-X/-XX`" options to parse and print packets:  

<table>
  <tr>
    <th>Option</th>
    <th>Meaning</th>
    <th>Example</th> 
  </tr>
  <tr>
    <td>-x</td>
    <td>Print the data of each packet (minus its link level header) in hex.</td>
    <td>12:58:03.592155 IP 192.168.35.211.ssh > 10.217.133.114.54092: Flags [P.], seq 260:296, ack 1, win 317, length 36</br>
        0x0000:  4548 004c 6b56 4000 4006 5a47 c0a8 23d3</br>
        0x0010:  0ad9 8572 0016 d34c 4251 850d 7a7c d8b4</br>
        ......</td>
   </tr>
   <tr>
    <td>-xx</td>
    <td>Print the data of each packet, including its link level header, in hex.</td>
    <td>13:16:30.839337 IP 192.168.35.211.ssh > 10.217.133.114.54092: Flags [P.], seq 260:296, ack 1, win 317, length 36</br>
        0x0000:  001e bdde 5f00 0800 2770 9e7a 0800 4548</br>
        0x0010:  004c 6ba0 4000 4006 59fd c0a8 23d3 0ad9</br>
        ......</td>
  </tr>
  <tr>
    <td>-X</td>
    <td>Print the data of each packet (minus its link level header) in hex and ASCII.</td>
    <td>13:19:13.539666 IP 192.168.35.211.ssh > 10.217.133.114.54092: Flags [P.], seq 1114673977:1114674085, ack 2055006128, win 317, length 108</br>
        0x0000:  4548 0094 744c 4000 4006 5109 c0a8 23d3  EH..tL@.@.Q...#.</br>
        0x0010:  0ad9 8572 0016 d34c 4270 9339 7a7c e7b0  ...r...LBp.9z|..</br>
        ......</td>
   </tr>
   <tr>
    <td>-XX</td>
    <td>Print the data of each packet, including its link level header, in hex and ASCII.</td>
    <td>13:22:22.536935 IP 192.168.35.211.ssh > 10.217.133.114.54092: Flags [P.], seq 1114682321:1114682429, ack 2055007124, win 317, length 108</br>
        0x0000:  001e bdde 5f00 0800 2770 9e7a 0800 4548  ...._...'p.z..EH</br>
        0x0010:  0094 7480 4000 4006 50d5 c0a8 23d3 0ad9  ..t.@.@.P...#...</br>
	......</td>
  </tr>
</table>