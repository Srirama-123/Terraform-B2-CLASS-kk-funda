# Terraform Conditional Expressions

## **Introduction**
Conditional expressions in Terraform allow you to make decisions within your configurations based on conditions. This helps in dynamically setting values, reducing redundancy, and improving flexibility.

Terraform uses the `? :` operator to evaluate conditions.

### **Syntax:**
```hcl
condition ? true_value : false_value
```
- If the `condition` evaluates to `true`, Terraform returns `true_value`.
- If the `condition` evaluates to `false`, Terraform returns `false_value`.

---

## **1. Basic Conditional Example**
Example: Setting instance type based on the environment.
```hcl
variable "environment" {
  type    = string
  default = "dev"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = var.environment == "prod" ? "t3.large" : "t2.micro"
}
```
### **Explanation:**
- If `environment` is set to `prod`, instance type will be `t3.large`.
- Otherwise, it defaults to `t2.micro`.

---

## **2. Conditional Expressions with Boolean Variables**
Example: Enabling monitoring only in production.
```hcl
variable "enable_monitoring" {
  type    = bool
  default = false
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  monitoring    = var.enable_monitoring ? true : false
}
```
### **Explanation:**
- If `enable_monitoring` is `true`, detailed monitoring is enabled.
- Otherwise, it is disabled.

---

## **3. Using Conditionals in Lists**
Example: Assigning different availability zones based on region.
```hcl
variable "region" {
  type    = string
  default = "us-west-2"
}

variable "availability_zones" {
  type = map(list(string))
  default = {
    "us-east-1" = ["us-east-1a", "us-east-1b"]
    "us-west-2" = ["us-west-2a", "us-west-2b"]
  }
}

output "selected_az" {
  value = var.availability_zones[var.region]
}
```
### **Explanation:**
- The `availability_zones` variable contains a mapping of regions to availability zones.
- Terraform selects the correct list based on the region value.

---

## **4. Using Conditionals in Maps**
Example: Assigning instance sizes dynamically based on environment.
```hcl
variable "environment" {
  type    = string
  default = "dev"
}

variable "instance_sizes" {
  type = map(string)
  default = {
    "dev"  = "t2.micro"
    "prod" = "t3.large"
  }
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = lookup(var.instance_sizes, var.environment, "t2.micro")
}
```
### **Explanation:**
- The `lookup` function retrieves the instance type based on the environment.
- If `environment` is not found, it defaults to `t2.micro`.

---

## **5. Nested Conditional Expressions**
Example: Setting an instance type with multiple conditions.
```hcl
variable "environment" {
  type    = string
  default = "dev"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = var.environment == "prod" ? "t3.large" : var.environment == "staging" ? "t3.medium" : "t2.micro"
}
```
### **Explanation:**
- If `environment` is `prod`, the instance type is `t3.large`.
- If `environment` is `staging`, the instance type is `t3.medium`.
- Otherwise, it defaults to `t2.micro`.

---

## **6. Using Conditionals in Resource Count**
Example: Creating an EC2 instance only if monitoring is enabled.
```hcl
variable "enable_monitoring" {
  type    = bool
  default = false
}

resource "aws_instance" "monitoring_server" {
  count         = var.enable_monitoring ? 1 : 0
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```
### **Explanation:**
- If `enable_monitoring` is `true`, Terraform creates one instance.
- Otherwise, Terraform does not create any instance.

---

## **Best Practices for Using Conditional Expressions**
1. **Use Simple Conditions Where Possible** - Avoid deeply nested conditionals.
2. **Prefer Maps for Complex Conditions** - Helps keep configurations readable.
3. **Use Defaults for Fallback Values** - Ensures resilience.
4. **Use Conditionals in `count` and `for_each` for Optional Resources**.

---


