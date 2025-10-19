# ansible-vault encrypt mysql_vault.yaml


## Objectives

- Automate web server installation and configuration using Ansible
- Install and enable **Nginx** on a managed node
- Deploy a custom `index.html` page
- Verify that the web server is running correctly
---
1. **Create a vault**:
   ```bash
   ansible-vault create mysql_vault.yaml

---   
2. Playbook: `mysql-playbook.yaml`
    ```yaml
   # Ansible Playbook: Install and Configure MySQL

This Ansible playbook automates the installation and configuration of **MySQL** on a production server. It also creates a database and a dedicated user with full privileges.

---

## Prerequisites

- Ansible installed on your control machine
- Managed node accessible via SSH
- `vars/mysql_vault.yml` file containing encrypted passwords:

```yaml
mysql_root_password: your_root_password
ivolve_user_password: your_ivolve_user_password

---
3. **Create an Inventory File** `inventory.ini`:
   ```ini
   [hosts]
   mv1
   mv2
---   
4. **Run** the Playbook:
   ```bash
   ansible-playbook -i inventory.ini mysql-playbook.yaml --ask-become-pass --ask-vault-pass
   
---  

   
