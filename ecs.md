# ECS (Elastic Container Service)
 - construct an ECS cluster in a stack \
`const ecsCluster = new ecs.Cluster(this, "MyContainerCluster", { vpc: this.vpc });`
 - use EC2 instances in the cluster \ 
    *(instead of Fargate, because EC2 is the better/cheaper option for services with continuous uptime)*
    
# ECR (Elastic Container Registry)
 - Launch an ECR repo \
    AWS CDK creates a default ECR repo when ECS cluster is constructed [(reference)](https://medium.com/tysonworks/deploy-go-applications-to-ecs-using-aws-cdk-1a97d85bb4cb)

    Otherwise:  `const ecrRepo = new ecr.Repository(this, "AttendorImageRepo");`

 - Create docker images from github repo and tag them with ECR tag \
    AWS CDK creates docker images with ```ecs.ContainerImage.fromAsset(`${__dirname}/api`)```
    
    Otherwise: `docker build https://github.com/scavasoft/<MyGithubSourceCodeRepo>.git#<MyBranch>:<Directory of the Dockerfile> -t <AWS Account id>.dkr.ecr.<Region>.amazonaws.com/<MyECRImageRepo>`
    [(reference)](https://stackoverflow.com/questions/26753030/how-to-build-docker-image-from-github-repository/56892395)

 - Get ECR repo authentication token for the docker client \
    `aws ecr get-login --region <Region> --registry-ids <AWSAccountId> --no-include-email`
    `docker login -u AWS -p <Password> https://<AWS Account Id>.dkr.ecr.<Region>.amazonaws.com`
    [(reference)](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html#registry_auth)

 - Push your image to Amazon ECR repo with docker client \
    `aws ecr create-repository --repository-name hello-repository --region region`