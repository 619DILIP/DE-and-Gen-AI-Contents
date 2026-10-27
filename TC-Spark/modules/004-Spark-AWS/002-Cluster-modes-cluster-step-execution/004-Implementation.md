## Implementation

**To enable step execution using the Amazon CLI**

- Specify the `--auto-terminate` parameter when you use the create-cluster command
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

---

