# Terraform Variables for AWS

## Introduction

In Terraform, variables allow us to make configurations dynamic and reusable. They help define values externally, reducing hardcoding and making infrastructure more manageable. This guide covers variable types, usage, and best practices in AWS Terraform configurations.

## Types of Variables in Terraform

Terraform supports different types of variables:

### **1. String Variable**

Used for text values.

```hcl
variable "region" {
  description = "AWS region for deployment"
  type        = string
  default     = "us-west-2"
}

provider "aws" {
  region = var.region
}
```

### **2. Number Variable**

Used for numerical values.

```hcl
variable "instance_count" {
  description = "Number of EC2 instances"
  type        = number
  default     = 2
}

resource "aws_instance" "example" {
  count         = var.instance_count
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

### **3. Boolean Variable**

Used for true/false values.

```hcl
variable "enable_monitoring" {
  description = "Enable detailed monitoring"
  type        = bool
  default     = true
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  monitoring    = var.enable_monitoring
}
```

### **4. List Variable**

Used for defining an ordered sequence of values.

```hcl
variable "availability_zones" {
  description = "List of availability zones"
  type        = list(string)
  default     = ["us-west-2a", "us-west-2b"]
}

resource "aws_subnet" "example" {
  count            = length(var.availability_zones)
  vpc_id          = "vpc-12345678"
  cidr_block      = "10.0.${count.index}.0/24"
  availability_zone = var.availability_zones[count.index]
}
```

### **5. Map Variable**

Used for defining key-value pairs.

```hcl
variable "instance_types" {
  description = "Instance types for different environments"
  type        = map(string)
  default = {
    dev  = "t2.micro"
    prod = "t3.medium"
  }
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = var.instance_types["dev"]
}
```

## Defining Variables in Terraform

Terraform variables can be defined in different ways:

### **1. Using ****`.tfvars`**** File**

Create a `terraform.tfvars` file:

```hcl
region = "us-east-1"
instance_count = 3
enable_monitoring = false
```

Apply configuration using:

```sh
terraform apply -var-file="terraform.tfvars"
```

### **2. Passing Variables via CLI**

```sh
terraform apply -var="region=us-east-1" -var="instance_count=3"
```

### **3. Using Environment Variables**

```sh
export TF_VAR_region="us-east-1"
export TF_VAR_instance_count=3
terraform apply
```

## Best Practices for Using Variables

1. **Use Descriptive Names** - Variable names should clearly indicate their purpose.
2. **Provide Defaults Where Possible** - Reduces the need for manual input.
3. **Use ****`.tfvars`**** for Sensitive Data** - Avoid hardcoding sensitive values in code.
4. **Use ****`locals`**** for Derived Values** - Helps in better code organization.

## Conclusion

Terraform variables make infrastructure configurations flexible, reusable, and easier to manage. By properly structuring variables, AWS Terraform deployments become more efficient and maintainable.

---



