# Ansible System Hardening Playbook 🛡️

An idempotent Ansible playbook designed to automate baseline security hardening for newly provisioned Linux servers. Supports both **RedHat (RHEL/Fedora/Rocky/Alma)** and **Debian (Ubuntu/Debian)** distribution families.

---

## ⚡ Key Features

* **Multi-OS Support:** Uses Ansible facts (`ansible_os_family`) to dynamically execute OS-specific tasks (`apt` vs `package`, `ufw` vs `firewalld`).
* **Idempotency:** Tasks only execute if the target system state differs from the desired configuration.
* **Service Minimisation:** Stops and disables unused or insecure daemons (`telnet`, `vsftpd`, `cups`, etc.).
* **SSH Hardening & Safety:**
  * Creates timestamped backups of `/etc/ssh/sshd_config` prior to editing.
  * Disables `PermitRootLogin`, `PasswordAuthentication`, and `PermitEmptyPasswords`.
  * **Syntax Validation:** Uses `sshd -t -f %s` to validate config edits before writing them to disk to prevent lockouts.
  * **Handlers:** Restarts SSH *only* when configuration changes occur.
* **Automated Firewall Management:**
  * **Debian:** Configures `ufw` (default deny incoming, allows SSH).
  * **RedHat:** Configures `firewalld` (sets default zone to `drop`, enables SSH service).

---

## 📋 Requirements

* **Ansible Core:** `2.12+` installed on the control node.
* **Collections Required:**
  ```bash
  ansible-galaxy collection install ansible.posix community.general
  ```

## 🚀 Quick Start

### 1. Clone the repository
```bash
git clone https://github.com/SudoShea/ansible-system-hardening.git
cd ansible-system-hardening
```
### 2. Configure inventory

Edit inventory.ini to define your target hosts:
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
