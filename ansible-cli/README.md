# 🤖 Ansible Learning — POC & Documentation

> **Author:** Karthi S | DevOps Learner  
> **GitHub:** [Karthi2305/ansible](https://github.com/Karthi2305/ansible)  
> **LinkedIn:** [karthi-s2001](https://www.linkedin.com/in/karthi-s2001/)

---

## 📌 Overview

This repository is a structured **Proof of Concept (POC) and Documentation** project for learning **Ansible** — the industry-standard, agentless IT automation tool used for configuration management, application deployment, and infrastructure orchestration.

The learning is organized from fundamentals to hands-on examples, covering both **Linux (SSH)** and **Windows (WinRM)** automation — a combination rarely covered in beginner-level POCs.

---

## 📂 Repository Structure

```
ansible-main/
└── ansible-cli/
    ├── 01-introduction/
    │   ├── what-is-ansible.md          # Ansible overview
    │   ├── why-ansible.md              # Benefits & real-world use cases
    │   └── ansible-vs-others.md        # Ansible vs Puppet vs Chef comparison
    │
    ├── 02-core-concepts/
    │   ├── controller-vs-host.md       # Architecture: Controller & Managed Hosts
    │   ├── inventory.md                # Inventory basics
    │   ├── modules.md                  # Core Ansible modules
    │   ├── playbooks.md                # Playbook fundamentals
    │   └── connectivity-linux-windows.md # SSH vs WinRM explained
    │
    ├── 03-security/
    │   ├── ansible-vault.md            # Encrypting secrets with Vault
    │   └── secrets-best-practices.md   # Production secrets management
    │
    ├── 04-tools/
    │   ├── ansible-doc.md              # Module documentation tool
    │   ├── ansible-galaxy.md           # Community roles registry
    │   └── ansible-lint.md             # Playbook linting & best practices
    │
    ├── 05-setup/
    │   ├── ansible-installation.md     # Install Ansible on controller
    │   └── winrm-setup.md              # Configure WinRM for Windows hosts
    │
    └── 06-examples/
        ├── cli-commands.md             # All important CLI commands with use cases
        ├── inventories/
        │   ├── hosts.ini               # Static INI inventory (web, db, win groups)
        │   └── README.md
        ├── playbooks/
        │   ├── install_nginx.yml       # Deploy NGINX on web servers
        │   ├── install_mysql.yml       # Deploy MySQL on DB servers with Vault
        │   └── README.md
        └── group_vars/
            ├── web/
            │   ├── secrets.yml         # NGINX credentials (Vault-encrypted)
            │   └── README.md
            └── db/
                ├── secrets.yml         # MySQL credentials (Vault-encrypted)
                └── README.md
```

---

## 🧠 Topics Covered

### 01 — Introduction
| File | What You Learn |
|------|---------------|
| `what-is-ansible.md` | What Ansible is, how it works, why it's agentless |
| `why-ansible.md` | Key advantages: agentless, idempotent, YAML-based, SSH/WinRM |
| `ansible-vs-others.md` | Side-by-side comparison with Puppet and Chef |

### 02 — Core Concepts
| File | What You Learn |
|------|---------------|
| `controller-vs-host.md` | Controller architecture, managed node requirements, real CI/CD use case |
| `inventory.md` | Static & dynamic inventory, groups, variables |
| `modules.md` | apt, yum, service, copy, template, user modules |
| `playbooks.md` | YAML structure, plays, tasks, modules |
| `connectivity-linux-windows.md` | SSH (Linux) vs WinRM (Windows) connectivity |

### 03 — Security
| File | What You Learn |
|------|---------------|
| `ansible-vault.md` | Create, edit, view encrypted secrets |
| `secrets-best-practices.md` | What NOT to do, never commit plain-text secrets |

### 04 — Tools
| File | What You Learn |
|------|---------------|
| `ansible-doc.md` | Look up module parameters instantly from CLI |
| `ansible-galaxy.md` | Download and reuse community-built roles |
| `ansible-lint.md` | Enforce best practices in CI/CD pipelines |

### 05 — Setup
| File | What You Learn |
|------|---------------|
| `ansible-installation.md` | Install via apt or pip on Ubuntu, RHEL, Amazon Linux |
| `winrm-setup.md` | Full WinRM HTTPS setup with certificates for Windows hosts |

### 06 — Hands-On Examples
| Resource | What It Demonstrates |
|----------|---------------------|
| `hosts.ini` | Static inventory with web, db, and Windows groups |
| `install_nginx.yml` | Install & start NGINX on web servers using `apt` + `service` modules |
| `install_mysql.yml` | Install MySQL on DB servers with Vault-encrypted secrets |
| `group_vars/web/secrets.yml` | NGINX credentials secured with Ansible Vault |
| `group_vars/db/secrets.yml` | MySQL root & app user credentials secured with Ansible Vault |
| `cli-commands.md` | 15+ essential CLI commands with real-world use cases |

---

## ⚙️ Getting Started

### Prerequisites
- Ubuntu / Debian / RHEL Linux (controller machine)
- Python 3.6+
- SSH access to managed Linux hosts
- (Optional) Windows hosts with WinRM enabled

### 1. Clone the Repository

```bash
git clone https://github.com/Karthi2305/ansible.git
cd ansible/ansible-cli
```

### 2. Install Ansible

```bash
# Ubuntu / Debian
sudo apt update && sudo apt install -y ansible

# Via pip (latest version)
pip install ansible

# Verify
ansible --version
```

### 3. Test Connectivity

```bash
ansible all -m ping -i 06-examples/inventories/hosts.ini
```

### 4. Run Playbooks

```bash
# Install NGINX on web servers
ansible-playbook -i 06-examples/inventories/hosts.ini \
  06-examples/playbooks/install_nginx.yml

# Install MySQL on DB servers (with Vault secrets)
ansible-playbook -i 06-examples/inventories/hosts.ini \
  06-examples/playbooks/install_mysql.yml --ask-vault-pass
```

---

## 🔐 Secrets Management

This project uses **Ansible Vault** to encrypt sensitive variables.

```bash
# Encrypt secrets file
ansible-vault encrypt 06-examples/group_vars/db/secrets.yml

# View encrypted file
ansible-vault view 06-examples/group_vars/db/secrets.yml

# Edit encrypted file
ansible-vault edit 06-examples/group_vars/db/secrets.yml
```

> ⚠️ **Never commit plain-text passwords to GitHub.** Always encrypt using Ansible Vault before pushing.

---

## 🖥️ Key Playbooks

### install_nginx.yml — NGINX on Web Servers

```yaml
- name: Install and configure NGINX on web servers
  hosts: web
  become: true
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install NGINX
      apt:
        name: nginx
        state: present

    - name: Ensure NGINX service is running
      service:
        name: nginx
        state: started
        enabled: true
```

### install_mysql.yml — MySQL on DB Servers with Vault

```yaml
- name: Install and configure MySQL on database servers
  hosts: db
  become: true
  vars_files:
    - ../group_vars/db/secrets.yml
  tasks:
    - name: Install MySQL Server
      apt:
        name: mysql-server
        state: present

    - name: Ensure MySQL service is running
      service:
        name: mysql
        state: started
        enabled: true
```

---

## 🔁 Essential CLI Commands

```bash
# Check connectivity to all hosts
ansible all -m ping

# Gather system facts from a group
ansible web -m setup

# Run a shell command on all servers
ansible all -m shell -a "df -h"

# Dry run (no actual changes)
ansible-playbook playbook.yml --check

# Show config differences before applying
ansible-playbook playbook.yml --diff

# Limit execution to specific host
ansible-playbook playbook.yml --limit 192.168.1.10

# Validate inventory structure
ansible-inventory -i inventories/hosts.ini --list

# Lint your playbook
ansible-lint playbook.yml

# View module documentation
ansible-doc apt
```

---

## 📊 Ansible vs Other Tools

| Feature | Ansible | Puppet | Chef |
|---------|---------|--------|------|
| Architecture | Agentless ✅ | Agent-based ❌ | Agent-based ❌ |
| Language | YAML (Simple) | DSL (Complex) | Ruby |
| Learning Curve | Low ✅ | Steep | Medium |
| Execution | Push-based | Pull-based | Pull-based |
| Windows Support | WinRM ✅ | Limited | Limited |
| Setup Overhead | Minimal ✅ | Heavy | High |

---

## 🪟 Windows Automation (WinRM)

This POC covers **Windows host automation** — a unique, production-relevant topic:

- WinRM HTTP (Port 5985) — Lab/Testing
- WinRM HTTPS (Port 5986) — Production with SSL certificates
- pywinrm Python package for controller connectivity
- `win_ping` module for validating Windows connectivity

Refer to [`05-setup/winrm-setup.md`](ansible-cli/05-setup/winrm-setup.md) for the complete step-by-step setup.

---

## 🔮 Roadmap / Next Steps

- [ ] Add **Handlers** (restart services on config change)
- [ ] Add **Roles** using `ansible-galaxy init`
- [ ] Add **Jinja2 Templates** for dynamic config files
- [ ] Integrate **AWS Dynamic Inventory**
- [ ] Build **CI/CD pipeline** using Ansible + GitHub Actions
- [ ] Add **Molecule** for role testing

---

## 📚 Learning Resources

- 📖 [Official Ansible Docs](https://docs.ansible.com/)
- 📦 [Ansible Galaxy](https://galaxy.ansible.com/)
- 🔧 [Ansible Best Practices](https://docs.ansible.com/ansible/latest/tips_tricks/ansible_tips_tricks.html)
- 🛡️ [Ansible Vault Docs](https://docs.ansible.com/ansible/latest/vault_guide/index.html)

---

## 🤝 Connect

If you're on a DevOps learning journey, let's connect and grow together!

- 💼 [LinkedIn](https://www.linkedin.com/in/karthi-s2001/)
- 🐙 [GitHub](https://github.com/Karthi2305)

---

> *"Don't configure servers manually. Write a playbook once, run it everywhere."* 🚀
