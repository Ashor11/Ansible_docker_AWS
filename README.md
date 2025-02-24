🚀 Deploying Node.js & Flask Apps Using Docker Compose on AWS EC2 & On-Prem (VMware)
📖 Overview

This project automates the deployment of Dockerized Node.js and Flask applications on AWS EC2 and On-Prem (VMware Workstation) using Ansible and Docker Compose.
🛠 Tech Stack

    Ansible - Automation
    Docker & Docker Compose - Containerization
    AWS EC2 - Cloud hosting
    VMware Workstation - On-Prem virtual machines
    Flask & Node.js - Backend apps
    Git - Version control
    Docker Hub - Container registry
    AWS IAM - Authentication

📌 Prerequisites

1️⃣ Install Ansible
sudo apt update && sudo apt install -y ansible


2️⃣ Install VMware Workstation (On-Prem Only)
Download from VMware and create a Linux VM.

3️⃣ Configure AWS CLI
aws configure

4️⃣ Update EC2 Security Group
Allow ports 22, 3000, and 8000 for SSH & app access through HTTP.

📜 File Structure

|-- playbook.yml         # Ansible automation
|-- docker-compose.yml   # Defines containers
|-- inventory            # Hosts configuration
|-- ansible.cfg          # Ansible settings


🚀 steps to deploy

1️⃣ Provisioning the Servers

    I used AWS EC2 to host my cloud deployment.
    I provisioned an On-Prem virtual machine using VMware Workstation to simulate a local server.

2️⃣ Configuring AWS IAM & CLI Authentication

    I authenticated my AWS environment using:

    aws configure

    Set up an EC2 instance with proper security group rules to allow SSH and app traffic (ports 22, 3000, and 8000).

3️⃣ Installing and Setting Up Dependencies

    I used Ansible to automate the installation of required packages (Docker, Git, Python) on both EC2 and the On-Prem VM.
    The Ansible playbook installs and configures Docker and Docker Compose on both environments.

4️⃣ Cloning the Application Code from GitHub

    I cloned my Node.js app repository from GitHub onto both servers using Ansible.

5️⃣ Building and Running the Node.js App in Docker

    Built a custom Docker image from my Node.js application source code.
    Created a Docker Compose file to define the services.

6️⃣ Deploying a Flask App from Docker Hub

    Instead of building a Flask image from scratch, I pulled a pre-built Flask image (ashor11/flask_as:v1) from Docker Hub for faster deployment.

7️⃣ Running Docker Containers with Docker Compose

    Created and deployed the Node.js & Flask applications using Docker Compose.
    Ensured containers were running in detached mode (-d) for background execution.

8️⃣ Testing and Verifying Deployment

    Checked running containers using:

docker ps
📌 Deployment Steps
1️⃣ Clone the Repo

git clone https://github.com/yourusername/your-repo.git
cd your-repo

2️⃣ Configure Inventory (inventory)

Update with EC2 public IP & On-Prem VM IP.

[ec2]
ec2-instance ansible_host=34.241.237.12 ansible_user=ec2-user ansible_private_key_file=/home/ansible/.ssh/demo_docker.pem

[onprem]
onprem-vm ansible_host=192.168.1.100 ansible_user=vmuser ansible_ssh_private_key_file=/home/ansible/.ssh/onprem.pem

3️⃣ Run Ansible Playbook

ansible-playbook -i inventory playbook.yml

4️⃣ Verify Deployment

docker ps
curl http://your-ec2-public-ip:8000  # Flask (EC2)
curl http://your-ec2-public-ip:3000  # Node.js (EC2)
curl http://private_ip:8000       # Flask (On-Prem)
curl http://privaet_ip:3000       # Node.js (On-Prem)
