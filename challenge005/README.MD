As a cloud engineer you need to grant permissions to an EC2 instance to access an S3
bucket. EC2 instances, by default, do not have permission to access any S3 bucket. To
allow an EC2 instance to access an S3 bucket, you need to configure the necessary
permissions. You also need to query the S3 buckets from the EC2 instances and
manipulate the S3 bucket.
******************Hint**************
The solution involves creating an IAM role that allows EC2 instances to access S3.
This role can be attached to an EC2 instance to grant it the necessary permissions to
access an S3 bucket. To create the IAM role, you will need to define an appropriate
policy that grants the required permissions for the S3 bucket. The policy should
specify the actions that the EC2 instance is allowed to perform on the S3 bucket, such
as read, write, or delete. You will also need to specify the ARN of the S3 bucket in the
policy.
Once you have created the IAM role and attached it to the EC2 instance, you should
be able to access the S3 bucket from the EC2 instance using the AWS SDK or CLI.
Note that the IAM role must have the appropriate permissions to access the S3 bucket,
and the EC2 instance must be launched with this IAM role.
