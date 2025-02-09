Protecting Your Applications with OpenTofu: Setting Up a Web Application Firewall (WAF)
In this tutorial, we'll enhance your application's security by creating a Web Application Firewall (WAF) using OpenTofu.

Why WAF?
WAF helps protect your web applications from common web exploits like SQL injection, cross-site scripting (XSS), and malicious bots. It acts as a shield, filtering out harmful traffic before it reaches your application.

Step 1: Define the Web ACL
Create a file named waf.tf and add the following code:

Terraform

resource "aws_wafv2_web_acl" "example" {
  name        = "my-waf"
  description = "My WAF"
  scope        = "REGIONAL"

  default_action {
    allow {}
  }

  visibility_config {
    cloudwatch_metrics_enabled = true
    metric_name                = "my-waf-metrics"
    sampled_requests_enabled   = true
  }
}
This defines a regional web access control list (web ACL) with a default allow action and logging enabled.

Step 2: Define a Rule Group
Create a rule group to define specific security rules. Add the following code to waf.tf:

Terraform

resource "aws_wafv2_rule_group" "example" {
  name        = "my-rule-group"
  description = "My Rule Group"
  scope        = "REGIONAL"
  capacity     = 10

  rule {
    name     = "AWSManagedRulesCommonRuleSet"
    priority = 1
    statement {
      managed_rule_group_statement {
        vendor_name = "AWS"
        name        = "AWSManagedRulesCommonRuleSet"
      }
    }
    visibility_config {
      cloudwatch_metrics_enabled = true
      metric_name                = "AWSManagedRulesCommonRuleSet"
      sampled_requests_enabled   = true
    }
  }

  visibility_config {
    cloudwatch_metrics_enabled = true
    metric_name                = "my-rule-group-metrics"
    sampled_requests_enabled   = true
  }
}
This defines a rule group with a capacity of 10 and includes the AWSManagedRulesCommonRuleSet, a pre-configured set of rules for common web exploits.

Step 3: Associate the Web ACL with Your ALB
Associate the web ACL with your Application Load Balancer. Add the following code to waf.tf:

Terraform

resource "aws_wafv2_web_acl_association" "example" {
  resource_arn = aws_lb.example.arn # Replace with your ALB ARN
  web_acl_arn  = aws_wafv2_web_acl.example.arn
}
This associates the web ACL with your ALB, enabling WAF protection for your application.

Step 4: Apply the Changes
Run the OpenTofu commands to apply your changes:

Bash

opentofu init
opentofu plan
opentofu apply
Step 5: Verify Your WAF
You can verify the WAF configuration in the AWS console by navigating to the WAF dashboard.