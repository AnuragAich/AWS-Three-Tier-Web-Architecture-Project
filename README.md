# AWS Three Tier Web Architecture Project
 
## Description:
In this hands-on workshop, you'll directly build a robust three-tier web architecture in AWS. We’ll walk through the step-by-step process of setting up and configuring all the essential components: network infrastructure, security settings, application servers, and databases. By the end of the session, you'll have a fully functional and scalable web environment, with practical skills to deploy and manage it in AWS.

## Architecture Overview
![AWS Architecture - DrawIO](https://github.com/AnuragAich/AWS-Three-Tier-Web-Architecture-Project/blob/main/AWS%20Three%20Tier%20Web%20Architecture%20.png)

In this architecture, client traffic is first routed through a public-facing Application Load Balancer, which directs it to EC2 instances running the web tier. These EC2 instances host Nginx web servers that serve a React.js website and forward API requests to an internal Application Load Balancer. The internal load balancer then directs traffic to the application tier, built with Node.js, which interacts with an Aurora MySQL database configured for high availability with multi-AZ deployments. Each tier—web, application, and database—features load balancing, health checks, and autoscaling to ensure continuous availability and performance.

## Services Used
![AWS Architecture - DrawIO](https://github.com/AnuragAich/AWS-Three-Tier-Web-Architecture-Project/blob/main/Services%20Used.png)

### AWS PROJECT
---

# Creating AWS Three Tier Web Architecture & Integrating Other AWS Resources

## Step 1: Download Code from GitHub in Your Local System

## Step 2: Create Two S3 Buckets
- Create one S3 bucket for storing web-server & app-server code.
- Upload the code to your S3 from your local system.
- Create another S3 bucket for VPC flow logs.

## Step 3: Create IAM Role with Policies
- S3 read only.
- SSM managed instance core.

## Step 4: Create VPC, Subnets, IGW, NAT-GW, RT
- Enable auto-assign public IP for web-tier public subnets.
- Create flow logs for VPC & use the S3 bucket created above.

## Step 5: Create Security Groups
1. **External-Load-Balancer-SG** --> HTTP (80): 0.0.0.0/0.
2. **Web-Tier-SG** --> HTTP --> Ext-LB-SG.
3. **Internal-Load-Balancer-SG** --> HTTP --> Web-Tier-SG.
4. **App-Tier-SG** --> Port 4000 --> Internal-LB-SG.
5. **DB-Tier-SG** --> MySQL (3306) --> App-Tier-SG.

## Step 6: Create DB Subnet Group & RDS
- Create DB subnet group.
- Create RDS - Multi-AZ.
- Place them in DB subnet group created above.

## Step 7: Create Test App Server, Install Packages, Test Connections
- [Test App-Server Commands](https://github.com/AnuragAich/AWS-Three-Tier-Web-Architecture-Project/blob/main/app-server-commands)
- Create AMI.
- Create launch template using AMI.
- Create target group.
- Create internal load balancer.
- Create autoscaling group.
- Edit `nginx.conf` file in local system by adding Internal-LB-DNS & upload the file in S3.

## Step 8: Create Test Web Server, Install Packages (Nginx, Node.js (React)), Test Connections
- [Test Web-Server Commands](https://github.com/AnuragAich/AWS-Three-Tier-Web-Architecture-Project/blob/main/web-server-commands)
- Create AMI.
- Create launch template using AMI.
- Create target group.
- Create external load balancer.
- Create autoscaling group.

## Step 9: Add External-ALB-DNS Record in Route 53

## Step 10: Create CloudWatch Alarms Along with SNS

## Step 11: Create CloudTrail

## Step 12: Deleting the Entire Infrastructure
- Delete CloudFront.
- Delete CloudWatch alarms.
- Delete records from Route 53.
- Delete load balancers, target groups, ASG, launch templates.
- Delete security group.
- Delete NAT gateway (it will take 5 mins).
- Release elastic IP.
- Delete VPC.
- Delete RDS subnet group, RDS.

---


## Workshop Instructions:

See [AWS Three Tier Web Architecture](https://catalog.us-east-1.prod.workshops.aws/workshops/85cd2bb2-7f79-4e96-bdee-8078e469752a/en-US)
