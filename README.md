# Automated Web Server Deployment using Ansible

![Ansible](https://img.shields.io/badge/Ansible-Automation-EE0000?logo=ansible&logoColor=white)
![Red Hat](https://img.shields.io/badge/OS-Red%20Hat%20Enterprise%20Linux-EE0000?logo=redhat&logoColor=white)
![Apache](https://img.shields.io/badge/Web%20Server-Apache-D22128?logo=apache&logoColor=white)
![YAML](https://img.shields.io/badge/Config-YAML-CB171E?logo=yaml&logoColor=white)

## 📌 Project Overview

This project demonstrates how to automate web server deployment and configuration on Red Hat Enterprise Linux (RHEL) using **Ansible**.

Instead of manually configuring each server, Ansible automates the entire deployment process through a single YAML Playbook.

The project is designed to simplify Linux system administration, reduce manual configuration, and ensure consistent deployment across multiple servers.

## 🎯 Project Objectives

- Automate Apache HTTP Server installation.
- Manage Apache service and enable it at system boot.
- Configure FirewallD to allow HTTP traffic.
- Deploy a custom HTML website.
- Manage SELinux security settings.
- Automate server configuration using Ansible Playbooks.

## 🛠️ Technologies & Tools

| Technology | Purpose |
|---|---|
| Ansible | Configuration Management & Automation |
| Red Hat Enterprise Linux | Managed Server Operating System |
| Apache HTTP Server | Web Server |
| FirewallD | Firewall Management |
| SELinux | Security Management |
| YAML | Playbook Configuration |
| SSH | Remote Server Connectivity |
| Git & GitHub | Version Control |

## 🏗️ Project Architecture

The project follows an Ansible Controller / Managed Node architecture.

- **Ansible Controller:** Executes Ansible Playbooks and manages remote servers.
- **Managed Node:** RHEL server configured automatically by Ansible.
- **SSH:** Provides secure communication between the Controller and Managed Node.

## 📂 Project Structure

```text
ansible-automated-web-server-deployment/
│
├── inventory
│
├── site.yml
│
├── files/
│   └── index.html
│
└── README.md
```

## ⚙️ Prerequisites

Before running this project, make sure you have:

- Ansible installed on the Controller machine.
- A RHEL-based Managed Node.
- SSH connectivity between Controller and Managed Node.
- Sudo privileges on the Managed Node.
- Python installed on the Managed Node.
- FirewallD and SELinux support on the target system.

Install the required Ansible Collection:

```bash
ansible-galaxy collection install ansible.posix
```

Install FirewallD dependencies on the Managed Node:

```bash
sudo dnf install firewalld python3-firewall -y
```

Start and enable FirewallD:

```bash
sudo systemctl enable --now firewalld
```

## 🚀 Deployment Steps

### 1. Configure Inventory

Add your target server IP address to the inventory file:

```ini
[webservers]
192.168.1.100
```

Replace the example IP with your actual RHEL server IP.

### 2. Test Connectivity

Verify communication between Ansible Controller and Managed Node:

```bash
ansible webservers -i inventory -m ping
```

### 3. Create the Website

Create a custom HTML page inside the `files/` directory.

The website will be deployed to:

```text
/var/www/html/index.html
```

### 4. Run the Playbook

Check the Playbook syntax:

```bash
ansible-playbook -i inventory site.yml --syntax-check
```

Run the deployment:

```bash
ansible-playbook -i inventory site.yml
```

## 🔧 Automated Tasks

The main Ansible Playbook (`site.yml`) performs the following operations:

| Task | Description |
|---|---|
| Install Apache | Installs the `httpd` package using DNF |
| Start Apache | Starts the Apache service |
| Enable Apache | Configures Apache to start automatically at boot |
| Install FirewallD | Installs FirewallD and Python dependencies |
| Start FirewallD | Enables and starts the firewall service |
| Configure Firewall | Allows incoming HTTP traffic on port 80 |
| Deploy Website | Copies the custom HTML page to the Apache document root |
| Configure SELinux | Sets SELinux to enforcing mode |

## ✅ Verification

After successful deployment, verify the configuration on the Managed Node.

**Check Apache Status:**

```bash
sudo systemctl status httpd
```

**Check Firewall Rules:**

```bash
sudo firewall-cmd --list-services
```

**Check SELinux Status:**

```bash
getenforce
```

Expected output:

```text
Enforcing
```

**Test the Website Locally:**

```bash
curl http://localhost
```

**Access the Website from a Browser:**

```text
http://SERVER-IP
```

Replace `SERVER-IP` with the actual IP address of your Managed Node.

## 📚 Key Ansible Concepts Practiced

- Inventory Files and Host Groups.
- YAML Fundamentals.
- Ansible Playbooks and Tasks.
- Privilege Escalation (`become`).
- Ansible Modules (`dnf`, `service`, `copy`, `firewalld`, `selinux`).
- Configuration Management.
- Infrastructure Automation.
- Linux Server Administration.

## 💡 Future Improvements

- Implement Ansible Roles for better project organization.
- Use Jinja2 Templates for dynamic website configuration.
- Configure HTTPS using SSL/TLS.
- Add automated deployment for multiple web servers.
- Implement Ansible Vault for sensitive credentials.
- Add error handling and validation tasks.
- Integrate the project with a CI/CD pipeline.

## 👨‍💻 Author

**Linux System Administration & Ansible Automation Project**

Developed as a practical project to demonstrate Linux administration, configuration management, and infrastructure automation using Ansible.

---

⭐ If you find this project useful, feel free to explore the repository and contribute.
