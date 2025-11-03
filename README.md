Reusable VPC + NAT + S3 Endpoint (Terraform)

Spin up a clean, production-style VPC scaffold in us-east-1 with:

1 VPC (10.112.0.0/16)

2 public subnets (1a, 1b) + 4 private subnets (1a, 1b)

Internet Gateway for public subnets

NAT Gateway in a public subnet for private egress

S3 Gateway VPC Endpoint (private access to S3)

Helpful outputs: vpc_id, public_subnet_ids, private_subnet_ids, nat_gateway_id, s3_endpoint_id

⚠️ Cost note: A NAT Gateway costs money while running (plus EIP). When you’re done, run terraform destroy.

Why this repo

I want a repeatable, “copy-paste-ready” VPC baseline I can:

Clone into a new folder/repo,

Search/replace the project name and (optionally) CIDRs,

terraform apply and keep moving—no Console clicking, no reverse-engineering.

What’s inside

vpc.tf – VPC + IGW + baseline tags

subnets.tf – 2 public + 4 private subnets (a/b)

route.tf – Public and private route tables + associations

nat.tf – Elastic IP + NAT Gateway + private routes through NAT

endpoint-s3.tf – S3 Gateway Endpoint attached to route tables

outputs.tf – IDs you’ll need for later stacks (EC2, ALB, RDS, etc.)

.gitignore – Keeps state, crash logs, tfvars, and editor noise out of Git

Variables are intentionally minimal; rename/tag/CIDR edits are simple search/replace to keep this “grab-and-go”.

Prereqs

Terraform ≥ 1.3

AWS CLI configured (aws sts get-caller-identity should work)

IAM permissions for VPC, Subnet, RouteTable, NAT/EIP, and Endpoints
