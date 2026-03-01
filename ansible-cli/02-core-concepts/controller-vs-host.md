# 🧠 Controller vs Managed Hosts in Ansible

Ansible follows a **controller–managed host architecture**.

---

## 🖥️ Controller Machine

The **controller** is the machine where:
- Ansible is installed
- Playbooks are written and executed
- Inventory files are stored

### Key points
- Only **Linux** can be an Ansible controller
- No agent is required on managed hosts
- Communicates using SSH (Linux) or WinRM (Windows)

### Examples
- Developer laptop
- CI/CD runner
- Bastion server

---

## 🧩 Managed Host (Target Node)

Managed hosts are the machines that Ansible configures.

### Supported OS
- Linux
- Windows
- Network devices (routers, switches)
- Cloud services (via APIs)

### Requirements
- Python (Linux)
- WinRM enabled (Windows)
- Network connectivity to controller

---

## 🔁 How They Work Together

1. Controller reads the inventory
2. Controller connects to hosts
3. Tasks are executed remotely
4. Results are returned to controller

---

## 🎯 Real-time Use Case

A DevOps engineer runs Ansible from a Jenkins server (controller) to configure:
- EC2 instances (Linux)
- Windows application servers

---

## 📌 Interview Tip

> “Ansible is agentless; only the controller needs Ansible installed.”
