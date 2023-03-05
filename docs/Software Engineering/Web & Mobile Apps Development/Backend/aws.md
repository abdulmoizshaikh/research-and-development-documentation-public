# AMAZON WEB SERVICES

**What is AWS cloud practitioner?**

An Amazon Web Services (AWS) certified cloud practitioner is defined as a technical professional who is well-versed with cloud computing and has foundational knowledge of AWS to support cloud operations across various verticals and industries.12-Apr-2022

https://www.spiceworks.com/tech/cloud/articles/aws-cloud-practitioner/#:~:text=An%20Amazon%20Web%20Services%20(AWS,across%20various%20verticals%20and%20industries.

## Free tier

As part of the AWS Free Tier, you can get started with Amazon EC2 for free. This includes 750 hours of Linux and Windows t2.micro instances (t3.micro for the regions in which t2.micro is unavailable), each month for one year. **To stay within the Free Tier, use only EC2 Micro instances.**

### EC2 or AWS Fargate?

There are two major models for how to run your containers on AWS:

- **EC2** (Deploy and manage your own cluster of EC2 instances for running the containers)
- **AWS Fargate** (Run containers directly, without any EC2 instances)

Both are completely valid techniques for operating your containers in a scalable and reliable fashion. Which one you pick primarily depends on which factors you want to optimize for.

#### Pricing

With the EC2 launch type billing is based on the cost of the underlying EC2 instances. This allows you to optimize price by taking advantage of billing models such as spot instances (bid a low price for an instance), or reserved instances (get a flat discount for committing to an instance for a certain time period). However, it is your responsibility to make sure that your containers are densely packed onto instances to get the best use out of them, otherwise you will be wasting money.

With the AWS Fargate launch type billing is based on how many CPU cores, and gigabytes of memory your task requires, per second. You only ever pay for what your task uses, no more paying for EC2 capacity that goes unused.

https://containersonaws.com/introduction/ec2-or-aws-fargate/

How much is AWS EC2 monthly?

The instances are available in three sizes (micro, small, and medium) with On-Demand prices that start at $0.013 per hour ($**9.50 per month**). You can also gain access to a pair of t2. micro instances (one running Linux and another running Windows) at no charge via the AWS Free Usage Tier.01-Jul-2014

Which AWS services are free?

Some of the services like **Amazon EC2, Amazon Cloudfront, Amazon S3** are free for a 12 month period, some like Amazom DynamoDB, Amazon Chime are always free, and others like Amazon Redshift, Amazon Lightsail have short term free trials, typically 30-60 days.

What is EC2 stands for?

Amazon Elastic Compute Cloud

**Amazon Elastic Compute Cloud** (Amazon EC2) provides scalable computing capacity in the Amazon Web Services (AWS) Cloud.

How long is AWS free?

for 12 months

When you create an AWS account, you're automatically signed up for the AWS Free Tier for **12 months**. The AWS Free Tier allows you to try some AWS services free of charge within certain usage limits.

Is Amazon EC2 really free?

Amazon EC2 pricing. **Amazon EC2 is free to try**. There are multiple ways to pay for Amazon EC2 instances: On-Demand, Savings Plans, Reserved Instances, and Spot Instances. You can also pay for Dedicated Hosts, which provide EC2 instance capacity on physical servers dedicated for your use.

Does AWS charge automatically?

**Amazon Web Services automatically charges the credit card that you provided when you sign up for an AWS account**. You can view or update your credit card information at any time, including designating a different credit card for AWS to charge. You can do this on the Payment Methods page in the Billing console.

Can we use AWS for free for students?

**There is no cost to join** and AWS Educate provides hands-on access to AWS technology, training resources, course content and collaboration forums. Students and educators apply online at www.awseducate.com in order to access: Grants for free usage of AWS services.

## AWS Educate

https://aws.amazon.com/education/awseducate/

### Introduction to the AWS Management Console

#### AWS Pricing

**How do you pay for AWS?**

1. **Pay-as-you-go**

   Pay-as-you-go allows you to easily adapt to changing business needs without overcommitting budgets and improving your responsiveness to changes. With a pay-as-you-go model, you can adapt your business depending on need and not on forecasts, reducing the risk of overprovisioning or missing capacity.

2. **Save when you commit**
   For AWS Compute and AWS Machine Learning, Savings Plans offer savings over On-Demand in exchange for a commitment to use a specific amount (measured in $/hour) of an AWS service or a category of services, for a one- or three-year period.

3. **Pay less by using more**

   With AWS, you can get volume based discounts and realize important savings as your usage increases. For services such as S3, pricing is tiered, meaning the more you use, the less you pay per GB. AWS also gives you options to acquire services that help you address your business needs.

https://aws.amazon.com/pricing/?aws-products-pricing.sort-by=item.additionalFields.productNameLowercase&aws-products-pricing.sort-order=asc&awsf.Free%20Tier%20Type=*all&awsf.tech-category=*all

#### **What does terminating an EC2 instance do?**

OR what is termination provision meaning in ec2

Terminate Instance

When you terminate an EC2 instance, **the instance will be shutdown and the virtual machine that was provisioned for you will be permanently taken away and you will no longer be charged for instance usage**. Any data that was stored locally on the instance will be lost.

https://docs.rightscale.com/faq/clouds/aws/Whats_the_difference_between_Terminating_and_Stopping_an_EC2_Instance.html

#### **Terminate your instance**

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/terminating-instances.html

#### **Security Groups**:

you will not charge for 1 by default security group section selecting when creating new ec2 instance

https://awseducate.instructure.com/courses/744/pages/introduction-to-the-aws-management-console?module_item_id=13987

**Key Pair**

Key Pair setup also not charge you anything

#### **How to setup billing alerts on AWS**

[ AWS 3 ] Create AWS billing alert for your free tier account

https://www.youtube.com/watch?v=pXTxmXhRZV4&ab_channel=JustmeandOpensource

#### What is root user and iam user in aws

There are two different types of users in AWS. You are either the account owner (root user) or you are an AWS Identity and Access Management (IAM) user. **The root user is created when the AWS account is created.** **IAM users are created by the root user or an IAM administrator for the account**.

#### What is difference between ECS and EC2?

For example, when comparing ECS vs. EC2, **ECS is primarily used to orchestrate Docker containers and EC2 is a computing service that enables applications to run on AWS**. ECS resources are scalable, just like EC2. However, ECS scales container clusters on-demand, rather than scaling compute resources like EC2.

How to deploy my docker app to aws

Deploy Docker Containers

https://www.amazonaws.cn/en/getting-started/tutorials/deploy-docker-containers/

sweet connect k backend pe use hora hi hy
AWS ki service hy paid hy
AWS fargate (isme local container bnte hain jo k as it is server pe deploy ho jata hy docker container)

https://aws.amazon.com/fargate/
