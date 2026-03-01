# Ansible Playbooks

This directory contains Ansible playbooks used to configure and manage
infrastructure components such as web servers and databases.

Playbooks define **what state the system should be in**, not how to do it.

---

## 📌 What is a Playbook?

- Written in YAML
- Contains one or more plays
- Each play targets a group of hosts
- Uses modules to perform tasks

---

## 📂 Playbooks in This Directory

| Playbook | Purpose |
|--------|--------|
| install_nginx.yml | Install and configure NGINX on web servers |
| install_mysql.yml | Install and configure MySQL on database servers |

---

## ▶️ How to Run Playbooks

```bash
ansible-playbook -i inventories/hosts.ini playbooks/install_nginx.yml
ansible-playbook -i inventories/hosts.ini playbooks/install_mysql.yml
```

---
If secrets are encrypted using Vault:
```bash
ansible-playbook -i inventories/hosts.ini playbooks/install_nginx.yml --ask-vault-pass
```

---
