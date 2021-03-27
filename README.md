# Github actions ec2-runner ECS-deploy
## Workflow and configs needed to deploy an application on multiple AWS (accounts) on ECS using ec2-runner with an assumed role by ec2.

## Configure ec2 Github runner
- Make sure you have an ec2 running on the AWS account.
- Also make sure that the ec2 has a role with assume role permissions for the accounts where we are deploying the app.
- After that click on GitHub repository settings of your application, go to actions, and configure a runner.

## Required Repository Secrets

1- ARN of the role to be assumed by ec2
  - this template uses ASSUME_ROLE_ARN_{{BRANCH_NAME}} as secret name format.

2- (optional) AWS_ROLE_EXTERNAL_ID for making sure the role is only assumed by the ec2 and no one else.

3- You can copy the workflow file from my account and use it for deploying your applications.
  - Make sure to replace all the placeholders with required config variables such as repo name, cluster name, service name, etc.
  - Make sure you have task-definition.json in the repo. (My template uses {{BRANCH_NAME}}-task-definition.json as naming convention when there are multiple branches and each branch deploy in a separate AWS account)
## What needs to be done on the AWS account

- Create a role (P) at destination accounts with is the permissions required for ECR login and ECS deployment.
- Create a role (Q) at ec2 runner account with assume role permissions to all destination accounts.
- Add trust policy on the role (P) allowing it to be assumed by role (Q).

### More details and sample app ?
If you are having issus understanding this or having issues with setting permissions, checkout [this](https://github.com/harshit9715/github-actions-ec2-runner-ecs-deploy) other repo. It includes more info but uses github default runner.
