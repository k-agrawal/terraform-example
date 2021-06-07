############### Atlantis Container Image Creation ###############

Step 1: Authenticate to your default ECR repository.

$ aws ecr get-login-password | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com

Step 2: Create Amazon ECR repository for Atlantis.

$ aws ecr create-repository \
    --repository-name atlantis \
    --image-scanning-configuration scanOnPush=true

Step 3: Create a docker image using Dockerfile.

$ docker build -t atlantis .

Step 4: Tag the image to push to your repository.

$ docker tag atlantis:latest <aws_account_id>.dkr.ecr.<region>.amazonaws.com/atlantis:latest

Step 5: Push the image to your ECR repository.

$ docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/atlantis:latest
