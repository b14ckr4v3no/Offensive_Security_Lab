# 🔎 Hari 1–2 — Recon Basic (Nmap)

---

## 1. Scan Basic

```bash
nmap -sV -sC -A <IP_Target>
```

- **-sV** → deteksi versi service
- **-sC** → jalankan script dasar Nmap (deteksi login anon, banner grabbing, dll)
- **-A** → OS detection, traceroute, service detail

👉 Catat hasilnya ke tabel:

| Port | Service | Version      | Potensi Exploit           |
|------|---------|--------------|---------------------------|
| 21   | FTP     | vsftpd 2.3.4 | Backdoor known exploit    |
| 22   | SSH     | OpenSSH 4.7  | Weak password brute force |
| 80   | HTTP    | Apache 2.2.8 | Directory traversal       |

---

## 2. Scan Semua Port

```bash
nmap -p- <IP_Target>
```

- **-p-** → scan semua port (1–65535). Kadang service tidak ada di port default

---

## 3. Script Vulnerability

```bash
nmap --script vuln <IP_Target>
```

Jalankan script Nmap khusus untuk cek CVE & vuln umum