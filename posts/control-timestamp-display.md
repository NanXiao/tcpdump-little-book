# Control timestamp display

`Tcpdump` provides abundant options to control timestamp display:  

<table>
  <tr>
    <th>Option</th>
    <th>Meaning</th>
    <th>Example</th> 
  </tr>
  <tr>
    <td>-t</td>
    <td>No time stamp for each line.</td>
    <td>IP 192.168.35.211.ssh > 10.217.133.114.64998: Flags [P.], seq 108:144, ack 1, win 317, length 36</td>
  </tr>
  <tr>
    <td>-tt</td>
    <td>Unix style, i.e., seconds and fractions of second since January 1, 1970, 00:00:00, UTC.</td>
    <td>1561024104.790056 IP 192.168.35.211.ssh > 10.217.133.114.64998: Flags [P.], seq 493732:494000, ack 181, win 317, length 268</td>
  </tr>
  <tr>
    <td>-ttt</td>
    <td>Show time delta between current and previous line on each dump line. The default is microsecond resolution.</td>
    <td>00:00:00.000320 IP 192.168.35.211.ssh > 10.217.133.114.65401: Flags [P.], seq 108:144, ack 1, win 317, length 36</td>
  </tr>
  <tr>
    <td>-tttt</td>
    <td>Print detailed timestamp of every packet.</td>
    <td>2019-06-20 18:16:07.208973 IP 192.168.35.211.ssh > 10.217.133.114.65401: Flags [P.], seq 1528425705:1528425813, ack 3085
343628, win 317, length 108</td>
  </tr>
  <tr>
    <td>-ttttt</td>
    <td>Show time delta between current and first line on each dump line. The default is microsecond resolution.</td>
    <td>00:00:00.000513 IP 192.168.35.211.ssh > 10.217.133.114.65401: Flags [P.], seq 260:296, ack 1, win 317, length 36</td>
  </tr>
</table>