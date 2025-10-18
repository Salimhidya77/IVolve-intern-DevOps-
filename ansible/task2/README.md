# Automated Web Server Configuration in Redhat Using Ansible Playbooks

## Objectives

- Automate web server installation and configuration using Ansible
- Install and enable **Nginx** on a managed node
- Deploy a custom `index.html` page
- Verify that the web server is running correctly
---
1. Playbook: `playbook.yml`
    ```yaml
    ---
    - name: Automated Web Server Configuration
      hosts: hosts
      become: true
      tasks:
        - name: Install nginx
          dnf:
            name: nginx
            state: present
            update_cache: true

        - name: Ensure Nginx is running
          service:
            name: nginx
            state: started
            enabled: true

        - name: Customize web page
          copy:
            content: |
              <html>
              <head>
                  <title>Welcome to Ansible Web Server</title>
              </head>
              <body>
                  <h1> Hello from Ansible!</h1>
                  <p>This web server is configured automatically using Ansible.</p>
              </body>
              </html>
            dest: /var/www/html/index.nginx-debian.html




2. **Create an Inventory File** `inventory.ini`:
   ```ini
   [hosts]
    mv1
    mv2
   

3. Run the Playbook:
   ```bash
   >> ansible-playbook playbook.yml 
   
   
4. **Verify Configuration**: 
   ```bash
    >> curl http://192.168.88.6
    >> curl http://192.168.88.7
   
