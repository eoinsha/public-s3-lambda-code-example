# Publicly accessible Lambda code
An example of public Lambda code access in S3

In cases where you want to provide a CloudFormation template or Terraform module for a publicly-distributed Lambda function, you may need to provide public access to the code in an S3 bucket.
You want to do this without making the public bucket's permissions too broad.

This repository is a brief example of how to make a ZIP-packaged Lambda Function code accessible publicly without exposing any unnecessary access.
Only the Lambda service of any AWS account may retrieve the code, limiting the risk of security issues and high bucket owner costs.

## Deployment

1. Edit the bucket name in each template
2. Deploy the bucket in the first account:
```bash
aws cloudformation deploy --stack-name=lambda-package-bucket --template bucket-template.yaml
```
3. Deploy the Lambda function in _any_ other account:
```bash
aws cloudformation deploy --stack-name=lambda-package --template template.yaml --capabilities CAPABILITY_NAMED_IAM
```