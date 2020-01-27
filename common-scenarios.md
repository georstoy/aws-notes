# Cross-stack reference
 - [How to create VPC that can be shared across stacks?](https://stackoverflow.com/questions/57623766/how-to-create-vpc-that-can-be-shared-across-stacks/57632803#57632803)

# Access Ec2 Ecs by ssh
 - define security group with inbound rule allowing access on port 22 for SSH

 - create key pair
   * cli
   `aws <service e.g. ec2> create-key-pair --key-name <my-key-pair>` \
   * aws console -> EC2 -> Key pairs
  
    [(reference)](https://stackoverflow.com/questions/57572065/how-can-i-access-an-ec2-instance-created-by-cdk)

 - add the public key to `context` in `cdk.json`
```
{
  "context": {
    "key_pair": <key pair name>
  }
  ...
}
```
 - pass the public key from context to ec2 instance in it's definition
```
const ecsCluster = new ecs.Cluster(this, "MyContainerCluster", {
      vpc: this.vpc,
      capacity: {
        instanceType: ec2.InstanceType.of(
          ec2.InstanceClass.T2,
          ec2.InstanceSize.MICRO
        ),
        keyName: <public key from context> 
      }
    });
```