This file must be encrypted in real usage.
**Encrypt it**
```bash
ansible-vault encrypt group_vars/web/secrets.yml
```
---
🧩 How These Are Used in Playbooks

```yaml
vars_files:
  - ../group_vars/web/secrets.yml
```


