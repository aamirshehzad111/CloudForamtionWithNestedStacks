# CloudForamtionWithNestedStacks

Templates:
* parentStack.yml
* efs.yml
* alb.yml
* rds.yml
* asg.yml

Prerequisite:

* you need have a vpc set up in your region with minimum 2 public and 2 private subnets.
* You should have secureString parameter created on aws parameter store with name `RDS_PASSWORD`
* You should have your tmeplates uplaoded on s3 bucket.

  EfsStack:
    Type: AWS::CloudFormation::Stack
    Properties:
      TemplateURL: "https://<your_bucket_name>.s3.<your_region>.amazonaws.com/<template_name>"
      TimeoutInMinutes: 30
      Parameters: 
        PrivateSubnetId1: !Select [ 0, !Ref PrivateSubnets ]
        PrivateSubnetId2: !Select [ 1, !Ref PrivateSubnets ]
        VPCId: !Ref VPCId
        VPCCidr: !Ref VPCCidr

Update all the resource in parentStack according above example.


Deploy:
* You are good to go now.

