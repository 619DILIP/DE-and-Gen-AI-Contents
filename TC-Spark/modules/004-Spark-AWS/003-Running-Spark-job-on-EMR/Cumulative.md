# Cumulative for the Running Spark job on EMR
<details><summary>Prerequisites and Learning Objectives</summary>

## Prerequisites 

- Sign up for an AWS account

## Objectives

- To learn how to run a Spark job in the EMR cluster in AWS.

---

</details>
<details><summary>Description</summary>

## Description

- The first thing to do for running your Spark job is to create an S3 bucket. Follow the steps below to easily create an S3 bucket using the console.

  - Sign in to the AWS Management Console and open the Amazon S3 console at [S3](https://console.aws.amazon.com/s3/)
   
  - Choose the `Create bucket` option.

  - Enter a name for your bucket, choose its AWS region, and click next.

  - You can click next on the `Set properties page` and `Set permissions page` if you want to use the default values mentioned there.

  - On the Review page, verify the settings and choose Create bucket.

- After creating the S3 bucket, upload your file to the S3 bucket by creating a folder there.


**Launch an Amazon EMR Cluster and Submit the Spark Job** 

- Go to the Amazon EMR console and `change the region` in which you want to deploy the cluster.

- Choose `Create cluster` 

- In the settings, enter the `Cluster name`, `choose the S3 bucket you created`, and check `Step execution`. 

- In the `Software Configuration` section, use the default release.

- In the `Hardware Configuration` section, choose the instance type and the number of instances.

- In the `Add steps` section, select `Spark` for `Application`.

- Finally, click on `Create cluster` and click on `the refresh icon` to see the status changing from Starting to Running to Terminating — All steps completed.

- Now go back to the S3 console, and you will see the output directory in which the results have been stored. You can click on it and download its contents.

---

</details>


<details><summary>Implementation</summary> 

## Implementation

- Creating an S3 bucket using the CLI 
```
aws s3api create-bucket \
     --bucket my-second-emr-bucket \
     --region us-east-2 \
     --create-bucket-configuration LocationConstraint=us-east-2
```

- To upload the file to the S3 bucket 
```
aws s3 sync tutorialEMR/ s3://my-second-emr-bucket/tutorialEMR
```

- Create the cluster and submit the Spark step
```
aws emr create-cluster \
     --name "Cluster" \
     --release-label emr-5.9.0 \
     --instance-type m4.large --instance-count 3 \
     --applications Name=Spark \
     --steps Type=Spark,Name="Spark Program",ActionOnFailure=CONTINUE,Args=["--class", "com.jeanr84.sparkjob.SparkJob", "s3://my-second-emr-bucket/tutorialEMR/spark-job-0.0.1-SNAPSHOT.jar", "s3://my-second-emr-bucket/tutorialEMR/input.txt", "s3://my-second-emr-bucket/tutorialEMR/output"] \
     --use-default-roles \
     --ec2-attributes SubnetId=subnet-e7ba9d9c \
     --auto-terminate
```

- Download the results repository locally
```
aws s3 sync s3://my-second-emr-bucket/tutorialEMR/output output
```
</details>
<details><summary>Summary</summary> 

## Summary 

- Log in to Amazon AWS and choose the `Create bucket` option in the S3 console. Enter the name of the bucket and choose its AWS region. 

- After creating the S3 bucket, upload your file to the S3 bucket by creating a folder there.

- In the EMR console, choose `Create cluster` to open the Quick Options wizard. Then enter the name of your cluster, choose the S3 bucket you created, and select the Spark option under applications to install Spark on your cluster. 

- For Software Configuration, choose a Release option. After that, select other necessary options and then click on the Create cluster option.

- After clicking on Create cluster, go back to the S3 console, and you will see the output directory there.

---

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
