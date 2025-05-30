# terraform-docker-task-4
Infrastructure as Code (IaC) with Terraform


## 🎯 Objective

Provision a local Docker container running the NGINX web server using Terraform to understand Infrastructure as Code (IaC) principles.

---

## 🛠️ Tools Used

- Terraform  
- Docker  
- Amazon Linux 2 (EC2 Instance)

---

## 📁 Deliverables

### 1. main.tf

```hcl
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.20"
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
  name  = "nginx_container"
  image = docker_image.nginx.name

  ports {
    internal = 80
    external = 8080
  }
}


# 2. Execution Logs# terraform init
Initializing the backend...
Initializing provider plugins...
- Finding kreuzwerker/docker versions matching "~> 2.20"...
- Installing kreuzwerker/docker v2.20.0...
Terraform has been successfully initialized!

# terraform plan
Plan: 2 to add, 0 to change, 0 to destroy.

# terraform apply -auto-approve
docker_image.nginx: Creating...
docker_image.nginx: Creation complete
docker_container.nginx: Creating...
docker_container.nginx: Creation complete
Apply complete! Resources: 2 added.

# docker ps
CONTAINER ID   IMAGE          PORTS                  NAMES
xxxxxxx        nginx:latest   0.0.0.0:8080->80/tcp   nginx_container

# curl http://localhost:8080
<!DOCTYPE html>
<html>
<head><title>Welcome to nginx!</title></head>
...

# terraform state list
docker_container.nginx
docker_image.nginx

# terraform destroy -auto-approve
Destroy complete! Resources: 2 destroyed.

 **Outcome**
Successfully provisioned a Docker container running NGINX using Terraform.

Learned how to use Terraform Docker provider.

Understood IaC concepts of automation and repeatability.

Verified the webserver was accessible at http://localhost:8080.

