---
draft: false
date:
  created: 2025-03-09
categories:
  - IaC
authors:
  - nhamchanvi
comments: true
---
# The Architect's Guide: Terraform Lifecycle Management Explained

Imagine your Terraform project is a grand building construction. You're not just throwing bricks together; you're meticulously designing a complex structure, a testament to your infrastructure-as-code expertise.

[![Image]](#)

[Image]: ../../assets/terraform-lifecycle-management-building.jpg

<div class="grid cards" markdown>
  - [Thanks to ![tekos-logo](../../assets/logo-tekos.png){ width="20" } for supporting this content.](https://tekos.net/)
</div>

<!-- more -->

## 1. The Architectural Blueprint: `terraform init`

This is like the initial architectural planning phase. You're gathering all the necessary resources and tools before construction begins.

You're downloading the specialized construction materials (**providers**) that enable you to build specific components of your building (e.g., steel beams for skyscrapers, plumbing for water systems).
You're setting up the site office (**remote backend**), where all the blueprints and important documents (**state**) are stored.
You're ensuring all the necessary tools and equipment are available (initializing the working directory).

```bash title="terraform init"

    Initializing the backend...

    Initializing provider plugins...
    - Finding latest version of hashicorp/aws...
    - Installing hashicorp/aws v5.90.0...
    - Installed hashicorp/aws v5.90.0 (signed by HashiCorp)

    Terraform has created a lock file .terraform.lock.hcl to record the provider
    selections it made above. Include this file in your version control repository
    so that Terraform can guarantee to make the same selections by default when
    you run "terraform init" in the future.

    Terraform has been successfully initialized!

    You may now begin working with Terraform. Try running "terraform plan" to see
    any changes that are required for your infrastructure. All Terraform commands
    should now work.

    If you ever set or change modules or backend configuration for Terraform,
    rerun this command to reinitialize your working directory. If you forget, other
    commands will detect it and remind you to do so if necessary.
```

## 2. The Foundation Laying: `terraform apply` (Initial Deployment)

This is the initial construction phase, where you're laying the foundation and erecting the main structure.

You're following the architectural blueprints (**your code**) to build the core components of your building.
You're ensuring that the foundation is solid and that the main structure is stable.
Terraform is actively creating resources, such as Virtual Machines, networks, and databases, which are the building blocks of your digital building.

```bash title="terraform apply"

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.web will be created
  + resource "aws_instance" "web" {
      + ami                                  = "ami-0076ac74e7710cd06"
      + arn                                  = (known after apply)
      + associate_public_ip_address          = (known after apply)
      + availability_zone                    = (known after apply)
      + cpu_core_count                       = (known after apply)
      + cpu_threads_per_core                 = (known after apply)
      + disable_api_stop                     = (known after apply)
      + disable_api_termination              = (known after apply)
      + ebs_optimized                        = (known after apply)
      + enable_primary_ipv6                  = (known after apply)
      + get_password_data                    = false
      + host_id                              = (known after apply)
      + host_resource_group_arn              = (known after apply)
      + iam_instance_profile                 = (known after apply)
      + id                                   = (known after apply)
      + instance_initiated_shutdown_behavior = (known after apply)
      + instance_lifecycle                   = (known after apply)
      + instance_state                       = (known after apply)
      + instance_type                        = "t3.micro"
      + ipv6_address_count                   = (known after apply)
      + ipv6_addresses                       = (known after apply)
      + key_name                             = (known after apply)
      + monitoring                           = (known after apply)
      + outpost_arn                          = (known after apply)
      + password_data                        = (known after apply)
      + placement_group                      = (known after apply)
      + placement_partition_number           = (known after apply)
      + primary_network_interface_id         = (known after apply)
      + private_dns                          = (known after apply)
      + private_ip                           = (known after apply)
      + public_dns                           = (known after apply)
      + public_ip                            = (known after apply)
      + secondary_private_ips                = (known after apply)
      + security_groups                      = (known after apply)
      + source_dest_check                    = true
      + spot_instance_request_id             = (known after apply)
      + subnet_id                            = (known after apply)
      + tags                                 = {
          + "Name" = "HelloWorld"
        }
      + tags_all                             = {
          + "Name" = "HelloWorld"
        }
      + tenancy                              = (known after apply)
      + user_data                            = (known after apply)
      + user_data_base64                     = (known after apply)
      + user_data_replace_on_change          = false
      + vpc_security_group_ids               = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + public_ip = (known after apply)

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

aws_instance.web: Creating...
aws_instance.web: Still creating... [10s elapsed]
aws_instance.web: Still creating... [20s elapsed]
aws_instance.web: Creation complete after 22s [id=i-0343344212a5a2b7d]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

public_ip = "13.37.220.7"
```

## 3. The Inspection and Planning: `terraform plan` (Change Preview)

This is like an inspection phase, where you're reviewing the blueprints and planning any modifications.

You're examining the proposed changes to your building before implementing them.
You're identifying any potential issues or conflicts that may arise from the changes.
Terraform compares the current state of your infrastructure with the desired state, showing you the changes it will make.

First, imaging that you want to allow SSH inbound traffic to the instance, update the Terraform code
```bash title="cat main.tf" hl_lines="8-27 33"
# main.tf - Example Terraform Configuration

# Configure the AWS Provider
provider "aws" {
  region = "eu-west-3"
}

# Create a Security Group
resource "aws_security_group" "allow_ssh" {
  description = "Allow SSH inbound traffic"
  ingress {
    description = "SSH from anywhere"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
  tags = {
    Name = "allow-ssh"
  }
}

# Create an EC2 Instance
resource "aws_instance" "web" {
  ami           = "ami-0076ac74e7710cd06"
  instance_type = "t3.micro"
  vpc_security_group_ids = [aws_security_group.allow_ssh.id]

  tags = {
    Name = "HelloWorld"
  }
}

# Output the Public IP of the EC2 Instance
output "public_ip" {
  value = aws_instance.web.public_ip
}
```
```bash title="terraform plan"
aws_instance.web: Refreshing state... [id=i-0343344212a5a2b7d]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
  ~ update in-place

Terraform will perform the following actions:

  # aws_instance.web will be updated in-place
  ~ resource "aws_instance" "web" {
        id                                   = "i-0343344212a5a2b7d"
        tags                                 = {
            "Name" = "HelloWorld"
        }
      ~ vpc_security_group_ids               = [
          - "sg-0a64bc766f1a92470",
        ] -> (known after apply)
        # (30 unchanged attributes hidden)

        # (8 unchanged blocks hidden)
    }

  # aws_security_group.allow_ssh will be created
  + resource "aws_security_group" "allow_ssh" {
      + arn                    = (known after apply)
      + description            = "Allow SSH inbound traffic"
      + egress                 = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = false
              + to_port          = 0
            },
        ]
      + id                     = (known after apply)
      + ingress                = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = "SSH from anywhere"
              + from_port        = 22
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 22
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags                   = {
          + "Name" = "allow-ssh"
        }
      + tags_all               = {
          + "Name" = "allow-ssh"
        }
      + vpc_id                 = (known after apply)
    }

Plan: 1 to add, 1 to change, 0 to destroy.

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

## 4. The Ongoing Construction: `terraform apply` (Changes)

This is the ongoing construction phase, where you're implementing the planned modifications.

You're implementing the changes that were identified in the inspection phase.
You're ensuring that the modifications are integrated seamlessly with the existing structure.
Terraform is making the required changes to your infrastructure.

```bash title="terraform apply"
aws_instance.web: Refreshing state... [id=i-0343344212a5a2b7d]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
  ~ update in-place

Terraform will perform the following actions:

  # aws_instance.web will be updated in-place
  ~ resource "aws_instance" "web" {
        id                                   = "i-0343344212a5a2b7d"
        tags                                 = {
            "Name" = "HelloWorld"
        }
      ~ vpc_security_group_ids               = [
          - "sg-0a64bc766f1a92470",
        ] -> (known after apply)
        # (30 unchanged attributes hidden)

        # (8 unchanged blocks hidden)
    }

  # aws_security_group.allow_ssh will be created
  + resource "aws_security_group" "allow_ssh" {
      + arn                    = (known after apply)
      + description            = "Allow SSH inbound traffic"
      + egress                 = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = false
              + to_port          = 0
            },
        ]
      + id                     = (known after apply)
      + ingress                = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = "SSH from anywhere"
              + from_port        = 22
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 22
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags                   = {
          + "Name" = "allow-ssh"
        }
      + tags_all               = {
          + "Name" = "allow-ssh"
        }
      + vpc_id                 = (known after apply)
    }

Plan: 1 to add, 1 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

aws_security_group.allow_ssh: Creating...
aws_security_group.allow_ssh: Creation complete after 5s [id=sg-07c5de6c1a356fd8f]
aws_instance.web: Modifying... [id=i-0343344212a5a2b7d]
aws_instance.web: Modifications complete after 5s [id=i-0343344212a5a2b7d]

Apply complete! Resources: 1 added, 1 changed, 0 destroyed.

Outputs:

public_ip = "13.37.220.7"
```

## 5. The Building's Memory: `terraform state list`

This is like the building's maintenance log, recording every change and modification.

The state file stores the current state of your building, including all its components and configurations.
It allows Terraform to track changes and ensure that the building remains consistent with the blueprints.
Using a remote backend is like storing the maintenance log in a secure, centralized location.

```bash title="terraform state list"
aws_instance.web
aws_security_group.allow_ssh
```

!!! info
    Terraform State Management is out-of-scope of this project, you can try your luck by searching on this website.

## 6. The Demolition: `terraform destroy`

This is the demolition phase, where you're tearing down the building.

You're removing all the components of your building in a controlled and orderly manner.
You're ensuring that the site is cleared and ready for future projects.
Terraform removes all the resources that it manages.

```bash title="terraform destroy"
aws_security_group.allow_ssh: Refreshing state... [id=sg-07c5de6c1a356fd8f]
aws_instance.web: Refreshing state... [id=i-0343344212a5a2b7d]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # aws_instance.web will be destroyed
  - resource "aws_instance" "web" {
      - ami                                  = "ami-0076ac74e7710cd06" -> null
      - arn                                  = "arn:aws:ec2:eu-west-3:842445166689:instance/i-0343344212a5a2b7d" -> null
      - associate_public_ip_address          = true -> null
      - availability_zone                    = "eu-west-3c" -> null
      - cpu_core_count                       = 1 -> null
      - cpu_threads_per_core                 = 2 -> null
      - disable_api_stop                     = false -> null
      - disable_api_termination              = false -> null
      - ebs_optimized                        = false -> null
      - get_password_data                    = false -> null
      - hibernation                          = false -> null
      - id                                   = "i-0343344212a5a2b7d" -> null
      - instance_initiated_shutdown_behavior = "stop" -> null
      - instance_state                       = "running" -> null
      - instance_type                        = "t3.micro" -> null
      - ipv6_address_count                   = 0 -> null
      - ipv6_addresses                       = [] -> null
      - monitoring                           = false -> null
      - placement_partition_number           = 0 -> null
      - primary_network_interface_id         = "eni-019b97d38ad8bbc1a" -> null
      - private_dns                          = "ip-172-31-46-161.eu-west-3.compute.internal" -> null
      - private_ip                           = "172.31.46.161" -> null
      - public_dns                           = "ec2-13-37-220-7.eu-west-3.compute.amazonaws.com" -> null
      - public_ip                            = "13.37.220.7" -> null
      - secondary_private_ips                = [] -> null
      - security_groups                      = [
          - "terraform-20250310103052126100000001",
        ] -> null
      - source_dest_check                    = true -> null
      - subnet_id                            = "subnet-051cb59940ea1c15e" -> null
      - tags                                 = {
          - "Name" = "HelloWorld"
        } -> null
      - tags_all                             = {
          - "Name" = "HelloWorld"
        } -> null
      - tenancy                              = "default" -> null
      - user_data_replace_on_change          = false -> null
      - vpc_security_group_ids               = [
          - "sg-07c5de6c1a356fd8f",
        ] -> null

      - capacity_reservation_specification {
          - capacity_reservation_preference = "open" -> null
        }

      - cpu_options {
          - core_count       = 1 -> null
          - threads_per_core = 2 -> null
        }

      - credit_specification {
          - cpu_credits = "unlimited" -> null
        }

      - enclave_options {
          - enabled = false -> null
        }

      - maintenance_options {
          - auto_recovery = "default" -> null
        }

      - metadata_options {
          - http_endpoint               = "enabled" -> null
          - http_protocol_ipv6          = "disabled" -> null
          - http_put_response_hop_limit = 1 -> null
          - http_tokens                 = "optional" -> null
          - instance_metadata_tags      = "disabled" -> null
        }

      - private_dns_name_options {
          - enable_resource_name_dns_a_record    = false -> null
          - enable_resource_name_dns_aaaa_record = false -> null
          - hostname_type                        = "ip-name" -> null
        }

      - root_block_device {
          - delete_on_termination = true -> null
          - device_name           = "/dev/xvda" -> null
          - encrypted             = false -> null
          - iops                  = 3000 -> null
          - tags                  = {} -> null
          - tags_all              = {} -> null
          - throughput            = 125 -> null
          - volume_id             = "vol-0cae9505d90a3918b" -> null
          - volume_size           = 8 -> null
          - volume_type           = "gp3" -> null
        }
    }

  # aws_security_group.allow_ssh will be destroyed
  - resource "aws_security_group" "allow_ssh" {
      - arn                    = "arn:aws:ec2:eu-west-3:842445166689:security-group/sg-07c5de6c1a356fd8f" -> null
      - description            = "Allow SSH inbound traffic" -> null
      - egress                 = [
          - {
              - cidr_blocks      = [
                  - "0.0.0.0/0",
                ]
              - description      = ""
              - from_port        = 0
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "-1"
              - security_groups  = []
              - self             = false
              - to_port          = 0
            },
        ] -> null
      - id                     = "sg-07c5de6c1a356fd8f" -> null
      - ingress                = [
          - {
              - cidr_blocks      = [
                  - "0.0.0.0/0",
                ]
              - description      = "SSH from anywhere"
              - from_port        = 22
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "tcp"
              - security_groups  = []
              - self             = false
              - to_port          = 22
            },
        ] -> null
      - name                   = "terraform-20250310103052126100000001" -> null
      - name_prefix            = "terraform-" -> null
      - owner_id               = "842445166689" -> null
      - revoke_rules_on_delete = false -> null
      - tags                   = {
          - "Name" = "allow-ssh"
        } -> null
      - tags_all               = {
          - "Name" = "allow-ssh"
        } -> null
      - vpc_id                 = "vpc-08fd73e2c03c3f90b" -> null
    }

Plan: 0 to add, 0 to change, 2 to destroy.

Changes to Outputs:
  - public_ip = "13.37.220.7" -> null

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

aws_instance.web: Destroying... [id=i-0343344212a5a2b7d]
aws_instance.web: Still destroying... [id=i-0343344212a5a2b7d, 10s elapsed]
aws_instance.web: Still destroying... [id=i-0343344212a5a2b7d, 20s elapsed]
aws_instance.web: Still destroying... [id=i-0343344212a5a2b7d, 30s elapsed]
aws_instance.web: Still destroying... [id=i-0343344212a5a2b7d, 40s elapsed]
aws_instance.web: Destruction complete after 43s
aws_security_group.allow_ssh: Destroying... [id=sg-07c5de6c1a356fd8f]
aws_security_group.allow_ssh: Destruction complete after 1s

Destroy complete! Resources: 2 destroyed.
```

Now, Terraform State is cleared
```bash title="terraform state list"
```

## 7. Building Districts: `terraform workspace`

This is like having different districts within your city, each with its own purpose and configuration.

Workspaces allow you to manage multiple environments (e.g., dev, staging, prod) within the same Terraform configuration.
Each workspace has its state file, ensuring that environments are isolated and independent.
This is like having different building sites for various phases of the project.

```bash title="terraform workspace"
Usage: terraform [global options] workspace

  new, list, show, select and delete Terraform workspaces.

Subcommands:
    delete    Delete a workspace
    list      List Workspaces
    new       Create a new workspace
    select    Select a workspace
    show      Show the name of the current workspace
```

!!! info
    I will use Terraspace for multiple environments management, so Terraform Workspace may be fitted in some specific cases.

## 0. Project Code Usage and Explain

1. Clone the example code from Github
```bash title="git clone https://github.com/nhamchanvi/project-as-code.git"
Cloning into 'project-as-code'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 0), reused 4 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (4/4), done.
```
2. Change directory to the `project-as-code/terraform-lifecycle-management`
```bash title="cd project-as-code/terraform-lifecycle-management"
```
3. List the files/dirs inside the project folder
```bash title="ls -alh"
total 16K
drwxrwxr-x 2 chanvi chanvi 4.0K Mar 10 17:49 .
drwxrwxr-x 4 chanvi chanvi 4.0K Mar 10 17:49 ..
-rw-rw-r-- 1 chanvi chanvi  102 Mar 10 17:49 .gitignore
-rw-rw-r-- 1 chanvi chanvi  909 Mar 10 17:49 main.tf
```
4. Inspect the `main.tf`
```bash title="cat main.tf"
# main.tf - Example Terraform Configuration

# Configure the AWS Provider
provider "aws" {
  region = "eu-west-3"
}

# Create a Security Group
# resource "aws_security_group" "allow_ssh" {
#   description = "Allow SSH inbound traffic"
#   ingress {
#     description = "SSH from anywhere"
#     from_port   = 22
#     to_port     = 22
#     protocol    = "tcp"
#     cidr_blocks = ["0.0.0.0/0"]
#   }
#   egress {
#     from_port   = 0
#     to_port     = 0
#     protocol    = "-1"
#     cidr_blocks = ["0.0.0.0/0"]
#   }
#   tags = {
#     Name = "allow-ssh"
#   }
# }

# Create an EC2 Instance
resource "aws_instance" "web" {
  ami           = "ami-0076ac74e7710cd06"
  instance_type = "t3.micro"
  # vpc_security_group_ids = [aws_security_group.allow_ssh.id]

  tags = {
    Name = "HelloWorld"
  }
}

# Output the Public IP of the EC2 Instance
output "public_ip" {
  value = aws_instance.web.public_ip
}
```

    * `provider "aws"`: Configures the AWS provider, specifying the region.
    * `resource "aws_security_group" "allow_ssh"`: Creates a security group that allows SSH access.
    * `resource "aws_instance" "web"`: Creates an EC2 instance in the subnet, using the security group.
    * `output "public_ip"`: Outputs the public IP address of the EC2 instance.

