# Layer 3 - Network Layer: IP, ICMP, TTL, and Routing

## Objective
The objective of this experiment was to observe Layer 3 network behavior by capturing ICMP traffic between a Kali Linux VM and an Ubuntu target VM. This experiment focused on IP addressing, source and destination IP fields, TTL, and routing.

## Lab Setup
- Kali Linux VM: traffic generator / pentester machine
- Ubuntu VM: target and packet capture machine
- VirtualBox: virtualization platform
- Ubuntu interface: enp0s3
- Ubuntu IP address: 192.168.1.22
- Tools used: ping, ip route, traceroute, tcpdump, Wireshark

## Method
I captured ICMP traffic on the Ubuntu VM using tcpdump. Then I generated Layer 3 traffic from Kali by sending ICMP Echo Requests using the ping command. I also checked the routing table and used traceroute to observe the network path to the Ubuntu target.

Capture command used:

```bash
sudo tcpdump -i enp0s3 -n -w layer3_icmp_ip_ttl.pcap icmp

Kali command used: ping -c 4

Result

Wireshark showed ICMP Echo Request packets from Kali to Ubuntu and ICMP Echo Reply packets from Ubuntu back to Kali. The IPv4 packet header showed the source IP address, destination IP address, protocol field, and TTL value.

Observed Layer 3 fields included:

Source IP address
Destination IP address
Time To Live
Protocol: ICMP
ICMP Echo Request
ICMP Echo Reply
Packet Analysis

An ICMP Echo Request is a Layer 3 diagnostic packet used to test IP reachability. In this lab, Kali sent Echo Requests to the Ubuntu VM, and Ubuntu returned Echo Replies. This confirmed that Layer 3 connectivity was working between the two virtual machines.

The TTL value showed that each IP packet has a lifetime limit. Routers decrement TTL as packets move through networks. If TTL reaches zero, the packet is discarded. This prevents packets from looping forever.

Security Relevance

Layer 3 is important in cybersecurity because IP addresses, ICMP traffic, routing, and TTL values are commonly used during network discovery and troubleshooting. Attackers and defenders both use ICMP and routing behavior to understand network reachability. Analysts can inspect Layer 3 traffic to identify scanning, misrouting, spoofing attempts, and unusual communication patterns.

Evidence
PCAP file: layer3_icmp_ip_ttl.pcap
Screenshot: Ubuntu IP address and routing table
Screenshot: Kali ping to Ubuntu
Screenshot: Kali routing table
Screenshot: traceroute output
Screenshot: Wireshark ICMP packets
Screenshot: expanded IPv4 header showing source IP, destination IP, and TTL
Screenshot: ICMP Echo Request and Echo Reply fields
Conclusion

This experiment demonstrated that Layer 3 provides logical addressing and routing using IP. The successful ICMP Echo Request and Echo Reply exchange confirmed IP-level communication between Kali and Ubuntu. Wireshark showed the IPv4 and ICMP fields used to deliver and verify network connectivity.
