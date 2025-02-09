Creating an Application Load Balancer (ALB) with OpenTofu
In this tutorial, we'll create an Application Load Balancer (ALB) to distribute incoming traffic across multiple EC2 instances.

Why ALBs?
ALBs provide high availability and scalability for your applications by distributing traffic across multiple targets, such as EC2 instances.

Step 1: Define the ALB
Create a file named alb.tf and add the following code:

Terraform

resource "aws_lb" "example" {
  name               = "my-load-balancer"
  internal           = false
  load_balancer_type = "application"
  security_groups    = [aws_security_group.allow_ssh.id] # Replace with your security group ID
  subnets            = [aws_subnet.public_subnet_1.id, aws_subnet.public_subnet_2.id]

  tags = {
    Name = "My ALB"
  }
}
This defines an ALB with specified parameters like name, type, security groups, and subnets.

Step 2: Define a Target Group
Create a target group for the ALB to route traffic to. Add the following code to alb.tf:

Terraform

resource "aws_lb_target_group" "example" {
  name     = "my-targets"
  port     = 80
  protocol = "HTTP"
  vpc_id   = aws_vpc.main.id
}
This defines a target group named "my-targets" that listens on port 80 for HTTP traffic.

Step 3: Define a Listener
Define a listener for the ALB to listen for incoming traffic on a specific port and protocol. Add the following code to alb.tf:

Terraform

resource "aws_lb_listener" "example" {
  load_balancer_arn = aws_lb.example.arn
  port              = "80"
  protocol          = "HTTP"

  default_action {
    type             = "forward"
    target_group_arn = aws_lb_target_group.example.arn
  }
}
This defines a listener that listens on port 80 for HTTP traffic and forwards requests to the target group.

Step 4: Apply the Changes
Run the OpenTofu commands to apply your changes:

Bash

opentofu init
opentofu plan
opentofu apply
Step 5: Verify Your ALB
You can verify the ALB creation in the AWS console by navigating to the EC2 dashboard and selecting "Load Balancers."