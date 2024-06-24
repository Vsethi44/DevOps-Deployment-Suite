# DevOps-Symphony

### Overview
This project integrates multiple DevOps tools and practices to demonstrate a full lifecycle of infrastructure provisioning, configuration management, containerization, and orchestration. The goal is to provide a hands-on example of how to effectively use these tools together in a real-world scenario. The project is divided into three main tasks, each focusing on different aspects of the DevOps pipeline.

### Task 1: Terraform

**Objective:** 
To launch an Ubuntu EC2 instance to be used as a Terraform workstation. From this workstation, use Terraform to launch a Red Hat Linux EC2 instance for Ansible automation tasks.

**Detailed Steps:**
1. **Setup Terraform Workstation:**
   - Launch an Ubuntu EC2 instance (t2.micro).
   - SSH into the instance and update the hostname.
   - Install necessary packages (`wget`, `unzip`, `python3-pip`).
2. **Install Terraform:**
   - Download and install Terraform.
   - Move Terraform executable to `/usr/local/bin` and verify the installation.
3. **Configure AWS CLI:**
   - Install AWS CLI using `pip3`.
   - Configure AWS CLI with access key and region information.
   - Verify the configuration by listing S3 buckets.
4. **Generate SSH Keys:**
   - Use `ssh-keygen` to create a key pair for SSH access.
   - Save the private key securely and use the public key in Terraform scripts.
5. **Write Terraform Scripts:**
   - Create `instance.tf` for defining the Red Hat Linux EC2 instance.
   - Create `sshkey.tf` to manage the SSH key pair in AWS.
6. **Execute Terraform Commands:**
   - Initialize Terraform with `terraform init`.
   - Format and validate the configuration with `terraform fmt` and `terraform validate`.
   - Generate and apply the execution plan with `terraform plan` and `terraform apply`.
7. **Access Ansible Workstation:**
   - SSH into the newly created Red Hat Linux instance using the generated key.

### Task 2: Ansible

**Objective:**
To install Ansible on the Red Hat Linux EC2 instance and configure it as an HTTP server.

**Detailed Steps:**
1. **Install Ansible:**
   - SSH into the Red Hat Linux EC2 instance.
   - Update the package repository and install Python.
   - Install AWS CLI, Boto, Boto3, and Ansible using `pip3`.
2. **Configure Ansible Inventory:**
   - Create an inventory file and add `localhost` with `ansible_connection=local`.
3. **Create Ansible Playbook:**
   - Write a playbook (`install_httpd.yml`) to install and configure the Apache HTTP server.
   - The playbook includes tasks to install `httpd`, start the service, and create a custom `index.html`.
4. **Run the Playbook:**
   - Execute the playbook using `ansible-playbook install_httpd.yml`.
   - Verify the installation by accessing the custom webpage through the instance's public IP.

### Task 3: Docker & Kubernetes

**Objective:**
To build a Docker image for a Python API, push it to Docker Hub, and deploy it on a Kubernetes cluster.

**Detailed Steps:**
1. **Prepare Docker Environment:**
   - Create a directory structure (`dockerdir`) and navigate to it.
   - Create a `Dockerfile` and `requirements.txt` file for the Python Flask API.
2. **Write Dockerfile:**
   - Define the base image, maintainer, and install necessary packages.
   - Copy application files and set the working directory.
   - Install Python dependencies and define the command to run the application.
3. **Build and Push Docker Image:**
   - Build the Docker image with `docker build -t <dockerhub-username>/mydocker-image:v1 .`.
   - Push the image to Docker Hub using `docker push <dockerhub-username>/mydocker-image:v1`.
4. **Create Kubernetes Deployment:**
   - Write a Kubernetes Pod configuration (`mypod.yml`) to deploy the Docker image.
   - Apply the Pod configuration using `kubectl apply -f mypod.yml`.
   - Expose the Pod externally using a NodePort service.
5. **Verify Deployment:**
   - List Kubernetes services and access the application through the exposed NodePort.

### Key Features
- **Infrastructure as Code:** Automates infrastructure provisioning with Terraform, ensuring repeatability and version control.
- **Configuration Management:** Uses Ansible for automated configuration and software installation, promoting consistency across environments.
- **Containerization:** Encapsulates the application and its dependencies in a Docker container, simplifying deployment and scaling.
- **Orchestration:** Manages containerized applications with Kubernetes, enabling efficient scaling, deployment, and management.

### Repository Structure
- **terraform/**
  - `instance.tf`: Terraform configuration for creating EC2 instances.
  - `sshkey.tf`: Terraform configuration for managing SSH keys.
- **ansible/**
  - `install_httpd.yml`: Ansible playbook for setting up an HTTP server.
  - `inventory.inv`: Ansible inventory file.
- **docker/**
  - `Dockerfile`: Dockerfile for building the Python API image.
  - `requirements.txt`: Dependencies for the Python API.
  - `code/`: Directory containing the Python API code.
- **kubernetes/**
  - `mypod.yml`: Kubernetes Pod configuration for deploying the Docker image.

### Conclusion
This project demonstrates a complete DevOps pipeline from infrastructure provisioning to application deployment using industry-standard tools. It showcases how Terraform, Ansible, Docker, and Kubernetes can be effectively used together to create, configure, deploy, and manage applications in a cloud environment.

