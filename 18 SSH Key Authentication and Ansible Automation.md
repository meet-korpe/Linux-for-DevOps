# SSH Key Authentication and Ansible Automation

## 1. SSH Passwordless Key-Based Authentication

Passwordless authentication allows a client to connect to a server securely without entering a password each time. It relies on a pair of cryptographic keys: a **private key** (kept on the client) and a **public key** (shared with the server).

### Step-by-Step Setup

- **Set Hostnames:** For easier identification, set specific hostnames on your machines using `hostnamectl set-hostname [name]` (e.g., "client" and "server").
- **Generate Key Pair:** On the client machine, run:

```bash
ssh-keygen -t rsa
```

This creates a private key (`id_rsa`) and a public key (`id_rsa.pub`) in the `/root/.ssh/` directory.

- **Copy Public Key to Server:** Use the `ssh-copy-id` utility to transfer your public key to the remote server.
  - Command: `ssh-copy-id root@192.168.1.106` (or the server's specific IP).
- **Verify on Server:** The public key will be appended to the server's `/root/.ssh/authorized_keys` file. You can verify this by running `cat authorized_keys` on the server.
- **Test Connection:** You should now be able to log in without a password:
  - Command: `ssh root@10.10.10.11`

## 2. Automation with Ansible

Ansible is an automation tool that uses the SSH protocol to manage multiple remote servers simultaneously from a single "control node" (client).

### A. Installation and Initial Setup

- **Install EPEL and Ansible:** Ansible requires the "Extra Packages for Enterprise Linux" repository.

```bash
yum install epel-release -y
yum install ansible -y
```

- **Define Inventory:** Create a list of target servers (IP addresses) in the Ansible hosts file, often grouped under a header.
  - File: `/etc/ansible/hosts`
  - Example Content:

```text
[cartoon]
192.168.1.117
192.168.1.181
```

### B. Ad-hoc Commands

You can run quick tasks across all servers in a group using ad-hoc commands.

- **Ping Test:** Verifies connectivity to all servers in the "cartoon" group.
  - Command: `ansible -m ping cartoon`

### C. Ansible Playbooks (YAML)

Playbooks are used for more complex, repeatable automation tasks. They are written in YAML format.

**Example: Installing Nginx (test.yml)**:

```yaml
---
- name: Install Nginx on CentOS 7
  hosts: cartoon
  become: yes
  tasks:
    - name: Install Nginx
      yum:
        name: nginx
        state: present
    - name: Start and Enable Nginx
      service:
        name: nginx
        state: started
        enabled: yes
```

- **Running a Playbook:**
  - Command: `ansible-playbook test.yml`

