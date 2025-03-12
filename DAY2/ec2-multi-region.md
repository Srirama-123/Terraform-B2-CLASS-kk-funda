# AWS Terraform: Deploying EC2 Instances in Multiple Regions

## Introduction
Deploying EC2 instances across multiple AWS regions enhances high availability and disaster recovery. This Terraform script provisions EC2 instances in two different AWS regions: `us-east-1` and `us-west-1`.

## Multi-Region Deployment in Terraform
Terraform allows defining multiple providers within a single configuration file. By using provider aliases, we can specify different AWS regions and create instances in each region accordingly.

## Terraform Script
```hcl
provider "aws" {
  alias  = "us_east_1"
  region = "us-east-1"
}

provider "aws" {
  alias  = "us_west_1"
  region = "us-west-1"
}

resource "aws_instance" "ec2_us_east" {
  provider      = aws.us_east_1
  ami           = "ami-0c55b159cbfafe1f0"  # Replace with valid AMI
  instance_type = "t2.micro"
  
  tags = {
    Name = "EC2-US-East-1"
  }
}

resource "aws_instance" "ec2_us_west" {
  provider      = aws.us_west_1
  ami           = "ami-0c55b159cbfafe1f0"  # Replace with valid AMI
  instance_type = "t2.micro"
  
  tags = {
    Name = "EC2-US-West-1"
  }
}
```

## Explanation
1. **Provider Block**: We define two provider blocks with different aliases to deploy resources in separate regions.
2. **Resource Definition**: The `aws_instance` resource is created twice, each associated with a different provider.
3. **AMI Selection**: Ensure you replace the AMI ID with a valid one for the respective region.
4. **Instance Tagging**: Each instance is tagged to identify the region in which it is deployed.

## Deployment Steps
1. Initialize Terraform: `terraform init`
2. Validate Configuration: `terraform validate`
3. Plan Deployment: `terraform plan`
4. Apply Deployment: `terraform apply -auto-approve`

## Conclusion
Using Terraform’s multi-provider feature, we can easily deploy EC2 instances across multiple AWS regions. This setup is ideal for redundancy, fault tolerance, and disaster recovery strategies.




**Further Reading:**
- [Terraform Registry](https://registry.terraform.io/)
- [Terraform Provider Documentation](https://developer.hashicorp.com/terraform/docs/providers)

