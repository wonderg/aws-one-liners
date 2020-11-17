# aws-one-liners
Oneliners for AWS CLI

```
Get EKS Config
aws eks --region region update-kubeconfig --name $clusterName

Get EC2 Instances info
aws ec2 describe-instances --output text --query 'Reservations[*].Instances[*].[InstanceId, InstanceType, ImageId, State.Name, LaunchTime, SubnetId, Placement.AvailabilityZone, Placement.Tenancy, PrivateIpAddress, PublicIpAddress, PrivateDnsName, PublicDnsName, [Tags[?Key==`Name`].Value] [0][0] ] > instances.tsv' 
```
