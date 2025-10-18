# Structured Configuration Management with Ansible Roles

## Objectives

- Organize configuration management using Ansible **roles**
- Install and configure **Docker**, **kubectl**, and **Jenkins**
- Verify the installations on the managed node
---
## Master Playbook: `roles.yml`

```yaml
---
- name: Configure Docker K8s Jenkins
  hosts: production
  become: true
  roles:
    - docker
    - kubectl
    - jenkins
```    
## Roles Overview

### 1. Docker Role
- Checks if Docker is already installed  
- Installs dependencies and Docker Engine if missing  
- Starts and enables the Docker service  
- Verifies installation  
- **Tasks**: `roles/docker/tasks/main.yml`

### 2. kubectl Role
- Ensures `curl` is installed  
- Checks if `kubectl` is present  
- Downloads and installs the latest stable `kubectl` if missing  
- Verifies installation  
- **Tasks**: `roles/kubectl/tasks/main.yml`

