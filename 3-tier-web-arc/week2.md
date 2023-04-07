# Create a 3 tier web artchitecture

Create a VPC

```
aws ec2 create-vpc \
    --cidr-block 10.1.0.0/22 \
    --tag-specifications ResourceType=vpc,Tags='[{Key=Name,Value="Cloudforce"}]'
```

Create Subnets

Create Public Subnet AZ1
```
aws ec2 create-subnet \
    --vpc-id vpc-04e49362baefd6887 \
    --cidr-block 10.1.0.0/26 \
    --availability-zone us-east-1a \
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="PublicWebServerVPC2"}]'
```

Create Public Subnet AZ2
```
aws ec2 create-subnet \
    --vpc-id vpc-04e49362baefd6887 \
    --cidr-block 10.1.0.64/26 \
    --availability-zone us-east-1b \
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="PublicWebServerVPC"}]'
```

Create Private App Server
```
aws ec2 create-subnet \
    --vpc-id vpc-04e49362baefd6887 \
    --cidr-block 10.1.2.0/26 \
    --availability-zone us-east-1a \
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="PrivateAppServer"}]'
```

Create Private App Server
```
aws ec2 create-subnet \
    --vpc-id vpc-04e49362baefd6887 \
    --cidr-block 10.1.2.64/26 \
    --availability-zone us-east-1b \
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="PrivateAppServer2"}]'
```

Create Private Rds Server
```
aws ec2 create-subnet \
    --vpc-id vpc-04e49362baefd6887 \
    --cidr-block 10.1.2.128/26 \
    --availability-zone us-east-1a \
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="PublicWebServerVPC"}]'
```

Create Private RDS Server
```
aws ec2 create-subnet \
    --vpc-id vpc-04e49362baefd6887 \
    --cidr-block 10.1.2.192/26 \
    --availability-zone us-east-1b \
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="PublicWebServerVPC"}]'
```

Create a Internet Gateway

```
aws ec2 create-internet-gateway \
    --tag-specifications ResourceType=internet-gateway,Tags='[{Key=Name,Value=cloudforce-igw}]'
```
Attach the IGW to our VPC

```
aws ec2 attach-internet-gateway --vpc-id "vpc-04e49362baefd6887" --internet-gateway-id "igw-0252d45a6bd3b915f" --region us-east-1
```

Create Private Route Tables 

```
aws ec2 create-route-table --vpc-id vpc-04e49362baefd6887
```

Create a web Server


add to user data
````
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Designing a 3 tier Aws Architecture </h1>" > /var/www/html/index.html
```
