# OSI 7-Layer Cybersecurity VM Lab

## Project Overview

This project documents a local cybersecurity/networking lab built with two virtual machines: Kali Linux and Ubuntu Linux. The goal of the lab was to demonstrate how network communication can be observed and analyzed across all seven layers of the OSI model.

Kali Linux was used as the client, traffic generator, and testing machine. Ubuntu Linux was used as the target machine, server, and packet capture system. Wireshark and tcpdump were used to collect and analyze packet captures for each layer.

All testing was performed in an authorized local VM lab environment.

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
