# Layer 4 - Transport Layer: TCP Open vs Closed Port Behavior

## Objective
The objective of this experiment was to observe Layer 4 transport behavior by comparing how TCP responds when port 80 is open versus when port 80 is closed.

This experiment focused on TCP ports, the three-way handshake, connection termination, and reset behavior.

## Lab Setup
- Kali Linux VM: traffic generator / pentester machine
- Ubuntu VM: target and packet capture machine
- VirtualBox: virtualization platform
- Ubuntu IP address: 192.168.1.22
- Kali IP address: 192.168.1.71
- Ubuntu interface: enp0s3
- Service tested: Apache2 web server
- Port tested: TCP port 80
- Tools used: Apache2, Nmap, curl, tcpdump, Wireshark, systemctl, ss

## Method
I started Apache2 on the Ubuntu VM so that TCP port 80 was open. Then I captured TCP traffic using tcpdump while scanning the Ubuntu VM from Kali with Nmap. After confirming the open-port behavior, I stopped Apache2 and scanned TCP port 80 again to observe closed-port behavior.

The packet capture was opened in Wireshark and filtered to isolate traffic between Kali and Ubuntu.

Capture command used on Ubuntu:

```bash
sudo tcpdump -i enp0s3 -n -w layer4_tcp_open_closed.pcap tcp

Nmap command used from Kali: nmap -p 80 --reason

Curl command used from Kali: curl http://

Apache start command:sudo systemctl start apache2

Apache stop command:sudo systemctl stop apache2

Result

When Apache2 was running, Nmap showed TCP port 80 as open. Wireshark showed the TCP three-way handshake between Kali and Ubuntu.

Observed open-port handshake:

Kali   → Ubuntu: SYN
Ubuntu → Kali:   SYN, ACK
Kali   → Ubuntu: ACK

In the packet capture, Kali 192.168.1.71 sent a TCP SYN packet to Ubuntu 192.168.1.22 on destination port 80. Ubuntu responded with a SYN-ACK, confirming that TCP port 80 was open and accepting connections.

The capture also showed HTTP traffic after the TCP connection was established, including:

GET / HTTP/1.1
HTTP/1.1 200 OK

This confirmed that Apache2 was serving web content over TCP port 80.

When Apache2 was stopped, TCP port 80 no longer accepted connections. A closed port responds differently than an open port. Instead of completing the TCP handshake, the target responds with a reset packet.

Observed closed-port behavior:

Kali   → Ubuntu: SYN
Ubuntu → Kali:   RST, ACK
Packet Analysis

TCP uses ports to identify services. In this experiment, port 80 represented the HTTP service provided by Apache2.

When a service is listening on a TCP port, the server responds to a connection request with SYN-ACK. This allows the TCP three-way handshake to complete.

When no service is listening on the port, the host may respond with RST or RST-ACK. This tells the client that the host is reachable, but the requested port is closed.

This behavior explains how tools like Nmap identify open and closed TCP ports.

Security Relevance

Layer 4 is important in cybersecurity because exposed TCP and UDP ports reveal what services are available on a system. Attackers use port scanning to discover services, while defenders use packet captures, firewall logs, and IDS tools to detect scanning and unauthorized access attempts.

Understanding TCP handshakes and reset behavior helps analysts identify:

Open services
Closed ports
Port scans
Connection attempts
Service exposure
Suspicious repeated SYN traffic
VM Networking Observation

The original packet capture contained additional port 80 traffic involving a public IP address. This happened because the Wireshark filter tcp.port == 80 shows any packet where either the source or destination port is 80.

To isolate the lab traffic, I used a more specific filter that included both the Kali IP address and Ubuntu IP address:

ip.addr == 192.168.1.22 && ip.addr == 192.168.1.71 && tcp.port == 80

This narrowed the view to only the Kali-to-Ubuntu lab traffic.

Evidence
PCAP file: layer4_tcp_open_closed.pcap
Screenshot: Apache2 running with port 80 open
Screenshot: Nmap showing port 80 open
Screenshot: Wireshark filtered traffic between Kali and Ubuntu
Screenshot: TCP three-way handshake
Screenshot: HTTP GET request and HTTP 200 OK response
Screenshot: Apache2 stopped with port 80 closed
Screenshot: Nmap showing port 80 closed
Screenshot: TCP reset packet for closed port
Conclusion

This experiment demonstrated how Layer 4 TCP behavior changes depending on whether a port is open or closed. When Apache2 was running, Ubuntu completed the TCP three-way handshake on port 80. When Apache2 was stopped, Ubuntu no longer accepted the connection and responded with reset behavior.

This lab showed how Nmap and Wireshark can be used together to analyze transport-layer service availability
