![](https://img.shields.io/github/commit-activity/t/subhamay-bhattacharyya/aws-cfn-nested-stacks)&nbsp;![](https://img.shields.io/github/last-commit/subhamay-bhattacharyya/aws-cfn-nested-stacks)&nbsp;![](https://img.shields.io/github/release-date/subhamay-bhattacharyya/aws-cfn-nested-stacks)&nbsp;![](https://img.shields.io/github/repo-size/subhamay-bhattacharyya/aws-cfn-nested-stacks)&nbsp;![](https://img.shields.io/github/directory-file-count/subhamay-bhattacharyya/aws-cfn-nested-stacks)&nbsp;![](https://img.shields.io/github/issues/subhamay-bhattacharyya/aws-cfn-nested-stacks)&nbsp;![](https://img.shields.io/github/languages/top/subhamay-bhattacharyya/aws-cfn-nested-stacks)&nbsp;![](https://img.shields.io/github/commit-activity/m/subhamay-bhattacharyya/aws-cfn-nested-stacks)&nbsp;![](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/bsubhamay/53535fe14b2a34adf2c58da3d4bc958b/raw/aws-cfn-nested-stacks.json?)

AWS CloudFormation nested stack templates.

## Overview

This repository contains AWS CloudFormation templates for creating nested stacks. These templates help in managing and deploying AWS resources in a structured and reusable manner.

## Templates

### VPC Template

The VPC template ([vpc/vpc.yaml](vpc/vpc.yaml)) creates a Virtual Private Cloud (VPC) with optional IPv6 CIDR block support. It includes parameters for project name, environment, GitHub attributes, and VPC configuration.

#### Parameters

- **ProjectName**: The Project name to be used as a resource tag value. Must be 5-30 characters long and contain only lowercase alphabets.
- **Environment**: The Environment name to be used as a resource tag value. Allowed values are "devl", "test", "prod".
- **GitHubRef**: GitHub Ref name to be used as a resource tag value. Can contain alphanumeric characters, slashes, underscores, and hyphens.
- **GitHubURL**: GitHub URL to be used as a resource tag value. Must start with 'https://github.com/' and can contain alphanumeric characters, dots, underscores, and hyphens.
- **GitHubWFRunNumber**: The Workflow run number to be used as a resource tag value.
- **GitHubSHA**: The SHA value of the last commit to be used as a resource tag value. Must be a 40-character hexadecimal string.
- **GitHubRepository**: The GitHub Repository name to be used as a resource tag value. Must be 10-30 characters long, contain lowercase letters, numbers, dashes, and start with a letter.
- **CiBuild**: CI Build of the feature branch to be appended to a resource name.
- **VPCCidrBlock**: VPC CIDR Block. Must be in the form x.x.x.x/x.
- **EnableIPV6Cidr**: Boolean to enable IPv6 CIDR.

#### Resources

- **VPC**: Creates an AWS VPC with specified CIDR block, DNS support, and tags.
- **IPv6CidrBlock**: Adds an IPv6 CIDR block to the VPC if IPv6 is enabled.

#### Outputs

- **VpcId**: The ID of the created VPC.
- **VpcCidrBlock**: The CIDR block of the VPC.
- **VpcCidrBlockAssociations**: The CIDR block associations of the VPC.
- **VpcDefaultNetworkAcl**: The default network ACL of the VPC.
- **VpcDefaultSecurityGroup**: The default security group of the VPC.
- **VpcIpv6CidrBlocks**: The IPv6 CIDR blocks of the VPC if IPv6 is enabled.

### SNS Topic Template

The SNS Topic template ([sns/sns-topic.yaml](sns/sns-topic.yaml)) creates an SNS Topic with optional KMS encryption. It includes parameters for project name, environment, GitHub attributes, and SNS configuration.

#### Parameters

- **ProjectName**: The Project name to be used as a resource tag value. Must be 5-30 characters long and contain only lowercase alphabets.
- **Environment**: The Environment name to be used as a resource tag value. Allowed values are "devl", "test", "prod".
- **GitHubRef**: GitHub Ref name to be used as a resource tag value. Can contain alphanumeric characters, slashes, underscores, and hyphens.
- **GitHubURL**: GitHub URL to be used as a resource tag value. Must start with 'https://github.com/' and can contain alphanumeric characters, dots, underscores, and hyphens.
- **GitHubWFRunNumber**: The Workflow run number to be used as a resource tag value.
- **GitHubSHA**: The SHA value of the last commit to be used as a resource tag value. Must be a 40-character hexadecimal string.
- **GitHubRepository**: The GitHub Repository name to be used as a resource tag value. Must be 10-30 characters long, contain lowercase letters, numbers, dashes, and start with a letter.
- **CiBuild**: CI Build of the feature branch to be appended to a resource name.
- **KmsMasterKeyAlias**: The KMS master key alias to be used for server-side encryption.
- **TopicBaseName**: The base name of the SNS topic. The topic name will be created by appending the environment and region.
- **TopicDisplayName**: The SNS topic display name.

#### Resources

- **SNSTopic**: Creates an SNS Topic with the specified properties and tags.

#### Outputs

- **SNSTopicArn**: The Arn of the SNS Topic.

### SNS Subscription Template

The SNS Subscription template ([sns/sns-subscription.yaml](sns/sns-subscription.yaml)) creates SNS Topic subscriptions for Email, SQS, Lambda, and HTTPS endpoints. It includes parameters for SNS topic ARN, email address, SQS queue ARN, Lambda function ARN, and HTTP endpoint.

#### Parameters

- **SNSTopicArn**: The ARN of the SNS Topic.
- **EmailAddress**: The email address to subscribe to the SNS topic.
- **SqsQueueArn**: The ARN of the SQS Queue to subscribe to the SNS topic.
- **LambdaFunctionArn**: The ARN of the Lambda function to subscribe to the SNS topic.
- **HttpEndpoint**: The HTTP endpoint to subscribe to the SNS topic.

#### Resources

- **EmailSubscription**: Creates an SNS subscription for the provided email address.
- **SqsSubscription**: Creates an SNS subscription for the provided SQS queue.
- **LambdaSubscription**: Creates an SNS subscription for the provided Lambda function.
- **HttpsSubscription**: Creates an SNS subscription for the provided HTTP endpoint with a delivery policy.

#### Outputs

- **EmailSubscriptionArn**: The ARN of the SNS Topic Email subscription.
- **SqsSubscriptionArn**: The ARN of the SNS Topic SQS subscription.
- **LambdaSubscriptionArn**: The ARN of the SNS Topic Lambda function subscription.
- **HttpsSubscriptionArn**: The ARN of the SNS Topic HTTP endpoint subscription.

## Usage

To deploy the VPC template, use the AWS CloudFormation console, AWS CLI, or any other tool that supports CloudFormation.

```sh
aws cloudformation create-stack --stack-name my-vpc-stack --template-body file://vpc/vpc.yaml --parameters ParameterKey=ProjectName,ParameterValue=myproject ParameterKey=Environment,ParameterValue=devl
```

To deploy the SNS Topic template, use the AWS CloudFormation console, AWS CLI, or any other tool that supports CloudFormation.

```sh
aws cloudformation create-stack --stack-name my-sns-topic-stack --template-body file://sns/sns-topic.yaml --parameters ParameterKey=ProjectName,ParameterValue=myproject ParameterKey=Environment,ParameterValue=devl
```

To deploy the SNS Subscription template, use the AWS CloudFormation console, AWS CLI, or any other tool that supports CloudFormation.

```sh
aws cloudformation create-stack --stack-name my-sns-subscription-stack --template-body file://sns/sns-subscription.yaml --parameters ParameterKey=SNSTopicArn,ParameterValue=arn:aws:sns:us-east-1:123456789012:sns-topic-name ParameterKey=EmailAddress,ParameterValue=example@example.com
```