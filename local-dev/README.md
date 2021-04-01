# Building docker image from local code

In the parent `aws-recon` directory, run the following command to build the docker image from existing code:

```shell
$ docker build \
    -t securiti/aws_recon:local-dev \
    -f local-dev/Dockerfile .
```

After docker image is built, you can run that image locally:
```
$ docker run -t --rm \
    -e AWS_REGION=us-west-2 \
    -e AWS_ACCESS_KEY_ID \
    -e AWS_SECRET_ACCESS_KEY \
    -e AWS_SESSION_TOKEN \
    -v $(pwd)/output.json:/output.json \
    securiti/aws_recon:local-dev  \
    aws_recon -v -s S3 -r global,us-east-1,us-east-2
```
