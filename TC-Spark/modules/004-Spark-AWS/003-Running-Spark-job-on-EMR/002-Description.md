## Description

- The first thing to do for running your spark job is to create a S3 bucket. Follow the below steps to easily create S3 bucket using console.

  - Sign in to the AWS Management Console and open the Amazon S3 console at [S3](https://console.aws.amazon.com/s3/)
   
  - Choose `Create bucket` option.

  - Enter the name for your bucket and then choose its AWS region and click next.

  - Use can click next on `Set properties page` and `Set permissions page`, if you want to use the defaults values mentioned there.

  - On the Review page, verify the settings and choose Create bucket.

- After creating s3 bucket, upload your file to the s3 bucket by creating a folder there.


**Launch an Amazone EMR Cluster and Submit the Spark-Job** 

- Go to Amazone EMR console and `change the region` on which you want to deploy the cluster.

- Choose `Create cluster` 

- On settings, Enter `Cluster name`, `choose s3 bucket you created` and check `Step execution`. 

- On the `Software Configuration` section, use the default release.

- On the Hardware configuration section, choose the instance type and the number of instances

- On the `Add steps` section select `Spark` for `Application`.

- Finally, click on `Create cluster` and click on `the refresh the icon` to see the status passing from Starting to Running to Terminating — All steps completed.

- Now go back to the S3 console and you will see the output directory in which the result has been stored, you can click on it and download its contents.

---

