This template deploys a VPC with an infrastructure diagram that has a three public and private subnets spread accross multi availability zones, with an aim to fully automate the implementation using Infrastructure as Code and CI/CD.
Parameters:  
Resources:
    PublicSubnet1CIDR: 
    Description: Domain DomainName for the public subnet in first Availability zone
    Type: String
    Default: pub--7eqwhyn6rn

    PrivateSubnet1CIDR: 
    Description: DomainName for the private subnet in first Availability zone
    Type: String
    Default: priv--whyn6rn7eq
    
    vpcCIDR: CIDR Notation of vpc
      Description:
      Type: String
      Default: x567hhdz

    AcmCertificateArn: 
      Description: Acm certification or keypair given to allow RDP access the instance
      Default: : arn:aws:acm:eu-west-1:8877665544:certificate/123456789012-1234-1234-1234-12345678
      Type:AWS::ECS::KeyName

    Resources:

    PubprivateVPC
    Type: 'AWS::ECS::VPC
    properties:
      Tag
        - Key: Name
          Value:
        - key: Network
          value: Public
  myStack:
    Type: AWS::CloudFormation::Stack
    Properties:
      TemplateURL: https://s3.amazonaws.com/cloudformation-templates-us-east-1/S3_Bucket.template
      TimeoutInMinutes: '60'
Outputs:
  StackRef:
    Value: !Ref myStack
  OutputFromNestedStack:
    Value: !GetAtt myStack.Outputs.BucketName