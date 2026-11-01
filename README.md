# Portfolio-Assignment
The objective of this task is to automate the deployment of a multi-page static portfolio website on an Ubuntu Linux server using Ansible.
# Portfolio Website Deployment Using Ansible

## Project Overview

This project demonstrates the automated deployment of a multi-page static portfolio website on an Ubuntu Linux server using **Ansible**.

Ansible is used to automate server configuration, Nginx installation, service management, and website file deployment. The project follows a role-based directory structure to make the deployment process organized, reusable, and easy to maintain.

The website is built using HTML5 and CSS3 and is hosted using the Nginx web server.

## Objectives

- Configure an Ansible project using a role-based directory structure.
- Automate Nginx installation on a remote Ubuntu server.
- Manage Nginx service status and enable it at system startup.
- Deploy multiple HTML and CSS files using Ansible.
- Use Ansible loops to simplify repetitive deployment tasks.
- Host a static portfolio website on an AWS EC2 instance.

## Technologies Used

| Technology | Purpose |
|---|---|
| Ubuntu Linux | Operating system |
| Ansible | Configuration management and automation |
| Nginx | Web server |
| HTML5 | Website structure |
| CSS3 | Website styling |
| AWS EC2 | Cloud virtual machines |
| Git | Version control |
| GitHub | Source code repository |
| MobaXterm | Remote SSH connection |

## Project Architecture

The project uses two EC2 instances:

1. **Ansible Control Node:** Executes Ansible commands and manages the deployment.
2. **Target Node:** Receives the website files and hosts the website using Nginx.

Ansible communicates with the target node through SSH.

## Project Directory Structure

```text
portfolio-project/
│
├── inventory.ini
├── site.yml
├── README.md
├── Screen-Shots/
│
└── roles/
    └── portfolio/
        │
        ├── tasks/
        │   └── main.yml
        │
        └── files/
            ├── index.html
            ├── about.html
            ├── projects.html
            ├── contact.html
            └── style.css
```

## Ansible Configuration

### 1. Inventory File

The `inventory.ini` file contains the details of the target server.

```ini
[webservers]
targetnode1 ansible_host=<TARGET_PRIVATE_IP> ansible_user=ubuntu
```

Replace `<TARGET_PRIVATE_IP>` with the actual private IP address of the target EC2 instance.

### 2. Main Playbook

The `site.yml` file executes the portfolio role on the target node.

```yaml
---
- name: Deploy portfolio website
  hosts: webservers
  become: yes
  roles:
    - portfolio
```

### 3. Ansible Role Tasks

The `roles/portfolio/tasks/main.yml` file contains the tasks required for deployment.

The tasks include:

- Updating the APT package cache.
- Installing Nginx.
- Starting and enabling the Nginx service.
- Copying the website files to the target server.

The Ansible `copy` module is used to transfer website files from the role's `files` directory to `/var/www/html/`.

An Ansible loop is used to deploy all five website files.

## Website Pages

The portfolio website consists of four HTML pages and one shared CSS stylesheet.

| File | Description |
|---|---|
| `index.html` | Home page |
| `about.html` | About page |
| `projects.html` | Projects page |
| `contact.html` | Contact page |
| `style.css` | Common styling for all pages |

The navigation menu allows users to move between all four pages.

## Deployment Procedure

### Step 1: Verify Ansible Connectivity

Run the following command from the Ansible control node:

```bash
ansible webservers -i inventory.ini -m ping
```

### Step 2: Execute the Playbook

Run the following command to start the automated deployment:

```bash
ansible-playbook -i inventory.ini site.yml
```

### Step 3: Verify Nginx Service

Connect to the target node and execute:

```bash
sudo systemctl status nginx
```

### Step 4: Verify Website Deployment

Check whether the website files are available:

```bash
ls -l /var/www/html/
```

### Step 5: Access the Website

Open a web browser and enter the target EC2 instance's public IP address:

```text
http://<TARGET_PUBLIC_IP>
```

The deployed portfolio website should now be accessible.

## Screenshots

The `Screen-Shots/` directory contains screenshots documenting the project setup and deployment process.

These screenshots demonstrate the Ansible configuration, deployment execution, and website accessibility.

## Key Learning Outcomes

- Understanding Ansible architecture and role-based project organization.
- Managing remote Linux servers using SSH.
- Automating package installation and service management.
- Using Ansible modules such as `apt`, `service`, and `copy`.
- Understanding loops in Ansible.
- Deploying static websites on Linux servers using Nginx.
- Working with AWS EC2 instances and GitHub.

## Conclusion

This project demonstrates how Ansible can simplify and automate static website deployment on Linux servers. By using an Ansible role, the deployment process becomes organized, repeatable, and easier to maintain.

The final outcome is a multi-page static portfolio website hosted on an Ubuntu EC2 instance using Nginx, with the deployment process automated through Ansible.

---

**Project Type:** Individual Assignment  
**Application:** Static Portfolio Website  
**Automation Tool:** Ansible  
**Web Server:** Nginx  
**Operating System:** Ubuntu Linux
