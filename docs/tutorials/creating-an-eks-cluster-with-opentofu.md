Orchestrating Containers with OpenTofu: Creating an EKS Cluster
In this tutorial, we'll delve into the world of container orchestration by creating an Amazon Elastic Kubernetes Service (EKS) cluster using OpenTofu.

Why EKS?
EKS is a managed Kubernetes service that makes it easy to run Kubernetes on AWS without needing to install, operate, and maintain your own 1  Kubernetes control plane. This allows you to focus on building and deploying your applications.   
 1. 
medium.com
medium.com

Step 1: Define the EKS Cluster
Create a file named eks.tf and add the following code:

Terraform

resource "aws_eks_cluster" "example" {
  name     = "my-eks-cluster"
  role_arn = aws_iam_role.eks_cluster.arn
  version = "1.24" # Specify your desired Kubernetes version

  vpc_config {
    subnet_ids              = [aws_subnet.public_subnet_1.id, aws_subnet.public_subnet_2.id] 
    endpoint_public_access = true
    public_access_cidrs    = ["0.0.0.0/0"]
  }
}

resource "aws_iam_role" "eks_cluster" {
  name = "eks-cluster-role"

  assume_role_policy = <<POLICY
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "eks.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
POLICY
}

resource "aws_iam_role_policy_attachment" "eks-cluster-AmazonEKSClusterPolicy" {
  policy_arn = "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
  role       = aws_iam_role.eks_cluster.name
}
This code defines an EKS cluster with a specified version and VPC configuration. It also creates an IAM role with the necessary permissions for the EKS cluster.

Step 2: Configure kubectl
To interact with your EKS cluster, you'll need to configure kubectl, the Kubernetes command-line tool. You can find instructions on how to install and configure kubectl in the Kubernetes documentation.

Once kubectl is installed, you'll need to update your kubeconfig with the cluster information. You can use the aws eks update-kubeconfig command for this.

Step 3: Apply the Changes
Run the OpenTofu commands to apply your changes:

Bash

opentofu init
opentofu plan
opentofu apply
Step 4: Verify Your EKS Cluster
You can verify the EKS cluster creation in the AWS console by navigating to the EKS dashboard. You can also use kubectl commands to interact with your cluster and verify its status.

Congratulations!
You've successfully created an EKS cluster using OpenTofu.

Next Steps:
Deploy a sample application to your EKS cluster.
Explore different EKS features, such as node groups and managed node groups.
Learn how to use Kubernetes concepts like deployments, services, and pods.