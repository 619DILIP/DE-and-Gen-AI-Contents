## Writing a Narrow Policy

A policy granting read only access to one specific bucket.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::company-sales-data-example",
                "arn:aws:s3:::company-sales-data-example/*"
            ]
        }
    ]
}
```

Both the bucket itself and the objects within it are listed, since listing a bucket and reading its objects are separate permissions.

## Creating a Role for an EC2 Instance

1. Open the IAM service in the AWS Management Console.
2. Create a new role and select EC2 as the trusted service.
3. Attach the narrow policy defined above.
4. Give the role a descriptive name, such as `pipeline-s3-read-role`.
5. Attach the role to the EC2 instance running the pipeline.

## Using the Role from Code

No credentials appear in the code. The SDK retrieves temporary credentials from the attached role automatically.

```python
import boto3

# No keys passed in, credentials come from the instance role
s3 = boto3.client("s3")
response = s3.get_object(
    Bucket="company-sales-data-example",
    Key="raw/orders.csv"
)
```

## Verifying Permissions

```text
aws sts get-caller-identity
aws s3 ls s3://company-sales-data-example/
```

Attempting an action outside the policy should fail, which confirms the permissions are correctly scoped.

## Steps to Follow

1. List exactly which actions the application needs to perform.
2. Write a policy granting only those actions on only those resources.
3. Create a role and attach that policy.
4. Assign the role to the service that needs it.
5. Test that permitted actions succeed and non permitted actions fail.