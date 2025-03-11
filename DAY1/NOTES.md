# Day 1: Introduction to Terraform & Infrastructure as Code (IaC)

## Topics Covered:
- What is Terraform?
- Why Use Terraform?
- Terraform vs. other IaC tools
- Installing Terraform on your system
- Configuring AWS CLI for Terraform

---

## What is Terraform?
Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp. It enables users to define, provision, and manage cloud infrastructure using declarative configuration files. Terraform supports multiple cloud providers, including AWS, Azure, and Google Cloud, allowing consistent automation across different environments.

### Key Features of Terraform:
- **Declarative Syntax**: Defines the desired state of infrastructure.
- **Multi-Cloud Support**: Works with AWS, Azure, GCP, and more.
- **State Management**: Maintains a state file to track infrastructure changes.
- **Automation & Scalability**: Automates resource provisioning and management.
- **Version Control**: Terraform configurations can be stored in Git for collaboration.

---

## Why Use Terraform?
- **Infrastructure as Code (IaC)**: Automates infrastructure deployment.
- **Consistency**: Ensures reproducibility across environments.
- **Automation**: Reduces manual provisioning errors.
- **Collaboration**: Works well in team environments with version control.
- **Multi-Cloud Support**: Enables cloud-agnostic deployments.

---

## Terraform vs. Other IaC Tools

| Feature              | Terraform | CloudFormation (AWS) | Ansible |
|----------------------|-----------|----------------------|---------|
| Multi-Cloud Support | ✅ Yes    | ❌ No (AWS Only)    | ✅ Yes  |
| Declarative Language | ✅ Yes (HCL) | ✅ Yes (YAML/JSON) | ❌ No (Procedural) |
| State Management     | ✅ Yes    | ✅ Yes             | ❌ No   |
| Mutable vs Immutable | ✅ Immutable | ❌ Mutable        | ❌ Mutable |
| Provisioning Speed   | ✅ Fast   | ✅ Fast            | 🔶 Medium |

Terraform stands out due to its declarative language (HCL), strong multi-cloud support, and powerful state management.

---

## Installing Terraform on Your System

### Windows Installation
1. Download Terraform from the [official website](https://www.terraform.io/downloads.html).
2. Extract the downloaded ZIP file.
3. Move the extracted `terraform.exe` to `C:\Program Files\Terraform`.
4. Add Terraform to the system `PATH`:
   - Search for "Environment Variables" in Windows.
   - Edit the `Path` variable under System Variables.
   - Add `C:\Program Files\Terraform`.
5. Verify the installation:
   ```sh
   terraform version
   ```

### Linux/macOS Installation
1. Run the following command to download and install Terraform:
   ```sh
   curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
   sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
   sudo apt-get update && sudo apt-get install terraform
   ```
2. Verify the installation:
   ```sh
   terraform version
   ```

---

## Configuring AWS CLI for Terraform
Terraform interacts with AWS via the AWS CLI. Follow these steps to configure it:

### Step 1: Install AWS CLI
- **Windows**: Download from [AWS CLI Installer](https://aws.amazon.com/cli/).
- **Linux/macOS**:
  ```sh
  curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
  sudo installer -pkg AWSCLIV2.pkg -target /
  ```
- Verify installation:
  ```sh
  aws --version
  ```

### Step 2: Create an IAM User for Terraform
1. Go to the AWS Management Console → IAM → Users.
2. Click "Add User", enter a username, and enable Programmatic Access.
3. Attach the policy **AdministratorAccess** (or least-privilege permissions).
4. Save the Access Key ID and Secret Access Key.

### Step 3: Configure AWS CLI
Run the following command and enter your IAM credentials:
```sh
aws configure
```
- **AWS Access Key ID**: (Enter the key from Step 2)
- **AWS Secret Access Key**: (Enter the secret key from Step 2)
- **Default region name**: e.g., `us-east-1`
- **Default output format**: (Press Enter for default `json`)

### Step 4: Verify AWS Configuration
Run the following command to verify authentication:
```sh
aws s3 ls
```
If no error appears, your AWS CLI is properly configured.

---

## Hands-on Exercise
1. Install Terraform on your system.
2. Verify the installation by running `terraform version`.
3. Configure AWS CLI with IAM user credentials (`aws configure`).
4. Verify AWS authentication using `aws s3 ls`.

---

## Conclusion
By the end of Day 1, students will:
- Understand Terraform’s role in Infrastructure as Code.
- Install and verify Terraform on their systems.
- Configure AWS CLI for Terraform deployments.
- Be ready to create their first Terraform configuration in the next session.
