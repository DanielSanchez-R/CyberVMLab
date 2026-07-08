# Layer 6 - Presentation Layer: HTTP vs HTTPS and TLS Encryption

## Objective
The objective of this experiment was to observe Layer 6 presentation-layer behavior by comparing plaintext HTTP traffic with encrypted HTTPS/TLS traffic.

This lab demonstrated how data can be readable when transmitted without encryption and protected when transmitted through TLS.

## Lab Setup
- Kali Linux VM: client / traffic generator
- Ubuntu VM: Apache2 web server and packet capture machine
- VirtualBox: virtualization platform
- Ubuntu IP address: 192.168.1.22
- Kali IP address: 192.168.1.71
- Ubuntu interface: enp0s3
- Services tested:
  - HTTP on TCP port 80
  - HTTPS on TCP port 443
- Tools used:
  - Apache2
  - curl
  - tcpdump
  - Wireshark
  - systemctl
  - ss

## Method
I configured Apache2 on the Ubuntu VM to serve web traffic over both HTTP and HTTPS. HTTP used TCP port 80, while HTTPS used TCP port 443 with TLS encryption.

I started a packet capture on Ubuntu, then generated web requests from Kali using curl. First, I made a plaintext HTTP request. Then I made an HTTPS request using the `-k` option because the Apache HTTPS site used a local self-signed certificate.

Capture command used on Ubuntu:

```bash
sudo tcpdump -i enp0s3 -n -w layer6_http_vs_https.pcap 'host 192.168.1.71 and (tcp port 80 or tcp port 443)'

HTTP request from Kali: curl -v http://

HTTPS request from Kali: curl -vk https://

Result

The HTTP traffic on port 80 was visible in Wireshark as readable plaintext. Wireshark showed the HTTP request and response clearly.

Examples of readable HTTP data included:

GET / HTTP/1.1
HTTP/1.1 200 OK

The HTTPS traffic on port 443 was not readable as plaintext. Instead, Wireshark showed TLS handshake packets and encrypted application data.

Examples of HTTPS/TLS traffic included:

Client Hello
Server Hello
Certificate
Encrypted Application Data

This confirmed that HTTP exposes web request data, while HTTPS protects the application data with encryption.

Packet Analysis

HTTP sends application-layer data without encryption. This means packet captures can reveal HTTP methods, URLs, headers, and sometimes page content.

HTTPS uses TLS to encrypt the application data. Wireshark can still show metadata such as source IP, destination IP, source port, destination port, packet length, and TLS handshake information. However, the actual web request and response contents are encrypted and not readable without the session keys.

In this experiment, the difference was visible:

Port 80 showed readable HTTP data.
Port 443 showed TLS negotiation and encrypted application data.
Security Relevance

Layer 6 is important in cybersecurity because it deals with data representation, encoding, compression, and encryption.

This experiment demonstrates why HTTPS is preferred over HTTP. If sensitive information is sent over HTTP, anyone with packet capture access may be able to read it. HTTPS protects confidentiality by encrypting the communication.

This is relevant for:

Detecting plaintext protocols
Identifying insecure web services
Understanding TLS encryption
Analyzing encrypted versus unencrypted traffic
Recognizing certificate usage
Explaining why credentials should not be sent over HTTP
Evidence
PCAP file: layer6_http_vs_https.pcap
Screenshot: Apache listening on ports 80 and 443
Screenshot: Kali HTTP curl request
Screenshot: Kali HTTPS curl request
Screenshot: Wireshark HTTP plaintext GET request
Screenshot: Wireshark HTTP 200 OK response
Screenshot: Wireshark TLS Client Hello / Server Hello
Screenshot: Wireshark encrypted TLS application data
Screenshot: Apache2 stopped and ports 80/443 closed after the test
Cleanup

After the experiment, I stopped Apache2 and disabled it to make sure ports 80 and 443 were closed.

Commands used:

sudo systemctl stop apache2
sudo systemctl disable apache2
sudo ss -tulpen | grep -E ':80|:443'

If the final command returned no output, then no service was listening on ports 80 or 443.

I also confirmed from Kali using:

nmap -p 80,443 --reason 192.168.1.22

Conclusion

This experiment demonstrated the Layer 6 difference between plaintext and encrypted communication. HTTP traffic on port 80 was readable in Wireshark, while HTTPS traffic on port 443 was protected by TLS encryption.

The lab showed how the presentation layer supports confidentiality by transforming readable application data into encrypted traffic before transmission.
