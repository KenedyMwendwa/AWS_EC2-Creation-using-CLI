# Creating an EC2 Instance in AWS Using CLI

This guide will walk you through the process of creating an EC2 instance in AWS using the AWS Command Line Interface (CLI). You will need to perform the following steps:

1. **Get VPC ID and Subnet ID**
    - Before creating resources, you need the VPC ID and Subnet ID.
    - Run the following commands:
        ```bash
        aws ec2 describe-vpcs
        aws ec2 describe-subnets --filters "Name=vpc-id,Values=your-vpc-id"
        ```
2. **Get AMI ID**
    - Identify the AMI ID of the Linux image you want to use.
    - Run the following command:
        ```bash
        aws ec2 describe-images --owners amazon --filters "Name=name,Values=your-ami-name"
        ```
3. **Create Security Group**
    - Create a security group and configure inbound rules to allow SSH access.
    - Run the following commands:
        ```bash
        aws ec2 create-security-group \
            --group-name your-sg-name \
            --description "Security group for EC2 instance" \
            --vpc-id your-vpc-id

        aws ec2 authorize-security-group-ingress \
            --group-id your-sg-id \
            --protocol tcp \
            --port 22 \
            --cidr 0.0.0.0/0
        ```
4. **Create SSH Key Pair**
    - Create an SSH key pair for accessing the EC2 instance.
    - Run the following command:
        ```bash
        aws ec2 create-key-pair \
            --key-name your-key-name \
            --query 'KeyMaterial' \
            --output text > your-key.pem
        ```
5. **Launch EC2 Instance**
    - Finally, launch the EC2 instance using the provided AMI, security group, subnet, and key pair.
    - Run the following command:
        ```bash
        aws ec2 run-instances \
            --image-id your-ami-id \
            --count 1 \
            --instance-type t2.micro \
            --key-name your-key-name \
            --security-group-ids your-sg-id \
            --subnet-id your-subnet-id
        ```

Make sure to replace placeholders like `your-vpc-id`, `your-ami-name`, etc., with your actual values. Adjust the parameters according to your specific requirements.

Feel free to reach out if you need further assistance!
