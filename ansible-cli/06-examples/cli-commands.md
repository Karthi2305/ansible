# Common Ansible Commands

This document covers commonly used Ansible commands along with
their purpose, when to use them, and real-world use cases.

---
```bash
ansible --version
```
Displays the installed Ansible version and configuration details.

---
```bash
ansible all -m ping
```
Checks connectivity between the controller and all managed hosts.

**Real-world use case**

Used to validate that all servers are reachable before a production deployment.
⚠️ This is not a network ping; it verifies Ansible connectivity.

---

```bash
ansible <group> -m setup
```

Collects system facts (OS, IP, CPU, memory, etc.) from hosts.

**Real-world use case**

Used to validate OS versions before applying OS-specific tasks.
---

```bash
ansible <group> -m shell -a "<command>"
```
Runs a shell command on target hosts.

**When to use**
- For quick troubleshooting
- For commands without a native module

**Real-world use case**

Checking disk usage across all servers during an incident.
---

```bash
ansible <group> -m command -a "<command>"
```
Executes a command without shell interpretation.

**When to use**
- Running safe, predictable commands
- Avoiding shell-related risks

**Real-world use case**

Running uptime or ls across servers to check load or files.
---

```bash
ansible-playbook playbook.yml
```

Executes an Ansible playbook.

**When to use**
- Running automation workflows
- Applying configuration changes

**Real-world use case**

Used to deploy applications or configure servers consistently.
---
```bash
ansible-playbook -i inventories/hosts.ini playbook.yml
```
Runs a playbook with a specific inventory file.

**When to use**
- Managing multiple environments
- Using custom inventories

**Real-world use case**

Running the same playbook against dev, QA, and prod inventories.
---
```bash
ansible-playbook playbook.yml --check
```

Performs a dry run without making actual changes.

**Real-world use case**

Used in CI/CD pipelines to validate changes safely.
---
```bash
ansible-playbook playbook.yml --diff
```
Shows configuration differences before applying changes.

**When to use**
- Auditing changes
- Reviewing configuration updates
---
```bash
ansible-playbook playbook.yml --limit <host/group>
```
Limits execution to specific hosts or groups.

**When to use**
- Partial deployments
- Debugging specific hosts

**Real-world use case**
Deploying a fix to a single node instead of the entire cluster.
---
```bash
ansible-vault create secrets.yml
```
Creates an encrypted file for storing secrets.

**When to use**

- Storing passwords, tokens, credentials

**Real-world use case**
Used to store database credentials securely in Git repositories.

```bash
ansible-vault edit secrets.yml
```
Edits an encrypted Vault file.

**When to use**
- Updating secrets
- Rotating passwords

```bash
ansible-vault view secrets.yml
```
Displays encrypted content in read-only mode.

---
```bash
ansible-inventory -i inventories/hosts.ini --list
```

Displays the resolved inventory structure.

**When to use**

- Debugging inventory issues
- Verifying group variables
---
```bash
ansible-doc <module>
```
Displays documentation for an Ansible module.
**When to use**
- Learning module options
- Writing accurate playbooks

**Real-world use case**
Used daily while developing new automation tasks.
---
```bash
ansible-galaxy install <role>
```
Downloads roles from Ansible Galaxy.

**When to use**

- Reusing community roles
- Accelerating automation development

**Real-world use case**
Using a hardened NGINX role instead of writing from scratch.
---
```bash
ansible-lint playbook.yml
```
Checks playbooks for best practices and syntax issues.

**When to use**
- Before committing code
- In CI pipelines

---
