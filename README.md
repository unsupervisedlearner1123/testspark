# Running Spark job on Amazon EMR
This repository contains a Python script that runs a Spark job and a CSV file. The job is submitted to an Amazon EMR cluster using the AWS CLI by creating a step. Here's a step-by-step guide on how to set up and run the job.

## Prerequisites
* An AWS account with appropriate permissions to create an EMR cluster.
* AWS CLI installed on your local machine.

## Setting up EMR Cluster
Follow the steps in the AWS console EMR service wizard to configure your cluster. Make sure to choose the appropriate instance type, security group, and key pair. Also, make sure to select the latest version of Spark. Once you've configured the cluster, click on "Create Cluster" to launch it.

## Uploading the files to S3
Upload the .py script and .csv file to an S3 bucket. Make sure to note down the S3 bucket name and the object key for the files.

## Running the job
* Open your terminal and run the following command to create a new step:
`
aws emr add-steps --cluster-id <cluster_id> --steps Type=spark,Name=<job_name>,ActionOnFailure=CONTINUE,Args=[--deploy-mode,cluster,--master,yarn,<s3_path_to_script.py>,<s3_path_to_csv_file>]
`
* Once you've run the command, you should see a step ID in the output. Use this ID to check the status of the step using the following command:
`
aws emr describe-step --cluster-id <your-cluster-id> --step-id <your-step-id>
`
If the step has completed successfully, you should see `"State": "COMPLETED"` in your output.
