Creating a MySQL Database with OpenTofu
In this tutorial, we'll provision a MySQL database using Amazon Relational Database Service (RDS).

Why RDS?
RDS makes it easy to set up, operate, and scale a relational database in the cloud. It handles routine database tasks such as backups, software patching, and automatic failure detection.

Step 1: Define the RDS Instance
Create a file named database.tf and add the following code:

Terraform

resource "aws_db_instance" "default" {
  allocated_storage    = 20
  db_name              = "mydb"
  engine               = "mysql"
  engine_version       = "8.0"
  instance_class       = "db.t3.micro"
  identifier           = "mydb-instance"
  username             = "admin"  # Replace with your desired username
  password             = "password" # Replace with a strong password
  vpc_security_group_ids = [aws_security_group.allow_ssh.id] # Replace with your security group ID
  skip_final_snapshot  = true
}
This defines a MySQL RDS instance with specified parameters like storage, engine version, instance class, and credentials.

Step 2: Apply the Changes
Run the OpenTofu commands to apply your changes:

Bash

opentofu init
opentofu plan
opentofu apply
Step 3: Verify Your Database
You can verify the database creation in the AWS console by navigating to the RDS dashboard.