# Ansible Inventory (hosts.ini)

The Ansible inventory defines **which hosts are managed** and **how Ansible connects to them**.

This file is equivalent to **Terraform provider + target configuration**.

---

## 📌 What is an Inventory?

- Inventory is a list of managed hosts
- Hosts can be grouped by role (web, db, windows)
- Variables can be defined per host or per group

---

## 📂 Inventory File Used


---

🧪 Validate Inventory
```bash
ansible-inventory -i inventories/hosts.ini --list
```
---
