Weekly Challenge 1

Create a CloudFormation template that launches 10 EC2 instances and sets up an Apache web server within a VPC. The template should also create two subnets within the VPC, one for public-facing resources and one for private resources. The EC2 instances should be placed in the private subnet and the Apache web server should be accessible from the Internet through a public subnet.

Guidelines

Guidelines:

The VPC should have a CIDR block of 10.0.0.0/16.

The public subnet should have a CIDR block of 10.0.1.0/24 and the private subnet should have a CIDR block of 10.0.2.0/24.

The EC2 instances should use an Amazon Linux 2 AMI and should be t2.micro type.

The EC2 instances should be accessible through SSH using an existing key pair.

The Apache web server should be installed on the EC2 instances and should display a default "Welcome to Apache" page when accessed from a web browser.

The CloudFormation template should include the creation of all necessary security groups, network interfaces, and routing tables.

The CloudFormation template should be written in JSON or YAML.

The 10 EC2 instances should be created in an Auto Scaling Group and be behind a Load Balancer to handle incoming traffic.