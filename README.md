# AWS-Cloudformation

This repository is for learn Infrastucture as Code with AWS cloudformation.

- Deploy VPC with parameters file:
    `./create.sh my-vpc vpc/vpc.yml vpc/vpc-parameters.json`

`create.sh` content file contains
```
aws cloudformation create-stack --stack-name $1 --template-body file://$2 --parameters file://$3 --capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM" --region=us-west-2
```

- Deploy Nat Gateway:
    `./create.sh my-vpc nat-gateway/nat.yml nat-gateway/nat-parameters.json`