## Launching an Instance from the Console

1. Open the EC2 service in the AWS Management Console.
2. Select an Amazon Machine Image, such as an Amazon Linux distribution.
3. Choose an instance type, starting with a small type for testing.
4. Create or select a key pair, and download the private key file.
5. Configure a security group allowing SSH access from a known IP address.
6. Launch the instance and wait for its status to become running.

## Connecting to the Instance

```text
chmod 400 my-key.pem
ssh -i my-key.pem ec2-user@<public-ip-address>
```

The `chmod` step restricts the key file permissions, which SSH requires before it will use the key.

## Setting Up a Python Environment

```text
sudo yum update -y
sudo yum install python3 -y
python3 --version
```

## Running a Pipeline Script

```text
# Copy the script to the instance
scp -i my-key.pem pipeline.py ec2-user@<public-ip-address>:~/

# Run it on the instance
ssh -i my-key.pem ec2-user@<public-ip-address>
python3 pipeline.py
```

## Launching an Instance with the CLI

```text
aws ec2 run-instances \
    --image-id ami-xxxxxxxxxxxx \
    --instance-type t3.micro \
    --key-name my-key \
    --security-group-ids sg-xxxxxxxxxxxx
```

## Stopping an Instance

Billing continues while an instance runs, so stopping it when not in use controls cost.

```text
aws ec2 stop-instances --instance-ids i-xxxxxxxxxxxx
```