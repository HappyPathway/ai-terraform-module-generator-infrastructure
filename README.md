# AI Terraform Module Generator Infrastructure

Infrastructure as Code (IaC) for deploying the AI Terraform Module Generator on AWS. This repository contains all the Terraform configurations needed to set up the production environment.

## Architecture Components

- ECS Fargate clusters for containerized services
- RDS PostgreSQL databases
- ElastiCache Redis cluster
- Application Load Balancer
- VPC networking setup
- CloudWatch monitoring
- IAM roles and policies
- S3 buckets for module storage
- Route53 DNS configuration

## Prerequisites

- AWS CLI configured with appropriate credentials
- Terraform 1.5+
- Docker for building container images

## Quick Start

1. Clone the repository:
```bash
git clone https://github.com/HappyPathway/ai-terraform-module-generator-infrastructure.git
```

2. Initialize Terraform:
```bash
terraform init
```

3. Configure variables:
```bash
cp terraform.tfvars.example terraform.tfvars
# Edit terraform.tfvars with your configuration
```

4. Deploy:
```bash
terraform apply
```

## Configuration

### Required Variables

- `aws_region`: AWS region to deploy to
- `environment`: Deployment environment (dev/staging/prod)
- `vpc_cidr`: VPC CIDR range
- `domain_name`: Domain name for the application
- `db_instance_class`: RDS instance type
- `redis_node_type`: ElastiCache node type

See `variables.tf` for all available variables and their descriptions.

## Module Organization

```
├── environments/          # Environment-specific configurations
│   ├── dev/
│   ├── staging/
│   └── prod/
├── modules/              # Reusable Terraform modules
│   ├── ecs/             # ECS cluster and services
│   ├── rds/             # RDS database
│   ├── redis/           # ElastiCache cluster
│   ├── networking/      # VPC and network resources
│   └── security/        # Security groups and IAM
├── main.tf              # Main Terraform configuration
└── outputs.tf           # Output definitions
```

## Deployment Instructions

### Initial Deployment

1. Configure AWS credentials:
```bash
aws configure
```

2. Create backend state bucket:
```bash
aws s3api create-bucket --bucket your-tf-state-bucket --region your-region
```

3. Deploy infrastructure:
```bash
terraform init
terraform plan
terraform apply
```

### Updates

1. Make changes to Terraform configurations
2. Run:
```bash
terraform plan  # Review changes
terraform apply # Apply changes
```

## Monitoring and Maintenance

- CloudWatch dashboards are available at AWS Console
- Logs are centralized in CloudWatch Logs
- Metrics are available in CloudWatch Metrics
- Regular maintenance tasks are documented in [maintenance.md](docs/maintenance.md)

## Security

- All databases are encrypted at rest
- SSL/TLS enabled for all services
- Security groups restrict access appropriately
- IAM roles follow least privilege principle
- Regular security patches via automated updates

## Related Repositories

- [Main Project](https://github.com/HappyPathway/ai-terraform-module-generator)
- [Frontend Service](https://github.com/HappyPathway/ai-terraform-module-generator-frontend)
- [Backend Service](https://github.com/HappyPathway/ai-terraform-module-generator-backend)

## License

MIT License - see [LICENSE](LICENSE) for details