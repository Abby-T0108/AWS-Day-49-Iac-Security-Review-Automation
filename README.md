# AWS-Day-49-Iac-Security-Review-Automation

Infrastructure-as-Code Security Review & Hardening

Project Overview
Performed security review of AWS CloudFormation templates using automated scanning tools to identify and remediate security misconfigurations before deployment.

Challenge
Infrastructure code often contains security vulnerabilities that can lead to:
* Data breaches from misconfigured S3 buckets
* Unauthorized access through overly permissive IAM roles
* Server compromise from open security groups
* Compliance violations

What I Did
* Analyzed CloudFormation templates for security issues
* Automated security scanning with Checkov and cfn-lint
* Identified 6+ critical security misconfigurations
* Remediated all issues following AWS best practices
* Created secure baseline template

Tools & Technologies
* Checkov: Policy-as-code security scanner
* cfn-lint: CloudFormation linter
* AWS CloudFormation: Infrastructure-as-Code
* Python: Tool installation and automation
* VS Code: Development environment

Security Issues Found & Fixed
1. Public S3 Bucket (CRITICAL) 
Issue: S3 bucket allowed public internet access
Fix: Enabled S3 Block Public Access on all settings
Impact: Prevented potential data breach

2. Open Security Group (CRITICAL) 
Issue: SSH and RDP ports open to 0.0.0.0/0
Fix: Restricted SSH to specific IP address only
Impact: Eliminated brute-force attack vector

3. Excessive IAM Permissions (HIGH) 
Issue: IAM role had AdministratorAccess
Fix: Created custom policy with least privilege (S3 read/write only)
Impact: Reduced blast radius of potential compromise

4. Missing S3 Versioning (MEDIUM)
Issue: No versioning enabled on S3 bucket
Fix: Enabled versioning for data recovery
Impact: Protection against accidental deletion

5. No Access Logging (MEDIUM)
Issue: S3 bucket had no access logs
Fix: Configured access logging to separate bucket
Impact: Enabled audit trail for compliance

How to Reproduce
Prerequisites
pip install checkov cfn-lint

Run Security Scans
checkov -f insecure-template.yaml
checkov -f secure-template.yaml
cfn-lint insecure-template.yaml
cfn-lint secure-template.yaml

Key Learnings
* Infrastructure security must be automated
* Shift-left security catches issues before deployment
* Policy-as-code tools make security consistent and repeatable
* Least privilege should always be applied
* Encryption, logging, and versioning should be defaults

Real-World Application
This process prevents:
* Capital One-style S3 data breaches
* Uber-style Credential exposure
* AWS account compromise from open security groups
* Compliance violations from missing audit logs

Skills Demonstrated
CloudFormation
Automated security scanning
Security policy enforcement
Risk assessment
Security documentation
Remediation and hardening
