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
--image-id ami-06e46074ae430fba6 \
--count 1 \
--instance-type t2.micro \
--key-name cloudforce \
--subnet-id subnet-04fcbc024f42beb38 \
--security-group-ids sg-0bbc0431234c68fcd \
--tag-specifications ResourceType=instance,Tags='[{Key=Name,Value="Cloudforce-Appserver2"}]' 

```

Creating An RDS multi AZ DB

```
aws rds create-db-instance \
    --db-name cloudForceDB
    --allocated-storage 20
    --db-instance-class db.m6i.large
    --engine MySQL8.0.32
    --master-username cloudsky
    --master-user-password cloudforce
    --db-security-groups DBSecurityGroup
    --vpc-security-group-ids 
    --availability-zone us-east-1a
    --db-subnet-group-name <value>]
[--db-parameter-group-name <value>]
[--backup-retention-period <value>]
[--preferred-backup-window <value>]
[--port <value>]
[--multi-az | --no-multi-az]
[--engine-version <value>]
[--auto-minor-version-upgrade | --no-auto-minor-version-upgrade]
[--license-model <value>]
[--iops <value>]
[--option-group-name <value>]
[--character-set-name <value>]
[--nchar-character-set-name <value>]
[--publicly-accessible | --no-publicly-accessible]
[--tags <value>]
[--db-cluster-identifier <value>]
[--storage-type <value>]
[--tde-credential-arn <value>]
[--tde-credential-password <value>]
[--storage-encrypted | --no-storage-encrypted]
[--kms-key-id <value>]
[--domain <value>]
[--copy-tags-to-snapshot | --no-copy-tags-to-snapshot]
[--monitoring-interval <value>]
[--monitoring-role-arn <value>]
[--domain-iam-role-name <value>]
[--promotion-tier <value>]
[--timezone <value>]
[--enable-iam-database-authentication | --no-enable-iam-database-authentication]
[--enable-performance-insights | --no-enable-performance-insights]
[--performance-insights-kms-key-id <value>]
[--performance-insights-retention-period <value>]
[--enable-cloudwatch-logs-exports <value>]
[--processor-features <value>]
[--deletion-protection | --no-deletion-protection]
[--max-allocated-storage <value>]
[--enable-customer-owned-ip | --no-enable-customer-owned-ip]
[--custom-iam-instance-profile <value>]
[--backup-target <value>]
[--network-type <value>]
[--storage-throughput <value>]
[--manage-master-user-password | --no-manage-master-user-password]
[--master-user-secret-kms-key-id <value>]
[--ca-certificate-identifier <value>]
[--cli-input-json <value>]
[--generate-cli-skeleton <value>]
[--debug]
[--endpoint-url <value>]
[--no-verify-ssl]
[--no-paginate]
[--output <value>]
[--query <value>]
[--profile <value>]
[--region <value>]
[--version <value>]
[--color <value>]
[--no-sign-request]
[--ca-bundle <value>]
[--cli-read-timeout <value>]
[--cli-connect-timeout <value>]
```
