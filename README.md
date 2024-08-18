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

**Task 2:** Create a Security Group 

   1. Make sure you are in the N.Virginia Region. 
   
   2. Navigate to EC2 by clicking on the Services menu available under the Compute section. 
   
   3. On the left panel menu, select the Security Groups under the Network & Security section. 
   
   4. Click on the Create security group button.
   
   5. Under Basic details:  <br> 
   
      Security group name: Enter My-SG <br>
      Description: Enter Security group for Load balancer and Launch Template  <br>
      VPC: Select Default VPC <br>
   
   6. Click on the Add rule button under Inbound rules.  <br>
   
      Type : Select HTTP  <br>
      Source : Select Anywhere Ipv4  <br>
   
   7. Leave everything as default and click on the Create security group button. <br>

**Task 3:** Create a Launch Template 

   1. In the left navigation pane (scroll down) within Instances, click on the Launch templates. 
   
   2. Click on the Create launch template button. 

   3. Under Launch template name and description section: <br>

      Launch template name: Enter labsLC <br>
      Leave other options as default. <br>
      
   4. Under Launch template contents: <br>

      Select Amazon Linux from the Quick Start <br>
      Amazon machine image (AMI): Select Amazon Linux 2 AMI (HVM), SSD Volume Type <br>

   5. Under Instance type: <br>

      Select t2.micro from the below list.
      
   6. Key pair (Login): Select Keep it as default

   7. Security groups: Select My-SG from the list <br>

         Leave all other options as default. <br> 
         Expand the option of Advanced details, Go to the User data, and paste the below script.  <br>

         ```
            #!/bin/bash
            
            sudo su
            
            yum update -y
            yum install -y httpd
            
            systemctl start httpd
            systemctl enable httpd
            
            echo "<html> <h1> Hello from Renato's Lab!! </h1> </html>" > /var/www/html/index.html

         ```
   **Task 4:** Create Targte group and Load Balancer 
   
      1. In the EC2 console, navigate to Target Groups from the left navigation panel. 
      
      2. Click on Create Target Group button. 

      3. Target Type: Select Instances 

            Name: Enter web-server-TG 
            Protocol: Choose HTTP 
            Port : Enter 80 
      
      4. Health check: 
      
            Protocol: Select HTTP 
            Path: Enter /index.html 

      5. Click on the Next button. 

      6. Leave this page as default and click on Create target group button. 

      7. Now to create a Load balancer. 

      8. In the EC2 console, navigate to Load balancers in the left-side panel. 

      9. Click on Create load balancer button at the top-left to create a new load balancer for our web servers.

      10. On the next screen, choose Create button under Application Load Balancer since we are testing the high availability of the web application. 

      11. Basic configuration: 
      
            Name: Enter Web-server-LB 
            Scheme: Select Internet-facing 
            IP address type: Choose IPv4  

      12. Availability Zones 

            VPC: Choose Default 
            Availability Zones  : Select us-east-1a and us-east-1b. 

      13. Security Groups: 

            Remove the default one and choose My-SG 

      14. In the listener part select the Target group that you have created earlier. 

      15. Click on Create Load Balancer button. 

      16. You have successfully created the Application Load balancer. 
      
      17. Wait for 2 to 3 minutes for the load balancer to become Active. 

   **Task 5:** Create an Auto Scaling Group 
   
      1. An Auto Scaling group is a scalable collection of EC2 instances. When you create an Auto Scaling group, you include information such as the subnets for the instances and the number of instances the group must maintain at all times. 
      
      2. Go to the left menu under EC2 and choose Auto Scaling Groups under Auto Scaling. 
      
      3. Click on the Create Auto Scaling group button. 

      4. Step 1 : Choose launch template or configuration 

         Auto Scaling group name : Enter My-ASG 
         Select the Launch template labsLC from the list and click on the Next button. 

      5. Step 2: Configure settings 

         VPC: Select the Default VPC from the list. 
         Subnet: Select Subnet of us-east-1a and us-east-1b 
         Click on the Next button. 

      6. Step 3: Configure advanced options 

         Load balancing - optional: Attach to an existing load balancer 
         Attach to an existing load balancer: Choose from your load balancer target groups 
         Existing load balancer target groups: web-server-TG 

      7. Health check - optional:  

         Health check type: EC2 (default) and Check the Turn on Elastic Load Balancing health checks checkbox. 
         Health check grace period: 60 seconds
         
      8. Click on the Next button. 
