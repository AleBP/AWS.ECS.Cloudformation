# AWS.ECS.Cloudformation
This AWS CloudFormation template deploys an ECS Service with an associated Application Load Balancer. Below is a detailed explanation of the template components and parameters.

Parameters
KeyPair: The name of an existing EC2 KeyPair to enable SSH access to the container instances.
LoadBalancerSubnets: List of subnets for the load balancer.
ECSSubnets: List of subnets for the ECS cluster.
VpcId: The VPC ID where resources will be deployed.
InstanceType: The instance type for the ECS cluster EC2 instances (default: t3a.small).
DesiredCapacity: The number of instances to launch in the ECS cluster (default: 1).
MaxSize: The maximum number of instances that can be launched in the ECS cluster (default: 2).
MinSize: The minimum number of instances that can be launched in the ECS cluster (default: 1).
Owner: A tag value to identify the owner of the resources.
healthCheckType: The health check type for the Auto Scaling group (default: EC2).
LaunchTemplateVersionNumber: The version number of the launch template (default: 1).
ISize: The volume size for the instance (default: 100 GB).
AmiID: The AMI ID for the instances, queried from AWS Systems Manager Parameter Store.
Resources
ECSCluster: Creates an ECS cluster with the name specified in the Owner parameter.
EC2InstanceProfile: An IAM instance profile for EC2 instances with necessary roles and policies.
ContainerServiceRole: An IAM role for the container service with policies to interact with ECS, EC2, and CloudWatch.
AutoScalingGroup: An Auto Scaling group for managing the ECS instances.
ScaleUpPolicy: A scaling policy to increase the capacity of the Auto Scaling group.
ScaleDownPolicy: A scaling policy to decrease the capacity of the Auto Scaling group.
LaunchTemplate: An EC2 launch template with instance configurations, including network interfaces, security groups, and user data to configure ECS.
ECSService: Defines the ECS service with a Caddy container, associated with the load balancer.
CaddyTaskDefinition: Defines the ECS task with a Caddy container.
ContainerInstancesSecurityGroup: A security group for the ECS instances with rules for SSH, HTTP, and HTTPS access.
LoadBalancerSecurityGroup: A security group for the Application Load Balancer with rules for HTTP and HTTPS access.
ApplicationLoadBalancer: An Application Load Balancer to distribute traffic to the ECS service.
ApplicationLoadBalancerListener: A listener for the Application Load Balancer on port 80.
caddyTargetGroup: A target group for the load balancer, associated with the ECS service.
Outputs
Cluster: The created ECS cluster.
Listener: The Application Load Balancer listener.
ApplicationLoadBalancerEndpoint: The DNS name of the Application Load Balancer.
SecurityGroup: The security group ID of the ECS instances.
EC2InstanceProfile: The IAM instance profile for the EC2 instances.

P.S: I used caddy image, you can change the image for what you need to do 
