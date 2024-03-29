# lambda-docker-ai

This is sample ai infrastructure on AWS Lambda.

## TensorFlow versions

Check [here](https://hub.docker.com/r/tensorflow/tensorflow/tags?page=1&name=py3)

## Local test

### Run container

```
$ docker run --rm -v ~/projects/indi/lambda-docker-ai:/var/task:ro,delegated -p 9000:8080 public.ecr.aws/lambda/python:3.12 lambda_function.lambda_handler
```

### Run test

```
$ curl -XPOST "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{}'
```

docker run --rm -v ~/projects/indi/lambda-docker-ai:/var/task:ro,delegated -p 9000:8080 public.ecr.aws/lambda/python:3.12 lambda_function.lambda_handler

## Commands

### Local test

0. Login ECR

```
$ ws ecr get-login-password --region <region-name> | docker login --username AWS --password-stdin xxxxxxxxxxxx.dkr.ecr.<region-name>.amazonaws.com
```

1. Image build

```
$ docker build -t lambda-python:latest .
```

2. Add tag

```
$ docker tag lambda-python:latest xxxxxxxxxxxx.dkr.ecr.<region-name>.amazonaws.com/lambda-python:latest
```

3. Run docker container

```
$ docker push xxxxxxxxxxxx.dkr.ecr.<region-name>.amazonaws.com/lambda-python:latest
```

### Upload container image

[Use Amazon ECR push commands](https://docs.aws.amazon.com/AmazonECR/latest/userguide/getting-started-cli.html)

### Build image on AWS Lambda

_Attention: Create Lambda function -made by container image- before exec command._

```
$ aws lambda update-function-code --function-name <your-function-name> --image-uri <your-ecr-repository-url>/<image-name>:latest
```
