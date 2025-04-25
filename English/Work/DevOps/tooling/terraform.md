# 🌱 Terraform Basics for DevOps

---

## 📌 What is Terraform?

- **Terraform** is an open-source Infrastructure as Code ([[IaC]]) tool by HashiCorp.
- It allows you to **provision, manage, and version infrastructure** using a declarative configuration language called **HCL (HashiCorp Configuration Language)**.
- Supports **multiple cloud providers**: [[AWS]], [[Azure]], [[GCP]], and many others.

---

## 🧱 Core Concepts

### 🗂️ Providers
```hcl
provider "aws" {
  region = "us-east-1"
}
```
- Define the cloud service you're working with.

### 📦 Resources
```hcl
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```
- Represent the components you want to manage (VMs, storage, networks).

### 🪄 Variables
```hcl
variable "region" {
  default = "us-west-2"
}
```
- Parameters you can pass in to customize modules/configs.

### 🪝 Outputs
```hcl
output "instance_ip" {
  value = aws_instance.example.public_ip
}
```
- Used to return useful information from your configuration.

---

## 🔄 Workflow

1. **Write**: Define infrastructure in `.tf` files.
2. **Init**: `terraform init` — initialize working directory.
3. **Plan**: `terraform plan` — preview changes.
4. **Apply**: `terraform apply` — execute changes.
5. **Destroy**: `terraform destroy` — tear down resources.

---

## 📁 File Structure Example

```
project/
│
├── main.tf
├── variables.tf
├── outputs.tf
└── terraform.tfvars
```

---

## 🔧 Useful Commands

```bash
terraform init       # Initialize Terraform directory
terraform plan       # Show what will be done
terraform apply      # Apply changes
terraform destroy    # Tear down infrastructure
terraform validate   # Check for syntax errors
terraform fmt        # Format configuration files
terraform state list # List all managed resources
```

---

## 📚 Tips for DevOps

- Use **remote backends** (e.g. S3) for storing Terraform state in teams.
- Use **modules** to reuse configurations.
- Combine with **CI/CD pipelines** to automate provisioning.
- Use **workspaces** for environment separation (e.g. dev, staging, prod).
