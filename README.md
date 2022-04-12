# AWS-Elb-BeanStalk

![BeanStalk](https://user-images.githubusercontent.com/19390842/163003810-cb21c8c0-41db-4cf9-88fe-74aa2c822e89.PNG)

In this project, we are going to make an application that needs to support the high demand of a large number of users accessing it simultaneously. This application will be used in The CloudBootcamp Conference, which is a conference that will have participants from allover the world. More than 10,000 people are expected to participate, both in person and online. This event will be broadcast over the internet and in person. At some point during the event, 10 vouchers will be drawn for 3 Cloud certifications. The audience will register the email to guarantee participation in the raffle. The objective of this project is to create an application with the necessary components for the participants to successfully access the page. For this, we will rely on AWS. We are going to use ElasticBeanstalk to deploy a web application and DynamoDB to store the emails. Let's rely on CloudFront to cache static and dynamicfiles to an EdgeLocation close to the user. This application will need to be responsive for Desktop and Mobile access.

Code To Run
Hands-on Project Solution - Part 1

# Steps on DynamoDB

- Create a new table
-- name: users
-- primary key: email

# Steps on Elastic Beanstalk

- Platform: Python 3.7+

- Application code:
-- Upload your code: https://tcb-bootcamps.s3.amazonaws.com/bootcamp-aws/en/tcb-conf-app-EN.zip

Click in 'Configure more options':

- Presets:
-- Configuration presets: High availability

- Software:
-- Environment properties:
--- AWS_REGION = us-east-1

- Instances:
-- Root volume type: General Purpose SSD - 8 GB

- Capacity:
-- Instances Min: 2
-- Instances Max: 4
-- Instance type: t2-micro
-- Scaling triggers:
--- CPUUtilization
--- Unit: Percent
--- Period: 1 Min
--- Breach durantion: 1 Min
--- Upper threshold: 50
--- Lower threshold: 40

- Security:
-- Select SSH key

- Networking:
-- VPC: Default:
-- Add IP Public
-- Select all subnets

- Create App

- Once the deploy completes, access the application and simulate a record insertion

- Investigate the error in the logs

- Add the permission AmazonDynamoDBFullAccess on the EC2 associate role in IAM.

- Try to insert the registry once again. It should be sucessful.


Hands-on Project Solution - Part 2

- Create CloudFront distribution
- Allowed HTTP methods:  GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE


Hands-on Project Solution - Part 3

Perform load testing.

- Install the stress tool to perform the load testing

sudo amazon-linux-extras install epel -y
sudo yum install stress -y

stress -c 4

- Explore the resources created by the AWS Elastic Beanstalk (EC2, ELB, Auto Scaling Group, Cloud Watch resources) and also the auto scaling process

- Once you finish exploring it, please remove the Elastic Beanstalk application, Elastic Beanstalk environment , disable and delete the CloudFront distribution and finally delete the DynamoDB users table
