# 🦈 Wireshark - Network Protocol Analyzer

## 📋 Overview
Wireshark adalah network protocol analyzer yang memungkinkan capture dan analisis traffic network secara real-time.

## 🚀 Basic Usage

### Starting Wireshark
```bash
# GUI mode
wireshark

# Command line (tshark)
tshark -i eth0

# Capture to file
tshark -i eth0 -w capture.pcap
```

### Interface Selection
- Choose appropriate network interface
- Consider monitor mode for wireless
- Use "any" to capture on all interfaces

## 🎯 Display Filters

### Basic Syntax
```
protocol.field operator value
```

### Common Protocols
```bash
# HTTP traffic
http

# HTTPS/TLS
tls
ssl

# DNS queries
dns

# TCP traffic
tcp

# UDP traffic
udp

# ICMP traffic
icmp

# ARP traffic
arp
```

### IP Address Filtering
```bash
# Specific IP
ip.addr == 192.168.1.100

# Source IP
ip.src == 192.168.1.100

# Destination IP
ip.dst == 192.168.1.100

# IP range
ip.addr >= 192.168.1.1 and ip.addr <= 192.168.1.255

# Subnet
ip.addr == 192.168.1.0/24
```

### Port Filtering
```bash
# Specific port
tcp.port == 80

# Source port
tcp.srcport == 80

# Destination port
tcp.dstport == 80

# Port range
tcp.port >= 1000 and tcp.port <= 2000

# Multiple ports
tcp.port in {80 443 8080}
```

### Protocol-Specific Filters
```bash
# HTTP methods
http.request.method == "GET"
http.request.method == "POST"

# HTTP status codes
http.response.code == 200
http.response.code == 404

# HTTP host
http.host == "example.com"

# DNS queries
dns.qry.name == "example.com"

# FTP commands
ftp.request.command == "USER"

# SSH traffic
ssh
```

## 🔥 Advanced Filtering

### Logical Operators
```bash
# AND
tcp.port == 80 and ip.addr == 192.168.1.100

# OR
tcp.port == 80 or tcp.port == 443

# NOT
not arp

# Parentheses for grouping
(tcp.port == 80 or tcp.port == 443) and ip.addr == 192.168.1.100
```

### String Matching
```bash
# Contains string
tcp contains "password"
http contains "login"

# Case insensitive
upper(http.host) contains "EXAMPLE"

# Regular expressions
http.host matches ".*\.example\.com"
```

### Time-based Filtering
```bash
# Relative time
frame.time_relative > 10

# Specific time range
frame.time >= "2023-01-01 00:00:00" and frame.time <= "2023-01-01 23:59:59"
```

## 🎯 Capture Filters (BPF Syntax)

### Basic Syntax
```bash
# Host filtering
host 192.168.1.100

# Port filtering
port 80

# Protocol filtering
tcp
udp
icmp
```

### Advanced Capture Filters
```bash
# Specific host and port
host 192.168.1.100 and port 80

# Network range
net 192.168.1.0/24

# Exclude traffic
not port 22

# Multiple conditions
host 192.168.1.100 and (port 80 or port 443)
```

## 🔧 Analysis Features

### Statistics
```bash
# Protocol hierarchy
Statistics > Protocol Hierarchy

# Conversations
Statistics > Conversations

# Endpoints
Statistics > Endpoints

# I/O graphs
Statistics > I/O Graphs
```

### Following Streams
```bash
# TCP stream
Right-click packet > Follow > TCP Stream

# UDP stream
Right-click packet > Follow > UDP Stream

# HTTP stream
Right-click packet > Follow > HTTP Stream

# TLS stream
Right-click packet > Follow > TLS Stream
```

### Export Objects
```bash
# HTTP objects
File > Export Objects > HTTP

# FTP objects
File > Export Objects > FTP-DATA

# SMB objects
File > Export Objects > SMB
```

## 🛡️ Security Analysis

### Detecting Suspicious Activity
```bash
# Large file transfers
tcp.len > 1000

# Unusual ports
tcp.port > 1024 and tcp.port < 5000

# Failed connections
tcp.flags.reset == 1

# DNS tunneling
dns and frame.len > 512
```

### Credential Hunting
```bash
# HTTP authentication
http.authorization

# FTP credentials
ftp.request.command == "USER" or ftp.request.command == "PASS"

# Telnet credentials
telnet

# SNMP community strings
snmp
```

### Malware Analysis
```bash
# Suspicious user agents
http.user_agent contains "bot"

# Suspicious file downloads
http.request.method == "GET" and http.request.uri contains ".exe"

# Command and control traffic
dns.qry.name matches ".*\.tk$" or dns.qry.name matches ".*\.ml$"
```

## 🎯 Command Line (TShark)

### Basic Usage
```bash
# List interfaces
tshark -D

# Capture on interface
tshark -i eth0

# Capture with filter
tshark -i eth0 -f "host 192.168.1.100"

# Read from file
tshark -r capture.pcap

# Write to file
tshark -i eth0 -w output.pcap
```

### Display Specific Fields
```bash
# Show specific fields
tshark -r capture.pcap -T fields -e frame.time -e ip.src -e ip.dst -e tcp.port

# JSON output
tshark -r capture.pcap -T json

# CSV output
tshark -r capture.pcap -T fields -E separator=, -e ip.src -e ip.dst
```

### Statistics with TShark
```bash
# Protocol hierarchy
tshark -r capture.pcap -q -z io,phs

# Conversations
tshark -r capture.pcap -q -z conv,tcp

# Endpoints
tshark -r capture.pcap -q -z endpoints,ip
```

## 📚 Useful Filters Collection

### Web Traffic Analysis
```bash
# All HTTP traffic
http

# HTTP errors
http.response.code >= 400

# POST requests
http.request.method == "POST"

# Large HTTP responses
http.content_length > 1000000

# Specific user agent
http.user_agent contains "Chrome"
```

### Network Troubleshooting
```bash
# TCP retransmissions
tcp.analysis.retransmission

# TCP resets
tcp.flags.reset == 1

# ICMP errors
icmp.type == 3

# Duplicate ACKs
tcp.analysis.duplicate_ack

# Zero window
tcp.window_size == 0
```

### Security Monitoring
```bash
# SMB authentication failures
smb2.nt_status == 0xc000006d

# Kerberos failures
kerberos.error_code

# LDAP bind failures
ldap.resultCode != 0

# SSH failed logins
ssh and tcp contains "Authentication failed"
```

## 🔗 References
- [Official Wireshark Documentation](https://www.wireshark.org/docs/)
- [Display Filter Reference](https://www.wireshark.org/docs/dfref/)
- [Wireshark User Guide](https://www.wireshark.org/docs/wsug_html_chunked/)
