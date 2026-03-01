# 🪟 WinRM Setup for Ansible (Windows Hosts)

Ansible uses **WinRM (Windows Remote Management)** to communicate with Windows hosts.

This document explains **how to configure WinRM securely** for Ansible automation.

---

## ❓ Why WinRM is Required

- Windows does not support SSH natively (like Linux)
- WinRM enables remote command execution
- Ansible connects to Windows using WinRM over HTTP/HTTPS

---

## 🔐 WinRM Connection Types

### ❌ Insecure (HTTP – NOT recommended)

- Port: `5985`
- No encryption
- Only for testing or labs

### ✅ Secure (HTTPS – Recommended for production)

- Port: `5986`
- Encrypted using SSL certificates
- Used in enterprise environments

---

## 🧰 Prerequisites

On the **Windows host**:
- Windows Server / Windows 10+
- Administrator access
- PowerShell (Run as Administrator)

On the **Ansible controller**:
- Python installed
- `pywinrm` package installed

```bash
pip install pywinrm
```

---

🔧 Step 1: Enable WinRM on Windows Host

Open PowerShell as Administrator and run:
```bash
winrm quickconfig
```

This will:

- Start WinRM service
- Set it to auto-start
- Open firewall rules

---

🔒 Step 2: Configure WinRM over HTTPS (Secure)

Create a Self-Signed Certificate
```bash
$cert = New-SelfSignedCertificate `
  -DnsName "windows-host" `
  -CertStoreLocation Cert:\LocalMachine\My
```

Note the **Thumbprint.**

---
**Create HTTPS Listener**
```bash
winrm create winrm/config/Listener?Address=*+Transport=HTTPS `
'@{Hostname="windows-host"; CertificateThumbprint="THUMBPRINT"}'
```

Replace **THUMBPRINT** with the actual certificate thumbprint.

---
🔥 Step 3: Open Firewall Port
```bash
netsh advfirewall firewall add rule name="WinRM HTTPS" dir=in action=allow protocol=TCP localport=5986
```
---

🔐 Step 4: Configure Authentication
```bash
winrm set winrm/config/service/auth '@{Basic="true"}'
winrm set winrm/config/service '@{AllowUnencrypted="false"}'
```

---
🖥️ Step 5: Configure Controller Trust (Linux)

Copy certificate from Windows to controller and convert to .crt.
Place it in:
```bash
/usr/share/ca-certificates/
```

Then update certificates:
```bash
sudo update-ca-certificates
```

---
📦 Inventory Configuration Example

```ini
[win]
windows_host ansible_host=65.2.xxx.xxx
ansible_user=Administrator
ansible_password=********
ansible_connection=winrm
ansible_winrm_transport=basic
ansible_winrm_port=5986
ansible_winrm_server_cert_validation=ignore
```

⚠️ Password must be stored using Ansible Vault.

---
🧪 Step 6: Test Connectivity

```bash
ansible win -m win_ping
```

Expected output:
```bash
win_ping: pong
```

---
🎯 Real-Time Use Case

Used to:

- Patch Windows servers
- Restart IIS
- Manage Windows services
- Apply security baselines
