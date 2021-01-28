Create VPC and Internet Gateway, then attach internet gateway to VPC.

Run script to create a VPC:

```
./create.sh vpc vpc.yml vpc-parameters.json
```

To update resources or parameter:

```
./update.sh vpc vpc.yml vpc-parameters.json
```