# Github actions ec2-runner ecs-deploy
## Workflow and configs needed to deploy an application on multiple AWS (accounts) on ECS using ec2-runner with assumed role by ec2.

## Required Repository Secrets

1- ARN of the role to be assumed by ec2
  - this template uses ASSUME_ROLE_ARN_{{BRANCH_NAME}} as secret name format.

2- (optional) AWS_ROLE_EXTERNAL_ID for making sure role is only assumed by the ec2 and no one else.

## What needs to be done on AWS account

- Create a role (P) at destination accounts with is the permissions required for ECR login and ECS deployment.
- Create a role (Q) at ec2 runner account with assume role permissions to all destination accounts.
- Add trust policy on role (P) allowing it to be assumed by role Q.
