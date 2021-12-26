# go-lambda-sample

## Configure aws

```.sh
## AWS Access Key ID : test
## AWS Secret Access Key : test
## Default region name : ap-northeast-1
## Default output format : json
aws configure
```

## Example access localstack with aws-cli

```.sh
## Create S3 Bucket in localstack container
$ aws --endpoint http://localstack:4566 s3 mb s3://testbucket
```
