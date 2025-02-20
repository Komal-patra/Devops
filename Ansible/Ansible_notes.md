# Ansible Guide

## Overview

- **Ansible** is an **IT automation** and **configuration management** tool.
- It allows managing multiple servers **simultaneously**, automating tasks from **server creation to deployment**.
- Ansible is **free & open-source** (both free and paid versions exist).
- It is **platform-independent**.
- Developed in **2012** by **Michael DeHaan**; later acquired by **Red Hat**.
- **GUI** for Ansible: **Ansible Tower** (rarely used).

## Key Components

- **Playbooks**: YAML files defining tasks and configurations.
- **Modules**: Small programs performing tasks (start services, install software, etc.).
- **Inventory**: Defines where Ansible should execute tasks.

> **Comparison:**
> - **Jenkins** → Pipelines (Groovy)
> - **Ansible** → Playbooks (YAML)
> - **Jenkins** requires **Java**, Ansible requires **Python**.

## Ansible Architecture

- **Ansible Server**: Controls and communicates with worker nodes.
- **Worker Nodes**: Execute commands from the Ansible Server.
- **Playbook**: Contains automation scripts.
- **Inventory**: Stores information about worker nodes and groups.

---

## 🔧 Setup & Installation

### 1️⃣ Launch Amazon EC2 Instance (Amazon Linux - t2.micro)

### 2️⃣ Install Ansible
```sh
amazon-linux-extras install ansible2 -y
```

### 3️⃣ Install Python
```sh
yum install python3 python-pip python-devel -y
```

### 4️⃣ Verify Installation
```sh
ansible --version
```

---

## 🔥 Adhoc Commands

### 1️⃣ Ping the Server
```sh
ansible -m ping localhost
```

### 2️⃣ Run Linux Commands
```sh
ansible localhost -a "yum install -y git"
```

### 3️⃣ Install Software on All Machines
```sh
ansible all -a "yum install git -y"
```

### 4️⃣ Remove Installed Packages
```sh
ansible all -a "dnf remove httpd* git* maven* -y"
```

---

## 🔑 SSH Configuration

### 1️⃣ Generate SSH Key
```sh
ssh-keygen
```

### 2️⃣ Add Worker Node IP to Inventory
```sh
vim /etc/ansible/hosts
```

### 3️⃣ Copy SSH Key to Worker Nodes
```sh
ssh-copy-id root@private_ip
```

---

## 📦 Modules

### 1️⃣ Package Management
```sh
ansible all -m dnf -a "name=git state=present"
```

### 2️⃣ Service Management
```sh
ansible all -m service -a "name=httpd state=started"
```

### 3️⃣ User Management
```sh
ansible all -m user -a "name=komal state=present"
```

### 4️⃣ File Transfer
```sh
ansible all -m copy -a "src=transfer.txt dest=/home/ec2-user/"
```

---

## 📜 Playbooks (YAML)

### 1️⃣ Basic Playbook (Ping Test)
```yaml
---
- name: My First Playbook
  hosts: all
  tasks:
    - name: Test Connectivity
      ping:
```

```sh
ansible-playbook playbook1.yml
```

### 2️⃣ Install Apache
```yaml
---
- name: Installing Apache
  hosts: all
  become: yes
  tasks:
    - name: Install Apache
      dnf:
        name: httpd
        state: present
    - name: Start Apache
      service:
        name: httpd
        state: started
```

---

## 🚀 Advanced Topics

### 🔐 Ansible Vault (Encrypt Data)
```sh
ansible-vault create creds1.txt
```

```sh
ansible-vault decrypt creds1.txt
```

### 🕹 Handlers (Task Dependencies)
```yaml
---
- name: Handlers Playbook
  hosts: all
  become: yes
  tasks:
    - name: Install Apache
      dnf:
        name: httpd
        state: present
      notify: Start Apache
  handlers:
    - name: Start Apache
      service:
        name: httpd
        state: started
```

### ⚙️ Conditional Execution
```yaml
---
- name: Conditional Playbook
  hosts: all
  become: yes
  tasks:
    - name: Install Apache on RedHat
      dnf:
        name: httpd
        state: present
      when: ansible_os_family == "RedHat"
```

---

## 🎯 Conclusion
- Ansible simplifies **IT automation**.
- **No need for agents** on worker nodes.
- Uses **YAML-based playbooks** for automation.
- **Highly scalable & flexible**.

> **"Automate Everything with Ansible!"** 🚀
