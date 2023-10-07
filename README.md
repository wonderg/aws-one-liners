# AWS One-Liners
Collection of one-liners for AWS CLI operations.

## EKS

### Get EKS Config
```bash
aws eks --region region update-kubeconfig --name $clusterName
```

## EC2

### Get EC2 Instances Info
```bash
aws ec2 describe-instances --output text --query 'Reservations[*].Instances[*].[InstanceId, InstanceType, ImageId, State.Name, LaunchTime, SubnetId, Placement.AvailabilityZone, Placement.Tenancy, PrivateIpAddress, PublicIpAddress, PrivateDnsName, PublicDnsName, [Tags[?Key==`Name`].Value] [0][0] ]' > instances.tsv
```

### Filter EC2 Instances by Tags
```bash
aws ec2 describe-instances --output text --query 'Reservations[*].Instances[*].[InstanceId, InstanceType, ImageId, State.Name, LaunchTime, SubnetId, Placement.AvailabilityZone, Placement.Tenancy, PrivateIpAddress, PublicIpAddress, PrivateDnsName, PublicDnsName, [Tags[?Key==`Name`].Value] [0][0] ]' --filters 'Name=tag:Something,Values=SomeValue'
```

## Load Balancers

### Get ELB Configurations
```bash
aws elb describe-load-balancers --query 'LoadBalancerDescriptions[*].[LoadBalancerName, DNSName, ListenerDescriptions[*]]'
```

### For ELB, CLB, ALB
```bash
aws elbv2 describe-load-balancers --query 'LoadBalancers[*].[LoadBalancerArn, LoadBalancerName, Type]'
aws elbv2 describe-target-groups --query 'TargetGroups[*].[TargetGroupArn, TargetGroupName, Port]'
```

## RDS

### Describe RDS Instances
```bash
aws rds describe-db-instances --query 'DBInstances[*].[DBInstanceIdentifier, DBInstanceClass, Engine[*]]'
```

## Redshift

### Describe Redshift Clusters
```bash
aws redshift describe-clusters --query 'Clusters[*].[ClusterIdentifier, NodeType, NumberOfNodes]'
```

## Miscellaneous

### Find Latest AmazonLinux2 AMI
```bash
aws ec2 describe-images --owners amazon --filters "Name=name,Values=amzn*" --query 'sort_by(Images, &CreationDate)[].Name'
```

### Get List of All Route53 Records
```bash
aws route53 list-hosted-zones |jq '.[] | .[] | .Id' | sed 's!/hostedzone/!!' | sed 's/"//g'> zones
for z in `cat zones`; do
  echo $z;
  aws route53 list-resource-record-sets --hosted-zone-id $z >>  records;
done
```
