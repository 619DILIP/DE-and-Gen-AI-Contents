# Cumulative for the Cluster Modes Cluster Step Execution
<details><summary>Prerequisites and Learning Objectives</summary>

## Prerequisites 

- Sign up for an AWS account.

## Objectives

- To learn how to use step execution in the cluster in AWS.

---
</details>
<details><summary>Description</summary>

## Description

- **To enable step execution using Quick in the AWS Console**

  - Open the Amazon EMR console at [EMR](https://console.amazonaws.cn/emr).

  - Choose Create cluster.

  - Choose Step execution.

  - Choose other settings as appropriate for your application, and then choose Create cluster.

- **To enable step execution using Advanced Options in the AWS Console**

  - Open the Amazon EMR console at [EMR](https://console.amazonaws.cn/emr).

  - Choose `Create cluster`.

  - Choose `Go to advanced options`.

  - Under `Add steps (optional)`, select `Auto-terminate cluster after the last step is completed`.

  - Choose other settings as appropriate for your application, and then choose `Create cluster`.

---
</details>


<details><summary>Implementation</summary> 

## Implementation

**To enable step execution using the Amazon CLI**

- Specify the `--auto-terminate` parameter when you use the create-cluster command:
```
aws emr create-cluster \
     --name "Cluster" \
     --release-label emr-5.9.0 \
     --instance-type m4.large --instance-count 3 \
     --applications Name=Spark \
     --steps Type=Spark,Name="Spark Program",ActionOnFailure=CONTINUE,Args=[--class,com.jeanr84.sparkjob.SparkJob,s3://my-second-emr-bucket/tutorialEMR/spark-job-0.0.1-SNAPSHOT.jar,s3://my-second-emr-bucket/tutorialEMR/input.txt,s3://my-second-emr-bucket/tutorialEMR/output] \
     --use-default-roles \
     --ec2-attributes SubnetId=subnet-e7ba9d9c \
     --auto-terminate
```

---
</details>
<details><summary>Summary</summary> 

## Summary

- Open the AWS console and choose `Create cluster`. Choose `Go to advanced options`. 

- Under `Add steps (optional)`, select `Auto-terminate cluster after the last step is completed`.

- The `--auto-terminate` option helps clean up the cluster without manually terminating the cluster after use.

---
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
