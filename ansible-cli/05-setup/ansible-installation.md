# 🛠️ Installing Ansible

Ansible must be installed only on the **controller machine**.

---

## Supported Controller OS
- Ubuntu / Debian
- RHEL / CentOS
- Amazon Linux
- macOS (limited)

---

## Install on Ubuntu / Debian

```bash
sudo apt update
sudo apt install -y ansible
```

---
Verify:
```bash
ansible --version
```

---
Install via Python (latest version)
```bash
pip install ansible
```
🎯 Real-Time Use Case

Ansible is installed on a Jenkins server which acts as the controller for all environments.
