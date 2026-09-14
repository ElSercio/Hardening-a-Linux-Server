# Hardening-a-Linux-Server

## 🛡️ Phase 1: Antimalware Protection & System Scanning

### Objective
Deploy and configure host-based antimalware solutions to detect, report,
and remediate malicious files, and to identify signs of rootkits or
system-level compromise.

### Tools Used
- **aptitude** — advanced package management for dependency resolution
- **ClamAV** (`clamav`, `clamav-daemon`, `clamav-freshclam`) — open-source
  antivirus engine for detecting trojans, viruses, and malware
- **rkhunter** (Rootkit Hunter) — scans for rootkits, backdoors, and local
  exploits

### Implementation

**1. Package Management Setup**
Installed `aptitude` as an alternative package manager to streamline
dependency handling during the hardening process.
```bash
sudo apt install aptitude
```

**2. ClamAV Installation & Configuration**
Installed the ClamAV antivirus engine along with its daemon and
signature-update service.
```bash
sudo apt install clamav clamav-daemon clamav-freshclam
```
Stopped the `clamav-freshclam` and `clamav-daemon` services to safely
reconfigure them via `dpkg-reconfigure`, ensuring the virus database
and daemon settings were properly initialized before running scans.
```bash
sudo systemctl stop clamav-freshclam clamav-daemon
sudo dpkg-reconfigure clamav-freshclam
sudo dpkg-reconfigure clamav-daemon
```

**3. Full System Scan & Remediation**
Performed a recursive scan of the filesystem, automatically removing
any infected files found.
```bash
sudo clamscan -ri --remove
```

**4. Rootkit Detection with rkhunter**
Installed and updated the rkhunter signature database, then ran a full
system check to detect rootkits, hidden processes, and suspicious
system modifications.
```bash
sudo apt install rkhunter
sudo rkhunter --update
sudo rkhunter --check
```

### Outcome
The server now has active malware scanning capabilities via ClamAV and
rootkit detection through rkhunter, adding a critical layer of
host-based threat detection to complement the network and access
controls implemented in earlier phases.

### You can find the evidences on this repository

