Managing DNS with OpenTofu: Creating a Hosted Zone and Records in Route 53
In this tutorial, we'll explore Route 53, Amazon's scalable and reliable DNS service. We'll create a hosted zone and configure DNS records to manage your domain names.

Why Route 53?
Route 53 provides a highly available and scalable DNS service, allowing you to route traffic to your applications and resources. It offers features like health checks, traffic policies, and domain registration.

Step 1: Define the Hosted Zone
Create a file named route53.tf and add the following code:

Terraform

resource "aws_route53_zone" "main" {
  name = "example.com"  # Replace with your domain name

  tags = {
    Name = "My Hosted Zone"
  }
}
This defines a hosted zone for the domain example.com. Replace this with your actual domain name.

Step 2: Define DNS Records
Now, let's add some DNS records to our hosted zone. Add the following code to route53.tf:

Terraform

resource "aws_route53_record" "www" {
  zone_id = aws_route53_zone.main.zone_id
  name    = "www"
  type    = "A"
  ttl     = "300"
  records = [aws_lb.example.dns_name] # Replace with your ALB's DNS name
}

resource "aws_route53_record" "root" {
  zone_id = aws_route53_zone.main.zone_id
  name    = "example.com" # Replace with your domain name
  type    = "A"
  ttl     = "300"
  alias {
    name                   = aws_lb.example.dns_name # Replace with your ALB's DNS name
    zone_id                = aws_lb.example.zone_id
    evaluate_target_health = true
  }
}
This creates two A records:

www: Points www.example.com to your Application Load Balancer.
root: Points example.com to your Application Load Balancer using an alias record.
Step 3: Apply the Changes
Run the OpenTofu commands to apply your changes:

Bash

opentofu init
opentofu plan
opentofu apply
Step 4: Verify Your Hosted Zone and Records
You can verify the creation of your hosted zone and records in the AWS console by navigating to the Route 53 dashboard.