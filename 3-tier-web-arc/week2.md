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
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="PublicWebServerVPC"}]'
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
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="PublicWebServerVPC"}]'
```

Create Private RDS Server
```
aws ec2 create-subnet \
    --vpc-id vpc-04e49362baefd6887 \
    --cidr-block 10.1.2.192/26 \
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="PublicWebServerVPC"}]'
```

