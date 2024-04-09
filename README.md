# AWS_Website_Architecture_V1
it's an common solution for website infrastructure on cloud

# We have to follow below steps to create this infrastructure:
AWS Components that we are using for this infrastrucure
- EC2
- VPC
- CloudFront
- RDS
- S3
- CloudWatch
- WAF (Web Application Firewall)
- AWS Shield
- ALB (Application load balancer)
- Auto Scalling Groups
- Elasticache
- AWS EKS (Elastic Kubernetes Services)
- NAT Gateway
- VPC Endpoint

## Common Approach to create:

- First create VPC by giving CIDR block range like (192.10.0.0/22) and create total 8 subnets within the same CIDR range in which two should be public and other should be private, name for the subnets you can given as per the diagram.
- launch ec2 instances in each AZ (for testing you can create one in each), for serving frontend also they will act as the reverse proxy.
- Create EKS cluster and divide the nodes equally in each AZ for HA.
- Create two RDS instances in both AZs in which one should be primary for serving the request and another should be standby with continuous replication.
- Elasticache also we are using here for better performance it will store the cache for the database query and serving the request much faster.
- CloudFront is acting as an Content Delivery network here, it will store the cache for the user so that they are able to resume thier journey where he left, we can say it will help to store the session so for achiving this we need to create the distribution in which source should be route53 and destination should be Application load balancer and another destination should be S3 which is for static content like term and condition page for the user also need to attcah the certifacte for serving https request.    
- Create Hosted Zones in Route53 and provide the target as CloudFront Distribution also provide CNAME record for routing thr traffic to CF, need to confire DNS records as per the DNS name that we have.
- 
