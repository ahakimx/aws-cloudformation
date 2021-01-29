## Create VPC and Internet Gateway

This section is create vpc and internet gateway then attach internet gateway to VPC.

 >  *Amazon Virtual Private Cloud (VPC) lets you provision a logically isolated selection of the Amazon Web Services (AWS) cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets and configuration of route tables and network gateways.*

*note*: when create an AWS account, a "default" VPC is created

Parameters:
```
Parameters:

  EnvironmentName:
    Description: An environment name for VPC
    Type: String

  VpcCIDR:
    Description: Enter the IP range CIDR notation
    Type: String
    Default: 10.0.0.0/16
```

Resource for this stack is `VPC`, `InternetGateway` and `InternetGatewayAttachment`:
```
Resources:
  VPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: !Ref VpcCIDR
      EnableDnsHostnames: true
      Tags:
        - Key: Name
          Value: !Ref EnvironmentName

  igwName:
    Type: AWS::EC2::InternetGateway
    Properties:
      Tags:
        - Key: Name
          Value: !Ref EnvironmentName

  AttachGateway:
    Type: AWS::EC2::VPCGatewayAttachment
    Properties:
      VpcId: !Ref VPC
      InternetGatewayId: !Ref igwName
```

Run script to create a VPC:

```
./create.sh vpc vpc.yml vpc-parameters.json
```

> *An internet gateway is a horizontally scaled, redundant and highly available VPC component that allow communication between instances in your VPC and the internet. It therefore imposes no availability risks or bandwidth constraints on your network traffic.*

*note*: default VPC already has an IGW attached.

To update resources or parameter:

Edit `ParameterValue` on `vpc-parameters.json` file, example:
```
[
    {
        "ParameterKey": "EnvironmentName",
        "ParameterValue": "UpdateProjectName"
    }
]
```

Update stack

```
./update.sh vpc vpc.yml vpc-parameters.json
```