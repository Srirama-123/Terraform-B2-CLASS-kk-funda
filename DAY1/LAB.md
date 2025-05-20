# **Launch an EC2 Instance in AWS Using Terraform**

## **Step 1: Install Prerequisites**
Ensure you have the following installed on your system:

1. **Terraform** → [Download & Install Terraform](https://developer.hashicorp.com/terraform/downloads)
2. **AWS CLI** → [Install AWS CLI](https://aws.amazon.com/cli/)
3. **AWS Credentials** configured using:
   ```bash
   aws configure
   ```
   Enter:
   - AWS Access Key ID
   - AWS Secret Access Key
   - Default Region (e.g., `us-east-1`)
   - Output Format (`json`)

Verify authentication:
```bash
aws sts get-caller-identity
```

---

## **Step 2: Create a Terraform Project**
Create a new directory for your Terraform project:
```bash
mkdir terraform-aws-ec2
cd terraform-aws-ec2
```

---

## **Step 3: Create Terraform Configuration Files**
Inside the `terraform-aws-ec2` directory, create the following **`.tf`** files.

### **1. `provider.tf` (AWS Provider Configuration)**
```hcl
provider "aws" {
  region = "us-east-1"  # Change to your preferred region
}
```

### **2. `ec2.tf` (EC2 Instance Configuration)**
```hcl
resource "aws_instance" "my_ec2" {
  ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux 2 AMI (Change as per your region)
  instance_type = "t2.micro"
  key_name      = "my-key"  # Ensure you have created an AWS Key Pair with this name

  tags = {
    Name = "Terraform-EC2"
  }
}
```

### **3. `output.tf` (Output Public IP)**
```hcl
output "instance_public_ip" {
  value = aws_instance.my_ec2.public_ip
}
```

---

## **Step 4: Initialize, Plan, and Apply Terraform**
### **1. Initialize Terraform**
```bash
terraform init
```
- This downloads the necessary AWS provider plugins.

- Then Execute This command     **terraform validate**  ( it check the all the  syntax whether it is correct or not ) 

### **2. Preview Execution Plan**
```bash
terraform plan
```
- This shows what Terraform will create.

### **3. Apply Configuration**
```bash
terraform apply -auto-approve
```
- This creates the EC2 instance.

### **4. Get Public IP**
```bash
terraform output instance_public_ip
```
- Copy the outputted **Public IP**.

---

## **Step 5: Connect to EC2**
SSH into your EC2 instance using:
```bash
ssh -i my-key.pem ec2-user@<PUBLIC_IP>
```
*(Replace `<PUBLIC_IP>` with the actual IP from `terraform output`.)*

---

## **Step 6: Destroy Infrastructure (If Needed)**
To **delete** the EC2 instance and free resources:
```bash
terraform destroy -auto-approve
```

---



