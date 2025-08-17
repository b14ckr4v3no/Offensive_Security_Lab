# 🗺️ Nmap - Network Mapper

## 📋 Overview
Nmap (Network Mapper) adalah tool open source untuk network discovery dan security auditing.

## 🚀 Basic Usage

### Host Discovery
```bash
# Ping scan
nmap -sn 192.168.1.0/24

# ARP scan (local network)
nmap -PR 192.168.1.0/24
```

### Port Scanning
```bash
# Basic TCP scan
nmap 192.168.1.100

# TCP SYN scan (stealth)
nmap -sS 192.168.1.100

# UDP scan
nmap -sU 192.168.1.100

# Specific ports
nmap -p 80,443,22 192.168.1.100

# All ports
nmap -p- 192.168.1.100
```

### Service & Version Detection
```bash
# Service version detection
nmap -sV 192.168.1.100

# OS detection
nmap -O 192.168.1.100

# Aggressive scan
nmap -A 192.168.1.100
```

### NSE Scripts
```bash
# Default scripts
nmap -sC 192.168.1.100

# Vulnerability scripts
nmap --script vuln 192.168.1.100

# SMB scripts
nmap --script smb* 192.168.1.100
```

## 🎯 Common Commands

| Command | Description |
|---------|-------------|
| `nmap -sn target` | Ping scan only |
| `nmap -sS target` | SYN stealth scan |
| `nmap -sV target` | Version detection |
| `nmap -O target` | OS detection |
| `nmap -A target` | Aggressive scan |
| `nmap -p- target` | Scan all ports |

## 🔥 Advanced Techniques

### Timing Templates
```bash
# Paranoid (slowest)
nmap -T0 target

# Sneaky
nmap -T1 target

# Polite
nmap -T2 target

# Normal (default)
nmap -T3 target

# Aggressive
nmap -T4 target

# Insane (fastest)
nmap -T5 target
```

### Output Formats
```bash
# Normal output
nmap -oN scan.txt target

# XML output
nmap -oX scan.xml target

# Grepable output
nmap -oG scan.grep target

# All formats
nmap -oA scan target
```

## ⚠️ Evasion Techniques
```bash
# Fragment packets
nmap -f target

# Decoy scan
nmap -D RND:10 target

# Source port
nmap --source-port 53 target

# Randomize hosts
nmap --randomize-hosts target1 target2
```

## 📚 Useful NSE Categories
- `auth` - Authentication bypass
- `broadcast` - Network broadcast discovery
- `brute` - Brute force attacks
- `default` - Default scripts
- `discovery` - Host and service discovery
- `dos` - Denial of service
- `exploit` - Exploitation scripts
- `external` - Scripts requiring external resources
- `fuzzer` - Fuzzing scripts
- `intrusive` - Intrusive scripts
- `malware` - Malware detection
- `safe` - Safe scripts
- `version` - Version detection
- `vuln` - Vulnerability detection

## 🎯 Pro Tips
1. Always start with basic scan before aggressive
2. Use timing templates appropriately
3. Save output in multiple formats
4. Combine different scan types for comprehensive results
5. Use NSE scripts for specific services

## 🔗 References
- [Official Nmap Documentation](https://nmap.org/docs.html)
- [Nmap Cheat Sheet](https://www.stationx.net/nmap-cheat-sheet/)
- [NSE Script Documentation](https://nmap.org/nsedoc/)
