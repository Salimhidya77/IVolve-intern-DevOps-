# ansible-vault encrypt vault.yml


## Objectives

- Automate web server installation and configuration using Ansible
- Install and enable **Nginx** on a managed node
- Deploy a custom `index.html` page
- Verify that the web server is running correctly
---
1. **Create a vault**:
   ```bash
   ansible-vault create mysql_vault.yml

---   
2. Playbook: `mysql-playbook.yaml`
    ```yaml
   --
- name: Install and configure MySQL
  hosts: production
  become: true
  vars_files:
    - vars/mysql_vault.yml

  tasks:
    - name: Install MySQL
      ansible.builtin.package:
        name: mysql-server
        state: present

    - name: Ensure MySQL service is running
      ansible.builtin.service:
        name: mysqld
        state: started
        enabled: true

    - name: Create iVolve database
      community.mysql.mysql_db:
        name: iVolve
        state: present
        login_user: root
        login_password: "{{ mysql_root_password }}"

    - name: Create user with privileges
      community.mysql.mysql_user:
        name: ivolve_user
        password: "{{ ivolve_user_password }}"
        priv: 'iVolve.*:ALL'
        state: present
        login_user: root
        login_password: "{{ mysql_root_password }}"

    - name: Validate connection and list databases
      ansible.builtin.shell: >
        mysql -u ivolve_user -p{{ ivolve_user_password }} -e "SHOW DATABASES;"
      register: db_check

    - name: Print validation output
      ansible.builtin.debug:
        var: db_check.stdout_lines


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

   
