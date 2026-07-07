# Layer 2 - Data Link Layer: ARP and MAC Address Resolution

## Objective
The objective of this experiment was to observe Layer 2 network behavior by capturing ARP traffic and identifying how IP addresses are mapped to MAC addresses on a local network.

## Lab Setup
- Kali Linux VM: traffic generator / pentester machine
- Ubuntu VM: target and packet capture machine
- VirtualBox: virtualization platform
- Ubuntu interface: enp0s3
- Ubuntu IP address: 192.168.1.22
- Ubuntu MAC address: 08:00:27:ca:dd:9d
- Gateway/router IP address: 192.168.1.1
- Tools used: tcpdump, Wireshark, ping, ip route, ip neigh

## Method
I captured ARP and ICMP traffic on the Ubuntu VM using tcpdump. I then generated network traffic by pinging between systems and observing how ARP resolved IP addresses to MAC addresses. The packet capture was opened in Wireshark and filtered using the `arp` display filter.

Command used to capture traffic:

```bash
sudo tcpdump -i enp0s3 -n -e -w layer2_arp_mac_test.pcap 'arp or icmp'

Wireshark filter used: arp

Result

Wireshark showed ARP request and ARP reply packets. One ARP request asked:

The ARP reply used a unicast destination because the target MAC address was known after resolution.

Important fields observed in Wireshark:

Ethernet source MAC address
Ethernet destination MAC address
Sender MAC address
Sender IP address
Target MAC address
Target IP address
ARP opcode request/reply
Security Relevance

ARP is important in cybersecurity because it controls local network address resolution. Attackers can abuse ARP through ARP spoofing or ARP poisoning to intercept traffic, redirect traffic, or perform man-in-the-middle attacks. Understanding normal ARP behavior helps analysts recognize suspicious ARP activity.

VM Networking Observation

The Ubuntu VM used a VirtualBox MAC address beginning with 08:00:27, which is commonly associated with VirtualBox virtual network adapters. This confirms that the traffic came from a virtualized network interface.

Because the lab uses virtualization and NAT/bridged networking, some Layer 2 visibility may show the gateway or VirtualBox network path instead of direct VM-to-VM MAC addressing. This is expected and demonstrates the difference between Layer 2 local delivery and Layer 3 IP reachability.

Evidence
PCAP file: layer2_arp_mac_test.pcap
Screenshot: ARP request in Wireshark
Screenshot: ARP reply in Wireshark
Screenshot: expanded Ethernet II header
Screenshot: expanded Address Resolution Protocol fields
Conclusion

This experiment demonstrated that Layer 2 uses MAC addresses for local network delivery and ARP to map IP addresses to MAC addresses. The packet capture confirmed that the Ubuntu VM responded to an ARP request for 192.168.1.22 with its MAC address 08:00:27:ca:dd:9d.
