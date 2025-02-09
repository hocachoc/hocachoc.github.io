Securing Your Server: Creating a Security Group with OpenTofu
In our previous tutorial, you learned how to launch a Linux server on AWS using OpenTofu. Now, it's time to take a crucial step towards securing your server by creating a security group.

Why Security Groups?

Think of a security group as a virtual firewall for your server. It controls inbound and outbound traffic, allowing you to specify which ports and protocols are allowed to access your server. This helps protect your server from unauthorized access and malicious attacks.

Step 1:  Define the Security Group

Let's create an OpenTofu configuration file to define our security group. Create a new file named security_group.tf and add the following code:

Terraform

resource "aws_security_group" "allow_ssh" {
  name = "allow_ssh"
  description = "Allow SSH inbound traffic"

 ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"] #  Allow SSH from anywhere (for demonstration purposes)
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "allow_ssh"
  }
}
Let's break down this code:

resource "aws_security_group" "allow_ssh" block: This defines a security group resource named "allow_ssh".
name: The name of the security group.
description: A brief description of the security group's purpose.
ingress: This block defines inbound traffic rules.
from_port and to_port: Specify the port range to allow. In this case, we're allowing traffic on port 22 (SSH).
protocol: Specifies the protocol to allow (TCP, UDP, ICMP).
cidr_blocks: Specifies the IP address ranges allowed to access the port. "0.0.0.0/0" allows access from anywhere (for this tutorial, we'll allow SSH from anywhere for simplicity. In a production environment, you would restrict this to your own IP address or a trusted range).
egress: This block defines outbound traffic rules. We're allowing all outbound traffic by default.
tags: Adds tags to the security group for easy identification.
Step 2:  Associate the Security Group with Your Instance

Now, let's modify your main.tf file from the previous tutorial to associate this security group with your EC2 instance. Add the following line within the aws_instance resource block:

Terraform

  vpc_security_group_ids = [aws_security_group.allow_ssh.id]
Your updated main.tf file should now look like this:

Terraform

terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

provider "aws" {
  region = "us-west-2" # Replace with your desired region
}

resource "aws_instance" "example" {
  ami                    = "ami-0c94855ba95c574c8" # Replace with a suitable AMI ID for your region
  instance_type          = "t2.micro"
  vpc_security_group_ids = [aws_security_group.allow_ssh.id] # Associate the security group
  tags = {
    Name = "My First Instance"
  }
}
This line tells OpenTofu to associate the security group we defined in security_group.tf with our EC2 instance.

Step 3:  Apply the Changes

Open your terminal, navigate to the directory containing your OpenTofu files, and run the following commands:

Bash

opentofu init
opentofu plan
opentofu apply
OpenTofu will create the security group and associate it with your EC2 instance.

Step 4:  Verify Your Security Group

You can verify the security group configuration in the AWS console by navigating to the EC2 dashboard and selecting "Security Groups". You should see your newly created security group with the inbound rule for SSH.

Congratulations! You've successfully secured your server by creating a security group with OpenTofu.

Next Steps:

Try modifying the security group rules to allow different ports or protocols.
Explore other security group features, such as egress rules and network interfaces.
Learn how to use security groups to control access to other AWS resources, such as databases and load balancers.