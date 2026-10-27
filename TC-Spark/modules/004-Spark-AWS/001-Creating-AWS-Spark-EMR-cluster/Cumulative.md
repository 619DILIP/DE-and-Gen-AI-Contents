# Cumulative for Creating AWS Spark EMR cluster
<details><summary>Prerequisites and Learning Objectives</summary>

## Prerequisites

- Sign up for an AWS account.

## Objectives

- To learn how to create a Spark-EMR cluster in AWS.

---
</details>
<details><summary>Description</summary>

## Description

**Steps to launch a cluster with Spark installed using the Console**

- Open the Amazon EMR console at [EMR](https://console.aws.amazon.com/emr).

- Choose the `Create cluster` option.

- Enter a `Cluster name` to help you identify the cluster. For example, "Spark EMR Cluster Demo".

- For `Software Configuration`, choose a release option.

- Choose the `Spark` option under `Applications` to install Spark on your cluster.

- Select other options as necessary and then choose `Create cluster` to launch the cluster. 

---

</details>


<details><summary>Implementation</summary> 

## Implementation

**To launch a cluster with Spark installed using the AWS CLI**

- Create the cluster with the following command.
```
aws emr create-cluster \
--name "<My First EMR Cluster>" \
--release-label <emr-5.36.0> \
--applications Name=Spark \
--ec2-attributes KeyName=<myEMRKeyPairName> \
--instance-type m5.xlarge \
--instance-count 3 \
--use-default-roles
```

- Here, you can provide the name of your cluster using the `--name` option. You can skip the `--ec2-attributes` if you have not created the EC2 key pair. 

**Note**
> The other required values for `--instance-type`, `--instance-count`, and `--use-default-roles` have been chosen for general-purpose clusters. 

---

</details>
<details><summary>Summary</summary> 

## Summary

- After logging in to AWS, choose `Create cluster` to open the Quick Options wizard. 

- Then enter the name of your cluster and choose the `Spark` option under `Applications` to install Spark on your cluster. 

- For `Software Configuration`, choose a release option. After that, select other necessary options and then click on the `Create cluster` option.

---

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
