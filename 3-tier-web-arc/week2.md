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
    --tag-specifications ResourceType=internet-gateway,Tags='[{Key=Name,Value="cloudforce-igw"}]'
```
Attach the IGW to our VPC

```
aws ec2 attach-internet-gateway --vpc-id "vpc-04e49362baefd6887" --internet-gateway-id "igw-0252d45a6bd3b915f" --region us-east-1
```

Create Private Route Tables 

```
aws ec2 create-route-table --vpc-id vpc-04e49362baefd6887
```

Create a web Server in both AZ1 and AZ2

```
aws ec2 run-instances \
--image-id ami-06e46074ae430fba6 \
--count 1 \
--instance-type t2.micro \
--key-name cloudforce \
--subnet-id subnet-0e902686c4d2890d7 \
--security-group-ids sg-0bbc0431234c68fcd \
--tag-specifications ResourceType=instance,Tags='[{Key=Name,Value="cloudforce-webserver2"}]' \
--user-data https://clouduserdata254.s3.amazonaws.com/user-data.txt

```

Create an App server in both AZs again
```
aws ec2 run-instances \
--image-id ami-0c55b159cbfafe1f0 \
--count 1 \
--instance-type t2.micro \
--key-name my-key-pair \
--output text --query 'GroupId') \
--subnet-id subnet-0123456789abcdef \
```

