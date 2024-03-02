# Terraform Cheat Sheet

Terraform is an Infrastructure as Code (IaC) tool used for building, changing, and versioning infrastructure safely and efficiently. This cheat sheet provides a quick reference to common Terraform commands and configurations.

## Table of Contents

1. [Terraform Basics](#terraform-basics)
2. [Terraform Commands](#terraform-commands)
3. [File Structure](#file-structure)
4. [Resource Configuration](#resource-configuration)
5. [Variables](#variables)
6. [Outputs](#outputs)
7. [Modules](#modules)
8. [Backend Configuration](#backend-configuration)
9. [Providers](#providers)

## Terraform Basics

- **Infrastructure as Code (IaC):** Terraform allows you to define your infrastructure using a high-level configuration language.
- **Execution Plan:** Terraform generates an execution plan. This shows what Terraform will do when you call `terraform apply`.
- **Resource Management:** Terraform allows for the creation, modification, and destruction of infrastructure resources.

## Terraform Commands

- `terraform init` - Initialize a Terraform working directory.
- `terraform plan` - Generate and show an execution plan.
- `terraform apply` - Apply the changes required to reach the desired state of the configuration.
- `terraform destroy` - Destroy the Terraform-managed infrastructure.
- `terraform validate` - Validates the Terraform files for syntax.
- `terraform fmt` - Rewrites Terraform configuration files to a canonical format and style.

## File Structure

- `main.tf` - The primary entry point for Terraform configuration.
- `variables.tf` - Defines variables used within the configuration.
- `outputs.tf` - Defines output values that can be useful for understanding the resources created.
- `provider.tf` - Specifies and configures the providers Terraform will use.

## Resource Configuration

```hcl
resource "aws_instance" "example" {
  ami           = "ami-abc123"
  instance_type = "t2.micro"
}
```

- Define a resource with `resource` followed by the resource type and a name.
- Inside the block, configure the resource with required and optional arguments.

## Variables

```hcl
variable "instance_type" {
  description = "The instance type of the EC2 instance"
  type        = string
  default     = "t2.micro"
}
```

- Declare variables in `variables.tf` and reference them using `var.<variable_name>`.

## Outputs

```hcl
output "instance_ip_addr" {
  value = aws_instance.example.public_ip
}
```

- Outputs allow you to extract information about your resources, which can be displayed after `terraform apply` or accessed by other configurations.

## Modules

- Modules allow you to create reusable components.

```hcl
module "vpc" {
  source = "./modules/vpc"
  cidr_block = "10.0.0.0/16"
}
```

- Use modules by specifying a `source` path and any required inputs.

## Backend Configuration

- Backends determine how Terraform loads and stores state.

```hcl
terraform {
  backend "s3" {
    bucket = "my-terraform-state"
    key    = "global/s3/terraform.tfstate"
    region = "us-east-1"
  }
}
```

## Providers

- Providers are plugins Terraform uses to manage resources.

```hcl
provider "aws" {
  region = "us-east-1"
}
```

- Specify providers and their configurations within your Terraform configurations.

---

This cheat sheet covers the fundamental aspects and commands of Terraform. For more detailed information, refer to the [Terraform Documentation](https://www.terraform.io/docs).
