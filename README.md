# Scalability and Security for LojaOnline]

# Project: Scalability and Security for LojaOnline

## Background
LojaOnline is a small e-commerce business that, due to its excellent customer service and unique products, began to grow rapidly. With this growth, the company noticed that its website was starting to experience performance issues, especially during traffic spikes caused by promotional campaigns and holidays. Additionally, the company was concerned about data security and protection against cyber-attacks like SQL injections and malicious scripts.

LojaOnline needed a solution that would ensure their website was always available, even during peak traffic times, and that would protect their operations from cyber threats. This is where we came in with an AWS-based solution to address these challenges.

## Challenges
1. **Scalability:** During marketing campaigns and promotions, the site experienced a significant amount of traffic, overloading the servers and resulting in slowdowns or even site crashes.
   
2. **Security:** LojaOnline was vulnerable to common web attacks such as SQL injection and cross-site scripting, which could compromise customer data and the integrity of the business.

3. **Monitoring:** There was a lack of visibility into the website's performance and traffic behavior, making it difficult to identify issues before they affected end-users.

## Implemented Solution
To address these challenges, we designed a solution using AWS services, specifically EC2 Auto Scaling, Application Load Balancer (ALB), Web Application Firewall (WAF), and CloudWatch for monitoring.

### 1. EC2 Auto Scaling
We implemented an Auto Scaling configuration to ensure that LojaOnline’s website could automatically handle traffic spikes. This was done by creating a Launch Template that defines the AMI, instance type, security group, and other essential settings. Auto Scaling was configured to maintain a minimum and desired capacity during normal periods and automatically scale out when traffic increased, ensuring the site remained fast and responsive.

### 2. Application Load Balancer
To efficiently distribute traffic and ensure high availability, we deployed an ALB in front of the web servers. The ALB distributes user requests among the EC2 instances, ensuring no single instance is overloaded, improving the site’s resilience.

### 3. AWS WAF
Security was enhanced by implementing AWS WAF. We created custom rules to block SQL injection attempts and cross-site scripting, protecting the site from common web threats. This allowed LojaOnline to have complete control over how traffic reached the site, blocking attacks before they even hit the server.

### 4. CloudWatch
Finally, to ensure LojaOnline had full visibility into the site’s performance, we implemented CloudWatch. We configured custom alarms and dashboards to monitor critical metrics like EC2 instance health, ALB latency, and traffic patterns. This enabled LojaOnline’s IT team to quickly identify and respond to potential issues before they impacted customers.

## Results
With the new AWS infrastructure, LojaOnline experienced a significant improvement in website performance and availability. During the last promotional campaign, the site was able to handle a 300% increase in traffic without any interruptions or slowdowns. Additionally, with WAF rules in place, LojaOnline blocked multiple attack attempts, ensuring the security of customer data.

LojaOnline now operates with the confidence that its website can grow alongside the business without compromising customer experience or security.


![Architecture Diagram](https://github.com/renatomateusx/Scalability-and-Security-for-LojaOnline/blob/master/Scalability-and-Security-for-LojaOnline-arch.png)

## Steps to reproduce the result

## Project Steps
**Task 1:** Sign in to AWS Management Console
Click on the Open Console  button, and you will get redirected to AWS Console in a new browser tab.
On the AWS sign-in page, 
Leave the Account ID as default. Never edit/remove the 12-digit Account ID present in the AWS Console. otherwise, you cannot proceed with the project.
Now copy your Username and Password in the Project Console to the IAM Username and Password in AWS Console and click on the Sign in button.
Once Signed in to the AWS Management Console, Make the default AWS Region as US East (N. Virginia) us-east-1.

**Task 2:** Create a Security Group 

1. Make sure you are in the N.Virginia Region. 

2. Navigate to EC2 by clicking on the Services menu available under the Compute section. 

3. On the left panel menu, select the Security Groups under the Network & Security section. 

4. Click on the Create security group button. 
