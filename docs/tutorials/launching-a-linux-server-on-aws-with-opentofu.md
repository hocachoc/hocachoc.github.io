# Your First Steps with IaC: Launching a Linux Server on AWS with OpenTofu

Welcome to the world of Infrastructure as Code (IaC)! In this tutorial, we'll guide you through your first steps with OpenTofu, a powerful tool that allows you to define and manage your cloud infrastructure using code.

## Why OpenTofu?

OpenTofu offers several advantages for managing your cloud infrastructure:

- **Automation**: No more clicking through endless menus in the AWS console. OpenTofu automates the process of creating and configuring your cloud resources.
- **Consistency**: OpenTofu ensures that your infrastructure is always deployed in a consistent and predictable manner, eliminating manual errors and inconsistencies.
- **Version Control**: You can track changes to your infrastructure code using version control systems like Git, making it easy to roll back changes or collaborate with others.
- **Reusability**: You can create reusable modules that can be used to deploy similar infrastructure components across different projects.

## Prerequisites

Before we begin, make sure you have the following:

- **An AWS Account**: You'll need an active AWS account to deploy your infrastructure. If you don't have one already, you can create a free tier account by following the instructions on the [AWS Account Creation page](#).

- **AWS Credentials**: Once you have an AWS account, you'll need to configure your AWS credentials on your local machine. This allows OpenTofu to interact with your AWS resources. You can find detailed instructions on how to set up your AWS credentials in the [AWS Credentials documentation](#).

- **OpenTofu Installed**: OpenTofu is the IaC tool we'll be using to define and manage our infrastructure.1 You can download and install OpenTofu by following the instructions on the [OpenTofu Installation page](#).

## Step 1: Define Your Infrastructure

Let's start by creating a simple OpenTofu configuration file that defines a Linux EC2 instance on AWS. Create a new file named main.tf and add the following code:

```terraform
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
  ami           = "ami-0c94855ba95c574c8" # Replace with a suitable AMI ID for your region
  instance_type = "t2.micro"
  tags = {
    Name = "My First Instance"
  }
}
```

Let's break down this code:

- **`terraform` block**: This block specifies the required providers for our configuration. In this case, we're using the `aws` provider.
- **`provider "aws"` block**: This block configures the AWS provider with the desired region. Replace `"us-west-2"` with your preferred AWS region.
- **`resource "aws_instance" "example"` block**: This block defines an EC2 instance resource named "example".
  - `ami`: This specifies the Amazon Machine Image (AMI) ID to use for the instance. Replace `"ami-0c94855ba95c574c8"` with an appropriate AMI ID for your region. You can find AMI IDs in the AWS console.
  - `instance_type`: This specifies the instance type, which determines the compute and memory capacity of the instance. We're using a `t2.micro `instance, which is a free tier eligible instance type.
  - `tags`: This allows you to add tags to your instance for easy identification and organization.

## Step 2: Initialize OpenTofu

Open your terminal and navigate to the directory where you saved `main.tf`. Then run the following command:

```bash
opentofu init
```

This command initializes the working directory and downloads the necessary plugins for the AWS provider.

## Step 3: Plan Your Infrastructure

Before applying your configuration, it's a good practice to run a plan to see what changes OpenTofu will make to your infrastructure. Run the following command:

```bash
opentofu plan
```

OpenTofu will analyze your configuration and display a plan of the resources it will create. This allows you to review the changes before they are applied.

## Step 4: Apply Your Configuration

If you're happy with the plan, you can apply your configuration and create the EC2 instance. Run the following command:

```bash
opentofu apply
```

OpenTofu will prompt you to confirm the changes. Type `yes` and press Enter to proceed.

OpenTofu will now create the EC2 instance in your AWS account. You can monitor the progress in your terminal.

## Step 5: Verify Your Instance

Once the apply process is complete, you can verify that your instance has been created by logging into the AWS console and navigating to the EC2 dashboard. You should see your newly created instance with the name "My First Instance".

Congratulations! You've successfully launched your first Linux server on AWS using OpenTofu.

**Next Steps:**

- Try modifying your configuration to change the instance type, AMI, or tags.
- Explore other OpenTofu resources, such as security groups, volumes, and networks.
- Learn how to destroy your infrastructure using `opentofu destroy`.
