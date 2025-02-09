Networking with OpenTofu: Creating a VPC and Subnets
In this tutorial, we'll dive into networking with OpenTofu. We'll create a Virtual Private Cloud (VPC) and subnets, the fundamental building blocks of your AWS network infrastructure.

Why VPCs and Subnets?
A VPC provides an isolated network environment within AWS where you can launch AWS resources. Subnets segment your VPC into smaller, isolated networks, allowing you to control traffic flow and security.

Step 1: Define the VPC
Create a file named vpc.tf and add the following code:

Terraform

resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "My VPC"
  }
}
This defines a VPC with the CIDR block 10.0.0.0/16, providing a range of private IP addresses for your resources.

Step 2: Define Subnets
Now, let's create two subnets within our VPC. Add the following code to vpc.tf:

Terraform

resource "aws_subnet" "public_subnet_1" {
  vpc_id     = aws_vpc.main.id
  cidr_block = "10.0.1.0/24"
  availability_zone = "us-west-2a" # Replace with your desired availability zone

  tags = {
    Name = "Public Subnet 1"
  }
}

resource "aws_subnet" "public_subnet_2" {
  vpc_id     = aws_vpc.main.id
  cidr_block = "10.0.2.0/24"
  availability_zone = "us-west-2b" # Replace with your desired availability zone

  tags = {
    Name = "Public Subnet 2"
  }
}
This creates two public subnets in different availability zones for high availability.

Step 3: Apply the Changes
Run the usual OpenTofu commands to apply your changes:

Bash

opentofu init
opentofu plan
opentofu apply
Step 4: Verify Your VPC and Subnets
You can verify the creation of your VPC and subnets in the AWS console by navigating to the VPC dashboard.