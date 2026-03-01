# 🧩 Ansible Modules

Modules are the **core building blocks** of Ansible.

A module is a **small program** that performs a specific task.

---

## 🔹 What Modules Do

Modules can:
- Install packages
- Manage files
- Start/stop services
- Create cloud resources
- Configure networks

---

## 🔹 Examples of Common Modules

| Module | Purpose |
|-----|-------|
| apt | Install packages (Debian/Ubuntu) |
| yum | Install packages (RHEL/CentOS) |
| service | Manage services |
| copy | Copy files |
| template | Create config files |
| user | Manage users |

---

## 🔹 Example Usage

```yaml
- name: Install nginx
  apt:
    name: nginx
    state: present
```
---
