Allocating a Static IP with OpenTofu: Creating an Elastic IP (EIP)
In this tutorial, we'll learn how to create an Elastic IP (EIP) address using OpenTofu. EIPs provide a static public IP that you can associate with your AWS resources.

Why EIPs?
EIPs offer several benefits for your cloud infrastructure:

Static IP Address: EIPs provide a fixed public IP address that you can associate with your instances or other resources, even if their private IP addresses change.
Fault Tolerance: If an instance with an associated EIP fails, you can quickly re-associate the EIP with another instance to maintain connectivity.
Accessibility: EIPs make it easier to access your resources from the internet, especially if you have dynamic IP addresses or need a consistent address for DNS records.
Step 1: Define the EIP
Create a file named eip.tf and add the following code:

Terraform

resource "aws_eip" "example" {
  vpc = true

  tags = {
    Name = "My EIP"
  }
}
This code defines an EIP with the vpc attribute set to true, which means it will be created in your VPC.

Step 2: Associate the EIP with Your Instance
To associate the EIP with your EC2 instance, add the following code to your main.tf file within the aws_instance resource block:

Terraform

  associate_public_ip_address = false # Prevent AWS from automatically assigning a public IP

  public_ip = aws_eip.example.public_ip
This code first disables the automatic assignment of a public IP address by AWS. Then, it associates the public IP of your EIP with the instance.

Step 3: Apply the Changes
Open your terminal, navigate to the directory containing your OpenTofu files, and run the following commands:

Bash

opentofu init
opentofu plan
opentofu apply
OpenTofu will create the EIP and associate it with your EC2 instance.

Step 4: Verify Your EIP
You can verify the EIP creation and association in the AWS console by navigating to the EC2 dashboard and selecting your instance. The EIP will be displayed in the instance details.

Congratulations!
You've successfully created an EIP and associated it with your EC2 instance using OpenTofu.

Next Steps:
Explore other EIP features, such as associating it with a network interface.
Learn how to disassociate and release EIPs.
Consider using EIPs with other AWS resources, such as NAT Gateways.