# aws-one-liners
Oneliners for AWS CLI

```
Get EKS Config
aws eks --region region update-kubeconfig --name $clusterName

Get EC2 Instances info
aws ec2 describe-instances --output text --query 'Reservations[*].Instances[*].[InstanceId, InstanceType, ImageId, State.Name, LaunchTime, SubnetId, Placement.AvailabilityZone, Placement.Tenancy, PrivateIpAddress, PublicIpAddress, PrivateDnsName, PublicDnsName, [Tags[?Key==`Name`].Value] [0][0] ] > instances.tsv' 

ELB Configurations 
aws elb describe-load-balancers --query 'LoadBalancerDescriptions[*].[LoadBalancerName, DNSName, ListenerDescriptions[*]]'

for ELB, CLB, ALB
aws elbv2 describe-load-balancers --query 'LoadBalancers[*].[LoadBalancerArn, LoadBalancerName, Type]'
aws elbv2 describe-target-groups --query 'TargetGroups[*].[TargetGroupArn, TargetGroupName, Port]'

RDS
aws rds describe-db-instances --query 'DBInstances[*].[DBInstanceIdentifier, DBInstanceClass, Engine[*]]'


Redshift
aws redshift describe-clusters --query 'Clusters[*].[ClusterIdentifier, NodeType, NumberOfNodes]'

Find latest AmazonLinux2 AMI
aws ec2 describe-images --owners amazon --filters "Name=name,Values=amzn*" --query 'sort_by(Images, &CreationDate)[].Name'
```

