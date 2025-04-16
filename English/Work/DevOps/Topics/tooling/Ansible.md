# 🛠️ Ansible Basics
**Last updated:** 2025-04-15  
**Tags:** #ansible #automation #devops #infrastructure #linux

---

## 🧠 What is Ansible?

Ansible is an open-source automation tool used for:
- Configuration management
- Application deployment
- Task automation
- Orchestration

It uses **YAML** for playbooks and communicates over **SSH** (no agent required).

---

## 📦 Key Concepts

### 🔸 Inventory
List of managed hosts (can be static or dynamic).
```ini
[web]
web01.example.com
web02.example.com

[db]
db01.example.com ansible_user=admin
```

### 🔸 Modules
Reusable scripts to perform tasks (e.g., `copy`, `yum`, `apt`, `user`).

### 🔸 Playbook
YAML file that defines tasks to be executed on hosts.

### 🔸 Task
Single automation action (e.g., install a package).

### 🔸 Role
Reusable collection of tasks, vars, templates, etc.

---

## 📋 Simple Playbook Example

```yaml
# file: install_nginx.yml
- name: Install and start Nginx on Ubuntu
  hosts: web
  become: true

  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
        update_cache: true

    - name: Start Nginx
      service:
        name: nginx
        state: started
        enabled: true
```

Run the playbook:
```bash
ansible-playbook -i inventory.ini install_nginx.yml
```

---

## 📁 Directory Structure Example

```
ansible/
├── inventory.ini
├── install_nginx.yml
└── roles/
    └── nginx/
        ├── tasks/
        │   └── main.yml
        ├── templates/
        └── vars/
```

---

## 📚 Useful Links

- 🔗 [Ansible Docs](https://docs.ansible.com/)
- 🔗 [Ansible Galaxy](https://galaxy.ansible.com/)
- 🔗 [Inventory Guide](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)

---

## ✅ Good Practices

- Use roles for reusability.
- Keep inventory outside the repo for sensitive data.
- Use `ansible-vault` for secrets.
- Test locally using `vagrant` or Docker.

---
