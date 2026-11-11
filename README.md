# getmeto-infra

## Common commands

### Login to AWS
```
aws --version
aws sso login --profile getmeto
aws configure sso;
aws sso login --profile getmeto
export AWS_PROFILE=getmeto
aws sts get-caller-identity
```

### Install cloud formation linting tool
```
pip install cfn-lint
pip install --upgrade pip
```

### Cloud formation linting tool usage
```
cfn-lint --version
cfn-lint path/to/stackfile.yaml
```

### Deploying to AWS CloudFormation
```
aws cloudformation deploy --template-file infra/00-hello.yaml --stack-name getmeto-hello --parameter-overrides Environment=dev
aws cloudformation describe-stacks --stack-name getmeto-hello --query "Stacks[0].Outputs" --output table 
aws cloudformation deploy --template-file infra/00-hello.yaml --stack-name getmeto-hello --no-execute-changeset
```

### Redeploy to AWS Cloudformation
```
aws cloudformation deploy \
  --template-file infra/01-oidc-github.yaml \
  --stack-name getmeto-github-oidc \
  --capabilities CAPABILITY_NAMED_IAM \
  --region us-east-1  --parameter-overrides ExistingOidcProviderArn=arn:aws:iam::343782217094:oidc-provider/token.actions.githubusercontent.com
```