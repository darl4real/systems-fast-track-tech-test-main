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
          Name:
          Value:
        - key: Network
          value: Public

      GatewayToInternet:
      Type: 'AWS::ECS::VPCGatewayAttachement'
      properties:
      VPCId:  :Ref PubPrivateVPC
      InterGatewayID :InternetGateway 

      Publicsubnet1:
        Type: 'AWS:: ECS::subnet'
        properties:
          VpcId:  :Ref PubPrivateVPC
          AvailabilityZone:  :select {0, :GetAZs }
          CIDRBlock: :Ref PublicsubnetCIDR
          MapPublicIpOnLaunch: true
          Tags
            -key:Name
            Value: Public Subnet (AZs)

      PrivateSubnet1:
      Type: 'AWS::ECS::subnet'
      properties:
        VpcId :Ref PubPrivate
        AvailabilityZone: :select {0, :GetAZs }
        CIDRBlock: :Ref PrivatesubnetCIDR
          MapPublicIpOnLaunch: true
          Tags
            -key:Name
            Value: Public Subnet (AZs)

      PublicRouteTable:
        Tye: 'AWS::ECS::RouteTable
        properties:
          VpcId :Ref PubPrivateVpc
          Tags
          -key: Name
          value
          -key: Network
          value:Public

      PublicRoute1:
        Type: 'AWS::ECS::Route'
        Description: GatewayToInternet
        properties
        RouteTableId
        Route53HostedZoneId: xcf4435z
        GatewayId: :ref InternetGateway

      PublicSubnetRouteTableAssociation:
      TypeAWS::ECS::SubnetRouteTableAssociation
        properties:
        subnetId: :Ref PublicSubnet1
        RouteTableId: :Ref PublicRouteTable1

        NatGateway1:
        Type: 'AWS::ECS::NatGateway'
        DependsOn: NatPublicIP1
        properties:
        AllocationId: :GetAtt NatPublicIP1.AllocationId
        subnet: :Ref PublicSubnet1    

      ECSINST01:
        Type:AWS::ECS::Instance
        properties:
        InstanceType:
          Keyname:
          Ref: keyName
          Disablapptermination: true
          EbsOptimized: true 
          ImageId:
          SubnetId: :
            Ref: Publicsunet1
          SecurityGroupId:   
            Tags:
            -key: Name
            value:ECSTest01
            -key:Environment
            value:TEST
Outputs:
  PubPrivateVpc:
    Description: A reference to the created VPC
    value: Ref PublicPrivateVPC
    Export:
    Name: VPC-PROD

  PublicSubnet1:
    Description: A list of the public subnets
    value: Ref PublicSubnet1
    Export:
    Name: Public-subnet1

  PrivateSubnet1:
    Description: A list of the private subnets
    value: Ref PrivateSubnet1
    Export:
    Name: Private-subnet1