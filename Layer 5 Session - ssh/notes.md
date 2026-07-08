# Layer 5 - Session Layer: SSH Session Establishment and Termination

## Objective
The objective of this experiment was to observe session-layer behavior by establishing an SSH session from the Kali Linux VM to the Ubuntu target VM. This experiment focused on session creation, authentication logging, encrypted session traffic, and session termination.

## Lab Setup
- Kali Linux VM: SSH client / traffic generator
- Ubuntu VM: SSH server / target and packet capture machine
- VirtualBox: virtualization platform
- Ubuntu IP address: 192.168.1.22
- Kali IP address: 192.168.1.71
- Ubuntu interface: enp0s3
- Service tested: OpenSSH Server
- Port tested: TCP port 22
- Tools used: ssh, OpenSSH Server, tcpdump, Wireshark, ss, systemctl, auth logs

## Method
I installed and started the OpenSSH server on the Ubuntu VM. I then captured TCP port 22 traffic using tcpdump while initiating an SSH login from the Kali VM to the Ubuntu VM. After logging in, I ran basic commands inside the SSH session and then exited the session. The resulting packet capture was opened in Wireshark for analysis.

Capture command used on Ubuntu:

```bash
sudo tcpdump -i enp0s3 -n -w layer5_ssh_session.pcap 'tcp port 22'

Result

The SSH session was successfully established from Kali to Ubuntu. Wireshark showed the TCP connection setup, SSH protocol negotiation, encrypted SSH traffic, and session termination. Ubuntu authentication logs confirmed that the user daniel logged in through SSH.

Packet Analysis

The SSH session began with a TCP three-way handshake:

Kali   → Ubuntu: SYN
Ubuntu → Kali:   SYN, ACK
Kali   → Ubuntu: ACK

After the TCP connection was established, the SSH protocol began. Wireshark showed SSH packets, but the contents were encrypted. This means the packet capture confirmed the session activity without exposing the username password or commands in plaintext.

The session ended with TCP connection termination packets such as FIN and ACK.

Security Relevance

Layer 5 is important in cybersecurity because many attacks and defensive investigations involve sessions. Analysts need to understand when a session starts, how long it lasts, what service it uses, and when it terminates.

SSH is also security-relevant because it is commonly used for remote administration. Monitoring SSH sessions can help defenders identify:

Successful logins
Failed login attempts
Unexpected remote access
Session duration
Source and destination IP addresses
Encrypted administrative traffic
Evidence
PCAP file: layer5_ssh_session.pcap
Screenshot: Ubuntu SSH service running
Screenshot: Kali SSH login to Ubuntu
Screenshot: Ubuntu SSH authentication log
Screenshot: Wireshark SSH traffic filter
Screenshot: TCP handshake for SSH session
Screenshot: encrypted SSH packets
Screenshot: SSH session termination
Conclusion

This experiment demonstrated session-layer behavior using SSH. Kali established a remote login session with the Ubuntu VM over TCP port 22. Wireshark confirmed the session setup and encrypted communication, while Ubuntu logs confirmed the authenticated login event. This shows how network traffic and host logs can be combined to analyze remote access sessions.
