# Git Build Badge Status Updated to VCS (BitBucket) -
## Problem - 
When The Pipeline released, The event Status of the pipeline (Start, Stop, Failed ...etc) should be visible to the repository related to the pipeline in bitbucket.

## Vision to solve - 
As the pipeline released, Using Lambda Function and SNS; Get the pipeline information as an event and by using AWS SDK "Boto3", fetch the source and its related information from pipeline -

### 1. If the source is "S3" -
Download the file from "S3" by using that fetched source information, read it and extract the important information and further use that information to show the status of pipeline to the related repository in any vcs (GitHub, BitBucket).

### 2. If the source is "vcs" - 
Using that fetched source information from pipeline, You can directly show the status of information to the related repository in any vcs (GitHub, BitBucket).

## Steps that follow -
1. Create a directory at **"/analytics-aws-management/pipelinev2-terraform/modules/pipeline"** with name **"git_build_badge_lambda_files"**.
2. Create a file index.py inside the above directory.
3. In the lambda.tf file, write a terraform code to create lambda function, an IAM Role with some resource policy and attached it to lambda.
4. In the pipeline.tf file, create a sns topic and subscription with evnts and in this sns, above created lambda is attached. 

Note - The above SNS is already used in all pipelines with existing git-build-badge lambda. I added our new lambda to this SNS subscription, So that It will automatically attached to all pipeline. 

Now, Whenever the pipeline is released, The SNS notify that the lambda function about pipeline and then lambda code will further take care. It will show the every status to the related repository.  
