# 🔐 Secrets Management – Best Practices in Ansible

Handling secrets securely is **critical** in production automation.

Ansible provides **Ansible Vault** to manage sensitive data such as:
- Passwords
- API keys
- SSH credentials
- Tokens

---

## ❌ What NOT to Do

Never:
- Store passwords in plain text
- Commit credentials to GitHub
- Hardcode secrets inside playbooks
- Share vault passwords in chat or email

Bad example:
```yaml
db_password: admin123
```

---


