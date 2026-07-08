# OSI 7-Layer Cybersecurity VM Lab

## Project Overview

This project documents a local cybersecurity/networking lab built with two virtual machines: Kali Linux and Ubuntu Linux. The goal of the lab was to demonstrate how network communication can be observed and analyzed across all seven layers of the OSI model.

Kali Linux was used as the client, traffic generator, and testing machine. Ubuntu Linux was used as the target machine, server, and packet capture system. Wireshark and tcpdump were used to collect and analyze packet captures for each layer.

All testing was performed in an authorized local VM lab environment.

Linux administration
Virtual machine networking
Packet capture
Wireshark analysis
tcpdump usage
Nmap scanning in an authorized lab
Apache2 service management
SSH session testing
HTTP vs HTTPS analysis
TCP open/closed port behavior
ARP/MAC address analysis
ICMP/IP/TTL analysis
Documentation discipline
Cleanup and service shutdown

---

## Lab Topology

OSI 7-Layer Cybersecurity VM Lab Topology](osi_7_layer_vm_lab_topology.png-diagram )

### Systems Used

| System | Role | IP Address |
|---|---|---|
| Kali Linux VM | Client / traffic generator | 192.168.1.71 |
| Ubuntu Linux VM | Target / server / packet capture machine | 192.168.1.22 |
| VirtualBox | Virtualization platform | Local VM network |
| Ubuntu Interface | Capture interface | enp0s3 |

---

## Tools Used

- Oracle VM VirtualBox
- Kali Linux
- Ubuntu Linux
- Wireshark
- tcpdump
- Nmap
- Apache2
- OpenSSH Server
- curl
- ping
- traceroute
- systemctl
- ss

---

## Project Structure

```text

├── README.md
├── topology-diagram.png
│
├── Layer 1/
│   ├── notes.md
│   └── screenshots & pcap/ kali linux screenshots
│
├── Layer 2/
│   ├── notes.md
│   └── screenshots & pcap/ kali linux screenshots
│
├── Layer 3/
│   ├── notes.md
│   └── screenshots & pcap/ kali linux screenshots
│
├── Layer 4/
│   ├── notes.md
│   └── screenshots & pcap/ kali linux screenshots
│
├── Layer 5/
│   ├── notes.md
│   └── screenshots & pcap/ kali linux screenshots
│
├── Layer 6/
│   ├── notes.md
│   └── screenshots & pcap/ kali linux screenshots
│
└── layer 7/
    ├── notes.md
    └── screenshots & pcap/ kali linux screenshots

Layer 1 - Physical Layer

This experiment demonstrated how link availability affects network communication. The Ubuntu VM network interface was disabled and re-enabled to show that higher-layer communication fails when the link is down.

Main concepts demonstrated:

Interface up/down state
Virtual network adapter behavior
Connectivity failure when the link is disabled

Evidence:

PCAP file
Interface state screenshots
Successful and failed ping screenshots


Layer 2 - Data Link Layer

This experiment captured ARP traffic to show how IP addresses are mapped to MAC addresses on a local network.

Main concepts demonstrated:

ARP request
ARP reply
Ethernet II headers
MAC address resolution
Broadcast MAC address

Evidence:

layer2_arp_mac_test.pcap
ARP request screenshot
ARP reply screenshot
Ethernet header screenshot

Layer 3 - Network Layer

This experiment used ICMP traffic to demonstrate IP-level communication between Kali and Ubuntu.

Main concepts demonstrated:

Source IP address
Destination IP address
ICMP Echo Request
ICMP Echo Reply
TTL
Routing

Evidence:

layer3_icmp_ip_ttl.pcap
Ping screenshots
Routing table screenshots
Wireshark IPv4 header screenshots


Layer 4 - Transport Layer

This experiment compared TCP behavior when port 80 was open versus closed.

Apache2 was started to open TCP port 80, then stopped to close the port. Nmap and Wireshark were used to observe the difference.

Open port behavior:

SYN
SYN, ACK
ACK

Closed port behavior:

SYN
RST, ACK

Main concepts demonstrated:

TCP ports
TCP three-way handshake
Open port detection
Closed port reset behavior
Nmap scan results

Evidence:

layer4_tcp_open_closed.pcap
Nmap open-port screenshot
Nmap closed-port screenshot
TCP handshake screenshot
TCP reset screenshot

Layer 5 - Session Layer

This experiment used SSH to demonstrate session establishment, encrypted session traffic, authentication logging, and session termination.

Main concepts demonstrated:

SSH session setup
TCP session behavior
Encrypted remote login
Authentication logs
Session close behavior

Evidence:

layer5_ssh_session.pcap
Successful SSH login screenshot
Ubuntu authentication log screenshot
Wireshark SSH packet screenshots

Layer 6 - Presentation Layer

This experiment compared plaintext HTTP traffic with encrypted HTTPS/TLS traffic.

HTTP behavior:

GET / HTTP/1.1
HTTP/1.1 200 OK

HTTPS/TLS behavior:

Client Hello
Server Hello
Certificate
Encrypted Application Data

Main concepts demonstrated:

Plaintext HTTP
TLS encryption
HTTPS traffic protection
Readable versus encrypted application data

Evidence:

layer6_http_vs_https.pcap
HTTP plaintext screenshot
TLS handshake screenshot
Encrypted application data screenshot

Layer 7 - Application Layer

This experiment demonstrated HTTP application-layer behavior using Apache2 web server logs and Wireshark packet captures.

Kali generated HTTP GET, HEAD, and custom User-Agent requests to the Ubuntu Apache server.

Main concepts demonstrated:

HTTP GET request
HTTP HEAD request
HTTP response codes
HTTP headers
User-Agent strings
Apache access logs

Example HTTP data observed:

GET / HTTP/1.1
HEAD / HTTP/1.1
User-Agent: Kali-Layer7-Portfolio-Lab
HTTP/1.1 200 OK

Evidence:

layer7_http_apache_logs.pcap
Apache access log screenshot
Wireshark HTTP GET screenshot
Wireshark HTTP HEAD screenshot
Custom User-Agent screenshot
Security Relevance

This lab demonstrates how network analysts and cybersecurity defenders can use packet captures, system logs, and service behavior to understand network activity across the OSI model.

The project shows how to identify:

Interface failures
ARP behavior
IP communication
ICMP traffic
TCP open and closed ports
SSH sessions
Plaintext versus encrypted traffic
HTTP requests and web server logs

Understanding these layers helps with troubleshooting, network defense, incident response, and traffic analysis.
