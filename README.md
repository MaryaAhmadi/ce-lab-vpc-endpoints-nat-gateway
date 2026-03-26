# Lab M7.08 - VPC Endpoints and NAT Gateway Optimization

**Repository:** https://github.com/MaryaAhmadi/ce-lab-vpc-endpoints-nat-gateway.git


**Activity Type:** Individual  
**Estimated Time:** 45-60 minutes

##📌 Overview
This lab demonstrates how to reduce AWS networking costs by replacing NAT Gateway traffic with VPC Gateway Endpoints for Amazon S3 and DynamoDB.
You will deploy a VPC with private resources, measure NAT Gateway usage, implement endpoints, and compare cost and performance before and after optimization.

## 🎯 Learning Objectives
Understand how NAT Gateway data processing charges accumulate
Deploy Gateway VPC Endpoints for S3 and DynamoDB
Analyze CloudWatch metrics for NAT Gateway traffic
Compare infrastructure behavior before and after optimization
Calculate cost savings from reduced NAT Gateway usage
Evaluate when to use Gateway vs Interface endpoints

## 🧰 Prerequisites
- AWS CLI installed and configured
- AWS account with permissions for:
- EC2
- S3
- DynamoDB
- CloudWatch
- IAM
- Basic knowledge of VPC networking (Module 7 Day 4)

## 🏗️ Architecture
- The lab environment includes:
- VPC with public and private subnets
- Internet Gateway (IGW)
- NAT Gateway for outbound traffic
- EC2 instance in a private subnet
- Gateway Endpoints for:
- Amazon S3
- Amazon DynamoDB

## ⚙️ Implementation Steps
1. VPC Setup
Created a VPC with CIDR 10.0.0.0/16
Configured public and private subnets
Enabled DNS hostnames

2. Networking Components
Attached Internet Gateway
Created NAT Gateway in public subnet
Configured route tables:
Public subnet → IGW
Private subnet → NAT Gateway

3. EC2 Deployment
Launched EC2 instance in private subnet
Attached IAM role with:
S3 access
DynamoDB access
SSM access

4. Baseline Traffic Generation
Created S3 bucket and uploaded 10MB file
Performed multiple downloads from S3
Inserted and scanned data in DynamoDB
Observed NAT Gateway traffic via CloudWatch

5. VPC Endpoint Deployment
Created S3 Gateway Endpoint
Created DynamoDB Gateway Endpoint
Associated endpoints with private route table

6. Post-Optimization Testing
Re-ran S3 and DynamoDB operations
Verified traffic bypassed NAT Gateway


## 📊 Results
- NAT Gateway Metrics Comparison
- Metric	Before Endpoints	After Endpoints
- BytesOutToDestination	~11 MB	~13 KB
- BytesOutToSource	~88 MB	~17 KB

##Key Observations
- Significant reduction in NAT Gateway traffic
- S3 and DynamoDB traffic no longer routed through NAT
- Remaining traffic is minimal (system-level)

## 💰 Cost Analysis

Before Optimization
S3 traffic: $22.50/month
DynamoDB traffic: $2.25/month
Other traffic: $0.45/month
NAT Gateway hourly: $32.85/month
Total: $58.05/month

After Optimization
S3: $0.00
DynamoDB: $0.00
Other traffic: $0.45/month
NAT Gateway hourly: $32.85/month

Total: $33.30/month

💡 Savings
Monthly savings: $24.75
Annual savings: $297

## 🧠 Key Takeaways
- Gateway endpoints for S3 and DynamoDB are free
- They eliminate NAT Gateway data processing charges
- CloudWatch metrics clearly show traffic reduction
- NAT Gateway still incurs hourly cost even with endpoints
- Interface endpoints can further reduce costs if NAT is no longer needed

## 📸 Screenshots 

Include:
- cloudwatch-before.png
- cloudwatch-after.png
- route-table-endpoint.png
- vpc-endpoints.png
- nat-gateway.png
- ec2-private-instance.png
- ssm-session.png
- s3-bucket.png
- dynamodb-table.png


## ✅ Verification Checklist
 ✅ VPC and networking configured
 ✅ NAT Gateway deployed
 ✅ Baseline traffic generated
 ✅ CloudWatch metrics captured
 ✅ VPC endpoints created
 ✅ Post-optimization metrics analyzed
 ✅ Cost savings calculated

##📚 Additional Resources
AWS VPC Endpoints Documentation
AWS NAT Gateway Pricing
Module 7 Day 4 lessons

## 🚀 Conclusion
This lab demonstrates how a simple architectural improvement—adding Gateway VPC endpoints—can significantly reduce AWS networking costs while improving performance and security.


