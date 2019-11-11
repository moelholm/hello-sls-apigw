# hello-sls-apigw

custom domain name > API Gateway (via CloudFront) > Lambda (Node.js)

# Guide

## Precondition
A Route53 hosted zone must exist. Also,

    npm install
    export AWS_REGION=<enter your AWS region id here>
    export DOMAIN_NAME=<enter your domain here>

Install an IAM policy for the serverless-domain-manager sls plugin

    HOSTED_ZONE_ID=<enter your zone id here>
    
    wget https://raw.githubusercontent.com/amplify-education/serverless-domain-manager/4f5bc85ce023d22f1342e897a423a8eaeac19cf7/scripts/cloudformation/serverless-domain-manager-deploy-policy.yaml
    
    aws cloudformation create-stack \
      --stack-name serverless-domain-manager \
      --template-body file://serverless-domain-manager-deploy-policy.yaml \
      --parameters ParameterKey=HostedZoneId,ParameterValue="$HOSTED_ZONE_ID" \
      --capabilities CAPABILITY_IAM

Finally, go to the IAM console and add the newly created serverless managed policy to your user.

## Install the service (Function and API)

    sls deploy

## Create DNS mapping for API Gateway

    sls create_domain
