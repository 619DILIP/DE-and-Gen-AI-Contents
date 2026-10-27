## Implementation

- Creating s3 bucket using CLI 
```
aws s3api create-bucket \
     --bucket my-second-emr-bucket \
     --region us-east-2 \
     --create-bucket-configuration LocationConstraint=us-east-2
```

- To upload the file in s3 bucket 
```
aws s3 sync tutorialEMR/ s3://my-second-emr-bucket/tutorialEMR
```

- Create the cluster and submit the Spark step
```
aws emr create-cluster \
     --name “Cluster” \
     --release-label emr-5.9.0 \
     --instance-type m4.large — instance-count 3 \
     --applications Name=Spark \
     --steps Type=Spark,Name=”Spark Program”,ActionOnFailure=CONTINUE,Args=[ — class,com.jeanr84.sparkjob.SparkJob,s3://my-second-emr-bucket/tutorialEMR/spark-job-0.0.1-SNAPSHOT.jar,s3://my-second-emr-bucket/tutorialEMR/input.txt,s3://my-second-emr-bucket/tutorialEMR/output] \
     --use-default-roles \
     --ec2-attributes SubnetId=subnet-e7ba9d9c \
     --auto-terminate
```

- Download locally the result repository
```
aws s3 sync s3://my-second-emr-bucket/tutorialEMR/output output
```
