Securing Your Domain: Obtaining an ACM SSL Certificate with OpenTofu
In this tutorial, we'll secure your domain with an SSL certificate using AWS Certificate Manager (ACM).

Why ACM?
ACM makes it easy to provision, manage, and deploy SSL certificates for your websites and applications. It integrates seamlessly with other AWS services like Application Load Balancers.

Step 1: Request a Certificate
Create a file named acm.tf and add the following code:

Terraform

resource "aws_acm_certificate" "example" {
  domain_name       = "example.com" # Replace with your domain name
  validation_method = "DNS"

  tags = {
    Name = "My SSL Certificate"
  }
}

resource "aws_acm_certificate_validation" "example" {
  certificate_arn         = aws_acm_certificate.example.arn
  validation_record_fqdns = [aws_route53_record.root.fqdn]
}

resource "aws_route53_record" "cert_validation" {
  for_each = {
    for dvo in aws_acm_certificate.example.domain_validation_options : dvo.domain_name => {
      name   = dvo.resource_record_name
      record = dvo.resource_record_value
      type   = dvo.resource_record_type
    }
  }

  allow_overwrite = true
  name            = each.value.name
  records         = [each.value.record]
  ttl             = 60
  type            = each.value.type
  zone_id         = aws_route53_zone.main.zone_id
}
This code requests an SSL certificate for your domain and automatically creates the necessary DNS validation records in Route 53.

Step 2: Apply the Changes
Run the OpenTofu commands to apply your changes:

Bash

opentofu init
opentofu plan
opentofu apply
Step 3: Verify Your Certificate
You can verify the certificate issuance in the AWS console by navigating to the ACM dashboard.