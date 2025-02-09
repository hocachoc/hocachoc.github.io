Provisioning an EBS Volume and Attaching it to Your EC2 Instance with OpenTofu
In the previous tutorials, you launched a Linux server and secured it with a security group. Now, let's expand your infrastructure by provisioning an Elastic Block Store (EBS) volume and attaching it to your EC2 instance.

Why EBS Volumes?
EBS volumes provide persistent block storage for your EC2 instances. Think of them as external hard drives that you can attach to your server. This allows you to:

Increase storage capacity: Add more storage to your instance as needed.
Improve performance: Choose different EBS volume types optimized for various workloads.
Enhance data durability: EBS volumes are designed for high availability and durability, protecting your data from loss.
Backup and restore data: Easily create snapshots of your EBS volumes for backups and disaster recovery.
Step 1: Define the EBS Volume
Create a new file named volume.tf and add the following code:

Terraform

resource "aws_ebs_volume" "example" {
  availability_zone = "us-west-2a" # Replace with your instance's availability zone
  size              = 10           # Size in gigabytes
  type              = "gp2"        # General purpose SSD volume type

  tags = {
    Name = "My EBS Volume"
  }
}
Let's break down this code:

resource "aws_ebs_volume" "example" block: This defines an EBS volume resource named "example".
availability_zone: Specifies the availability zone where the volume will be created. This should match the availability zone of your EC2 instance.
size: Specifies the size of the volume in gigabytes.
type: Specifies the volume type. We're using "gp2", which is a general purpose SSD volume.
tags: Adds tags to the volume for identification.
Step 2: Attach the EBS Volume to Your Instance
Now, let's create another file named attach_volume.tf to attach the EBS volume to your EC2 instance. Add the following code:

Terraform

resource "aws_volume_attachment" "example" {
  device_name = "/dev/sdf"       # Device name to attach the volume to
  volume_id   = aws_ebs_volume.example.id
  instance_id = aws_instance.example.id
}
resource "aws_volume_attachment" "example" block: This defines a volume attachment resource.
device_name: Specifies the device name to attach the volume to on the instance.
volume_id: References the ID of the EBS volume we created in volume.tf.
instance_id: References the ID of the EC2 instance from main.tf.
Step 3: Apply the Changes
Open your terminal, navigate to the directory containing your OpenTofu files, and run the following commands:

Bash

opentofu init
opentofu plan
opentofu apply
OpenTofu will create the EBS volume and attach it to your EC2 instance.

Step 4: Verify the Volume Attachment
You can verify the volume attachment in the AWS console by navigating to the EC2 dashboard, selecting your instance, and then checking the "Storage" tab. You should see your newly attached EBS volume.

You'll likely need to SSH into your instance and format the volume before you can use it.  (You can find instructions for formatting volumes in the AWS documentation.)

Congratulations!
You've successfully provisioned an EBS volume and attached it to your EC2 instance using OpenTofu.

Next Steps:
Explore different EBS volume types and their performance characteristics.
Learn how to create snapshots of your EBS volumes for backups.
Experiment with resizing your EBS volumes.
