# Ansible System Hardening Playbook 🛡️

![Ansible Linting](https://github.com/SudoShea/ansible-system-hardening/actions/workflows/lint.yml/badge.svg)

An idempotent Ansible playbook designed to automate baseline security hardening for newly provisioned Linux servers. Supports both **RedHat (RHEL/Fedora/Rocky/Alma)** and **Debian (Ubuntu/Debian)** distribution families.

---

## ⚡ Key Features

* **Cross-Family Compatibility:** Dynamically detects OS family to manage `firewalld` (RHEL) or `ufw` (Debian).
* **Automated CI/CD Quality Control:** Fully validated on every push via `ansible-lint` and GitHub Actions workflows.
* **Insecure Service Removal:** Stops and disables legacy services (`telnet`, `vsftpd`, `cups`, `rpcbind`, `avahi-daemon`).
* **SSH Hardening:** Enforces `PasswordAuthentication no` and `PermitRootLogin no`.
* **Kernel & Core Dumps:** Restricts core dump creation via `limits.conf` and `sysctl`.

---

## 📋 Requirements

* **Ansible Core:** `2.15+` installed on the control node.
* **Dependencies:** Install required collections via `requirements.yml`:
  ```bash
  ansible-galaxy collection install -r requirements.yml
  ```

## 🚀 Quick Start

### 1. Clone the repository & install dependencies
```bash
git clone https://github.com/SudoShea/ansible-system-hardening.git
cd ansible-system-hardening
ansible-galaxy collection install -r requirements.yml
```
### 2. Configure inventory

Edit `inventory.ini` to define your target hosts:
```bash
[servers]
192.168.1.50 ansible_user=admin
```
### 3. Dry-Run Check (Recommended)

Test the execution against your target hosts without applying any changes:
```bash
ansible-playbook -i inventory.ini site.yml --check
```
### 4. Apply Hardening

Execute the playbook across all inventory targets:
```bash
ansible-playbook -i inventory.ini site.yml --ask-become-pass
```
---
## 📄 License
Distributed under the MIT License. See `LICENSE` for details.
