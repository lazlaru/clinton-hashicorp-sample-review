# Getting Started with Terraform
In this guide, you’ll install Terraform, create a basic configuration, and use it to deploy and destroy a Docker container.

---

## Prerequisites

Before you begin, make sure you have:

- Terraform **v1.0.0** or later installed  
- Docker installed and running  
- Command-line access to your local machine  

---

## Step 1: Install Terraform

Download Terraform for your operating system from [terraform.io/downloads](https://www.terraform.io/downloads).  
Unzip the file and move the executable into your system’s PATH.

---

## Step 2: Create a Working Directory

Create a directory for your Terraform configuration:

```bash
mkdir terraform-demo
cd terraform-demo
touch main.tf
```

---

## Step 3: Write the Terraform Configuration

Open `main.tf` and paste the following code:

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}

provider "docker" {
  host = "unix:///var/run/docker.sock"
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
```

---

## Step 4: Initialize Terraform

Run the following command to initialize your project:

```bash
terraform init
```

Terraform downloads the Docker provider and prepares the environment.  
Check for any errors before continuing.

---

## Step 5: Apply the Configuration

Use the following command to provision your Docker container:

```bash
terraform apply
```

Type `yes` when prompted to confirm.  
Terraform creates the container and displays a success message when finished.

---

## Step 6: Destroy the Infrastructure

When you’re done testing, remove the container:

```bash
terraform destroy
```

Confirm with `yes` when prompted.  
Terraform removes all resources it created.

---

## Next Steps

In this guide, you learned how to install Terraform and deploy a Docker container using a simple configuration.  

Next, explore:

- [Terraform State and Backends](https://developer.hashicorp.com/terraform/language/state)  
- [Using Variables and Outputs](https://developer.hashicorp.com/terraform/language/values/variables)  
- [Creating Multi-Resource Deployments](https://developer.hashicorp.com/terraform/tutorials)

---
