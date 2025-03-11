Here is the complete guide in **GitHub-friendly Markdown (`.md`) format**. You can copy and save it as `terraform_aws_ec2_guide.md` for use in GitHub or documentation.  

---

```md
# Terraform Installation & EC2 Instance Creation on AWS

## Step 1: Introduction to Terraform

### What is Terraform?
Terraform is an **Infrastructure as Code (IaC)** tool that allows you to define and provision cloud resources using HashiCorp Configuration Language (**HCL**). It supports multiple cloud providers, including **AWS, Azure, and Google Cloud**.

### Key Features of Terraform
- **Declarative Language:** Define the desired state of infrastructure.
- **Cloud-Agnostic:** Supports AWS, Azure, GCP, and more.
- **State Management:** Maintains a state file (`terraform.tfstate`) to track resources.
- **Execution Plan:** `terraform plan` shows expected changes before applying.
- **Automation:** Easily automate infrastructure provisioning.

---

## Step 2: Install Terraform

### 1. Download Terraform

#### For Windows:
1. Download Terraform from the official site: [Terraform Download](https://developer.hashicorp.com/terraform/downloads)
2. Extract the ZIP file and place it in a folder (e.g., `C:\terraform`).
3. Add the Terraform binary to the **System PATH** (Steps below).

#### For Linux/MacOS:
```bash
sudo apt update && sudo apt install -y unzip
wget https://releases.hashicorp.com/terraform/1.11.1/terraform_1.11.1_linux_amd64.zip
unzip terraform_1.11.1_linux_amd64.zip
sudo mv terraform /usr/local/bin/
```

### 2. Verify Terraform Installation
Run the following command to check if Terraform is installed:
```bash
terraform -version
```
Expected Output:
```bash
Terraform v1.11.1
on windows_amd64
```

---

## Step 3: Add Terraform to System Path (Windows)
To use Terraform from any directory:
1. Open **Command Prompt (cmd)** or **PowerShell** as Administrator.
2. Copy the folder path where Terraform is extracted (e.g., `C:\Users\kkfunda\Downloads\terraform_1.11.1_windows_amd64`).
3. Search **"Environment Variables"** in Windows.
4. Click on **Environment Variables** → Find `Path` under **System Variables** → Click **Edit**.
5. Click **New**, paste the Terraform folder path, and click **OK**.
6. Restart the terminal and verify with:
   ```bash
   terraform -version
   ```

---

## Step 4: Install AWS CLI and Configure AWS

### 1. Install AWS CLI
- Download AWS CLI from: [AWS CLI Official Website](https://aws.amazon.com/cli/)
- Install it and verify:
  ```bash
  aws --version
  ```

### 2. Configure AWS CLI
Run:
```bash
aws configure
```
It will ask for:
- **AWS Access Key ID**
- **AWS Secret Access Key**
- **Region** (e.g., `us-east-1`)
- **Output format** (default: `json`)

To check the authentication:
```bash
aws sts get-caller-identity
```
Expected output:
```json
{
    "UserId": "XXXXXXXXXXXX",
    "Account": "123456789012",
    "Arn": "arn:aws:iam::123456789012:user/my-user"
}
```

---

## Step 5: Create an EC2 Instance using Terraform

### 1. Create a New Directory
```bash
mkdir terraform-aws-ec2
cd terraform-aws-ec2
```

### 2. Create Terraform Configuration Files

#### `provider.tf` (AWS Provider Configuration)
```hcl
provider "aws" {
  region = "us-east-1" # Change to your preferred region
}
```

#### `ec2.tf` (EC2 Instance Configuration)
```hcl
resource "aws_instance" "my_ec2" {
  ami           = "ami-0c55b159cbfafe1f0" # Amazon Linux 2 AMI (Change as per region)
  instance_type = "t2.micro"
  key_name      = "my-key" # Ensure you have created an AWS Key Pair with this name

  tags = {
    Name = "Terraform-EC2"
  }
}
```

#### `variables.tf` (Optional - Defining Variables)
```hcl
variable "region" {
  default = "us-east-1"
}
```

#### `output.tf` (Output Public IP)
```hcl
output "instance_public_ip" {
  value = aws_instance.my_ec2.public_ip
}
```

---

## Step 6: Initialize, Plan, and Apply Terraform

### 1. Initialize Terraform
Run:
```bash
terraform init
```
This downloads the required AWS provider plugins.

### 2. Plan Execution
Run:
```bash
terraform plan
```
It will show the resources that will be created.

### 3. Apply Configuration
Run:
```bash
terraform apply -auto-approve
```
Terraform will create the EC2 instance.

### 4. Get Public IP
Run:
```bash
terraform output instance_public_ip
```
Copy the public IP to connect via SSH.

---

## Step 7: Connect to the EC2 Instance

### 1. SSH into EC2
```bash
ssh -i my-key.pem ec2-user@<PUBLIC_IP>
```
(Replace `<PUBLIC_IP>` with the actual IP from `terraform output`.)

### 2. Verify EC2 Running on AWS Console
- Go to the **AWS Management Console** → **EC2 Dashboard**.
- Check if the instance is running.

---

## Step 8: Destroy the Infrastructure
To **delete** the EC2 instance and free resources, run:
```bash
terraform destroy -auto-approve
```

---

## Conclusion

✅ **Terraform simplifies AWS infrastructure provisioning.**  
✅ **With Terraform, you can automate resource creation, modification, and deletion.**  
✅ **State files track infrastructure changes.**  

### Basic Terraform Commands:
- `terraform init` → Initialize Terraform
- `terraform plan` → Show execution plan
- `terraform apply` → Create resources
- `terraform destroy` → Delete resources

---

## Next Steps

🔹 Deploy **Security Groups, IAM Roles, and S3 Buckets** using Terraform.  
🔹 Learn **Terraform Modules** to create reusable infrastructure.  
🔹 Use **Terraform Cloud & Remote State Management** for better collaboration.

🚀 Now you are ready to use Terraform for AWS infrastructure automation! Let me know if you need any modifications! 🎯
```

---

This is a **GitHub-friendly** Markdown file that preserves **proper formatting** for documentation. 🎯  
You can save this as `terraform_aws_ec2_guide.md` and use it in your **GitHub repository**, **Wiki**, or **training materials**. 🚀
