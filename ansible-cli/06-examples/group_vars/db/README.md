This file must be encrypted in real usage.
**Encrypt it**
```bash
ansible-vault encrypt group_vars/db/secrets.yml
```
---

🧩 How These Are Used in Playbooks

Example from your playbook:
```yaml
vars_files:
  - ../group_vars/db/secrets.yml
```
---
