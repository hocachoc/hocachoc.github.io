Controlling Access with OpenTofu: Creating an IAM User and Role with Assume Role Functionality
In this tutorial, we'll dive deeper into Identity and Access Management (IAM) and learn how to create an IAM user and an IAM role with assume role capabilities using OpenTofu. This powerful combination allows you to delegate access to your AWS resources securely and efficiently.

Why IAM Users and Roles with Assume Role?
IAM users are identities within your AWS account that you create for people or applications. IAM roles, on the other hand, are identities that you can assign to AWS resources or federated users. The "assume role" functionality allows an entity (like an IAM user) to temporarily take on the permissions of an IAM role.

This is particularly useful for:

Delegating permissions: Granting specific access to users or applications without giving them permanent credentials.
Enhancing security: Limiting the scope of access and reducing the risk of credential compromise.
Enabling cross-account access: Allowing users from one AWS account to access resources in another account.
Step 1: Define the IAM User
Create a file named iam.tf and add the following code to define an IAM user:

Terraform

resource "aws_iam_user" "example" {
  name = "example-user"

  tags = {
    Name = "Example IAM User"
  }
}
This creates an IAM user named "example-user."

Step 2: Define the IAM Role
Next, define an IAM role that the user can assume. Add the following code to iam.tf:

Terraform

resource "aws_iam_role" "example" {
  name = "example-role"

  assume_role_policy = <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::YOUR_ACCOUNT_ID:user/example-user"  # Replace with your account ID
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
EOF
}
This defines an IAM role named "example-role." The assume_role_policy explicitly allows the "example-user" to assume this role.  Make sure to replace YOUR_ACCOUNT_ID with your actual AWS account ID.

Step 3: Define an IAM Policy (Optional)
You can optionally create an IAM policy to attach to the role, granting specific permissions. For example, to allow the role to read objects from an S3 bucket, add the following code to iam.tf:

Terraform

resource "aws_iam_policy" "example" {
  name        = "example-policy"
  description = "Example IAM Policy"

  policy = <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::your-s3-bucket/*"  # Replace with your S3 bucket name
    }
  ]
}
EOF
}

resource "aws_iam_role_policy_attachment" "example" {
  role       = aws_iam_role.example.name
  policy_arn = aws_iam_policy.example.arn
}
This 1  code defines an IAM policy that allows the role to read objects from the specified S3 bucket.  Replace "your-s3-bucket" with the name of your S3 bucket.   
 1. 
levelup.gitconnected.com
levelup.gitconnected.com

Step 4: Apply the Changes
Run the OpenTofu commands to apply your changes:

Bash

opentofu init
opentofu plan
opentofu apply
Step 5: Verify your IAM User and Role
You can verify the creation of your IAM user and role in the AWS console by navigating to the IAM dashboard.

Congratulations!
You've successfully created an IAM user and role with assume role functionality using OpenTofu.

Next Steps:
Explore different ways to use assume role, such as cross-account access or delegating permissions to applications.
Learn how to use the AWS Security Token Service (STS) to generate temporary credentials for assuming roles.
Implement least privilege principles by granting only the necessary permissions to your users and roles.