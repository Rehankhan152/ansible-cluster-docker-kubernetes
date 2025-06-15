# 🔧 Ansible Cluster with Docker Containers & Kubernetes Pods

This project demonstrates how to **manually set up an Ansible cluster** using **Docker containers** and **Kubernetes pods (via Minikube)**, without using pre-built images. It includes an Ansible master and two managed nodes configured from scratch for automation testing.

---

## 📁 Project Structure

ansible-cluster/
├── docker/
│ ├── Dockerfile
│ ├── inventory
│ └── test.yml
├── kubernetes/
│ ├── ansible-master.yaml
│ ├── node1.yaml
│ ├── node2.yaml
├── README.md

yaml
Copy
Edit

---

## 🚀 Technologies Used

- Ansible
- Docker (Manual container creation)
- Kubernetes (via Minikube on Windows CMD)
- Rocky Linux 8 (base image)
- SSH for node communication
- YAML Playbooks for automation

---

## 📦 Setup in Docker

1. Build the custom image:
   ```bash
   docker build -t ansible-node .
Run containers manually:

bash
Copy
Edit
docker run -itd --name master ansible-node
docker run -itd --name node1 ansible-node
docker run -itd --name node2 ansible-node
Set up SSH keys between master and nodes, then run:

bash
Copy
Edit
ansible-playbook -i inventory test.yml
☸️ Setup in Kubernetes (Minikube)
Start Minikube:

bash
Copy
Edit
minikube start
Apply the pod YAMLs:

bash
Copy
Edit
kubectl apply -f ansible-master.yaml
kubectl apply -f node1.yaml
kubectl apply -f node2.yaml
SSH from the master to each node using Pod IPs, copy keys, then run the playbook.

📝 Sample Playbook
yaml
Copy
Edit
- name: Run test playbook on nodes
  hosts: nodes
  become: yes
  tasks:
    - name: Install Apache
      package:
        name: httpd
        state: present

💡 What I Learned
Setting up secure SSH communication from scratch

Deploying real apps in Kubernetes using Minikube locally

Writing and applying Ansible playbooks manually across nodes

Real DevOps automation without shortcuts

