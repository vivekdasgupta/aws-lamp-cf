# AWS Cloudformation template for LAMP Stack

  This template will create a redundant, secure and cost effective lamp stack in AWS.

  Assumption : This stack is to be created in Sydney region.


# Design / Specifications

# Cost

  The aim here is to provide a minimal cost solution. However the solution needs to be highly available at the same time. For redundancy there are 3 availability zones in AWS Sydney region. I am utilizing 2 of them to provide redundancy at lower cost. The instances types used are "small" as well and can be scaled up or down based on load.

# Redundancy

  The PHP application will run on multiple EC2 instances across availability zones. The instances will be a part of target group.

  AWS Application Load Balancer  (ALB) will be used to provide redundancy and load balancing. It will distribute traffic onto the instances at the backend.

  The AWS RDS (MySQL) will also be a multi-AZ database, hence redundant.


# Security

  Security groups will limit access to instances and the load balancers.  The load balancer will be available publicly over internet, but will be accessible only on port 80. The instances will be reachable on port 80 via this load balancer only. The instances will also allow access on port 22 (SSH) for any maintenance/troubleshooting. The CIDR for internet access is a param for this CF stack and can be restricted to appropriate range for security.   MySQL database will only allow connection on port 3306 from the instances.

  In a real world production environment, the Application Load Balancer can be restricted to only allow HTTPS connections on port 443, for public facing apps. This will require a SSL certificate to be attached to the Load Balancer.

# PHP app

The PHP app is a simple app which will print the current date/time and few other config details. It also connects to the database and prints the information that it connected successfully.
