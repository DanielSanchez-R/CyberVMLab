# Layer 7 - Application Layer: HTTP Requests, Responses, and Apache Logs

## Objective
The objective of this experiment was to observe Layer 7 application-layer behavior by generating HTTP requests from a Kali Linux VM to an Apache2 web server running on an Ubuntu VM.

This experiment focused on HTTP methods, HTTP headers, HTTP responses, status codes, User-Agent strings, and Apache access logs.

## Lab Setup
- Kali Linux VM: HTTP client / traffic generator
- Ubuntu VM: Apache2 web server and packet capture machine
- VirtualBox: virtualization platform
- Ubuntu IP address: 192.168.1.22
- Kali IP address: 192.168.1.71
- Ubuntu interface: enp0s3
- Service tested: Apache2 HTTP server
- Port tested: TCP port 80
- Tools used:
  - Apache2
  - curl
  - tcpdump
  - Wireshark
  - Apache access logs
  - systemctl
  - ss

## Method
I started Apache2 on the Ubuntu VM and created a simple custom web page for the lab. I then captured HTTP traffic using tcpdump while sending different HTTP requests from Kali.

The experiment included:
- A normal HTTP GET request
- An HTTP HEAD request
- An HTTP GET request with a custom User-Agent string
- Apache access log monitoring
- Wireshark packet analysis

Custom webpage command:

```bash
echo "Layer 7 Application Layer - Apache HTTP Lab" | sudo tee /var/www/html/index.html

Result

Wireshark showed readable Layer 7 HTTP traffic between Kali and Ubuntu. The packet capture displayed HTTP request methods, headers, User-Agent values, and server responses.

Observed HTTP request data included:

GET / HTTP/1.1
HEAD / HTTP/1.1
Host: 192.168.1.22
User-Agent: Kali-Layer7-Portfolio-Lab

Observed HTTP response data included:

HTTP/1.1 200 OK
Content-Type
Content-Length

Apache access logs also recorded the same requests from Kali. The logs confirmed the client IP address, request method, requested resource, HTTP response code, and User-Agent string.

Packet Analysis

Layer 7 represents application-level communication. In this lab, HTTP was the application-layer protocol.

The GET request asked the Apache server to return the web page content. The HEAD request asked the server to return only the response headers without the page body. The custom User-Agent request showed how clients identify themselves through HTTP headers.

Wireshark confirmed the HTTP traffic at the packet level, while Apache access logs confirmed the same activity from the server side.

This showed that Layer 7 activity can be analyzed from both:

Network packet captures
Application/server logs
Security Relevance

Layer 7 is extremely important in cybersecurity because most user-facing attacks and investigations happen at the application layer.

Web servers expose application behavior through:

HTTP methods
Requested paths
Status codes
Headers
User-Agent strings
Source IP addresses
Web server logs

Understanding Layer 7 traffic helps analysts detect:

Web scanning
Suspicious HTTP methods
Unusual User-Agent strings
Failed requests
Unauthorized access attempts
Application-layer reconnaissance
Web attack patterns
Misconfigured web services

Because this lab used plaintext HTTP, the request and response contents were readable in Wireshark. This also connects back to Layer 6, where HTTPS/TLS was shown to encrypt application data.

Evidence
PCAP file: layer7_http_apache_logs.pcap
Screenshot: Apache2 running on Ubuntu
Screenshot: Custom Apache index page
Screenshot: Kali HTTP GET request
Screenshot: Kali HTTP HEAD request
Screenshot: Kali custom User-Agent request
Screenshot: Apache access log showing Kali requests
Screenshot: Wireshark HTTP GET request
Screenshot: Wireshark HTTP HEAD request
Screenshot: Wireshark HTTP 200 OK response
Screenshot: Wireshark custom User-Agent header
Screenshot: Apache stopped and port 80 closed after cleanup
