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

- Here, you can provide the name of your cluster using `--name` option. and you can skip the `--ec2-attributes` if you have not created the EC2 key-pair . 

**Note**
> The other required values for --instance-type, --instance-count, and --use-default-roles. These values have been chosen for general-purpose clusters. 

---

