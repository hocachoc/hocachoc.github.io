Distributing Content Globally with OpenTofu: Setting Up CloudFront
In today's interconnected world, delivering content quickly and efficiently to users across the globe is paramount. That's where CloudFront comes in. This tutorial will guide you through setting up a CloudFront distribution using OpenTofu.

Why CloudFront?
CloudFront is Amazon's content delivery network (CDN). It caches your content at edge locations around the world, ensuring fast delivery and low latency for your users, regardless of their location.

Step 1: Define the CloudFront Distribution
Create a file named cloudfront.tf and add the following code:

Terraform

resource "aws_cloudfront_distribution" "example" {
  origin {
    domain_name = aws_lb.example.dns_name # Replace with your ALB's DNS name
    origin_id   = "myS3Origin"
  }

  enabled             = true
  is_ipv6_enabled     = true
  comment             = "My CloudFront Distribution"
  default_root_object = "index.html"

  aliases = ["example.com"] # Replace with your domain name

  default_cache_behavior {
    allowed_methods  = ["GET", "HEAD"]
    cached_methods   = ["GET", "HEAD"]
    target_origin_id = "myS3Origin"
    
    forwarded_values {
      query_string = false
      cookies {
        forward = "none"
      }
    }

    viewer_protocol_policy = "redirect-to-https"
    min_ttl                = 0
    default_ttl            = 3600
    max_ttl                = 86400
  }

  price_class = "PriceClass_All"

  restrictions {
    geo_restriction {
      restriction_type = "none"
    }
  }

  viewer_certificate {
    acm_certificate_arn = aws_acm_certificate.example.arn # Replace with your ACM certificate ARN
    ssl_support_method = "sni-only"
  }
}
This code defines a CloudFront distribution with your ALB as the origin. It configures caching behavior, redirects HTTP to HTTPS, and uses your ACM certificate for SSL.

Step 2: Apply the Changes
Run the OpenTofu commands to apply your changes:

Bash

opentofu init
opentofu plan
opentofu apply
Step 3: Verify Your Distribution
You can verify the CloudFront distribution creation in the AWS console by navigating to the CloudFront dashboard.