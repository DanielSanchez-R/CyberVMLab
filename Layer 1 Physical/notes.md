# Layer 1 - Physical Layer: Virtual Link Test

## Objective
The objective of this experiment was to demonstrate how loss of a network link affects communication between two virtual machines.

## Lab Setup
- Kali Linux VM: traffic generator / pentester machine
- Ubuntu VM: target machine
- VirtualBox: virtualization platform
- Tooling: ping, ip command, tcpdump, Wireshark

## Method
I first confirmed that the Ubuntu network interface was active and reachable from Kali using ICMP ping. Then I disabled the Ubuntu network interface using the `ip link set down` command and attempted the same ping test again. After observing failure, I re-enabled the interface and restored connectivity.

## Result
When the Ubuntu interface was UP, Kali successfully sent ICMP Echo Requests and received Echo Replies. When the Ubuntu interface was DOWN, Kali could no longer communicate with the Ubuntu VM.

## Security Relevance
This demonstrates that all higher-layer network activity depends on lower-layer link availability. In cybersecurity operations, link failure, cable disconnects, disabled adapters, or virtual NIC issues can appear as complete service outages even when the operating system and applications are still running.

## Evidence
- Interface UP screenshot
- Successful Kali ping screenshot
- Interface DOWN screenshot
- Failed Kali ping screenshot
- Wireshark/tcpdump packet capture
