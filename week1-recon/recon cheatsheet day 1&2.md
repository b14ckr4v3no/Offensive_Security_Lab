# 🧾 Recon Cheat Sheet (Before Exploit)

---

## 1️⃣ Identifikasi Target
- **Ping sweep / host discovery**
  ```bash
  nmap -sn 192.168.56.0/24
  ```
  → cek host mana yang hidup.
- **OS fingerprinting**
  ```bash
  nmap -O <IP_Target>
  ```
  → deteksi sistem operasi.

---

## 2️⃣ Port & Service Scanning
- **Quick scan (common ports)**
  ```bash
  nmap -sV -sC <IP_Target>
  ```
- **Full port scan**
  ```bash
  nmap -p- <IP_Target>
  ```
- **Aggressive scan (detail lengkap)**
  ```bash
  nmap -A <IP_Target>
  ```

---

## 3️⃣ Enumeration (Info Lanjutan)
- **FTP**
  ```bash
  nmap -p21 --script ftp-anon <IP_Target>
  ```
- **SMB**
  ```bash
  nmap -p445 --script smb-enum-shares,smb-enum-users <IP_Target>
  ```
- **HTTP**
  ```bash
  whatweb http://<IP_Target>
  gobuster dir -u http://<IP_Target> -w /usr/share/wordlists/dirb/common.txt
  ```
- **Banner grabbing (manual)**
  ```bash
  nc <IP_Target> <port>
  ```

---

## 4️⃣ Analisis Hasil
Buat tabel hasil recon:

| Port  | Service | Version     | Potensi Exploit                |
|-------|---------|-------------|--------------------------------|
| 21    | FTP     | vsftpd 2.3.4| CVE-2011-2523 (backdoor)       |
| 80    | HTTP    | Apache 2.2.8| Directory traversal            |
| 3306  | MySQL   | 5.0.51a     | Auth bypass                    |

Cross-check di:
- [Exploit-DB](https://www.exploit-db.com/)
- `searchsploit <service> <version>`
- [CVE Database](https://cve.mitre.org/)

---

## 5️⃣ Dokumentasi
- Catat hasil scan + versi service.
- Simpan screenshot atau output command.
- Jangan buru-buru exploit → buat peta dulu.

---

## ⚡ Aturan Praktis
> Pengintaian bukan tentang menemukan jalan masuk.<br>
> Ini tentang memahami medan sehingga Anda tahu pintu mana yang harus diketuk.