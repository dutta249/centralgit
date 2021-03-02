<!-- VSCode Markdown Exclusions-->
<!-- markdownlint-disable MD025 Single Title Headers-->
# Tapestry AWS Elastic container services (ECS) Terraform Module

## Examples

### basic
```hcl
module "ecs" {
  source                     = "git@github.com:tapestryinc/aws_ecs?ref=v1.0.0"
  aws_ecs_capacity_provider  = true
  ecs_capacity_provider_name = "tapestry"
  ecs_auto_scalling_grp_arn  = "arn:aws:autoscaling:region:123456789012:autoScalingGroup:uuid:autoScalingGroupName/asg-name"
  managed_scaling = [{
    maximum_scaling_step_size = 1
    minimum_scaling_step_size = 1
    status                    = "ENABLED"
    target_capacity           = 2
  }]
  create_cluster = true
  cluster_name   = "tapestry"
  family_name    = "tapestry_family"

  container_definitions_json = <<EOF
  [
      {
        "name": "nginx",
        "image": "nginx",
        "cpu": 10,
        "memory": 128,
        "essential": true,
        "portMappings": [
          {
            "containerPort": 80,
            "hostPort": 80
          }
        ]
      }
  ]
  EOF

  ecs_service_name              = "tapestry_service_name"
  tasks_desired_count           = 1
  tasks_maximum_percent         = 100
  tasks_minimum_healthy_percent = 1

}
```

## Dependencies
### primary
  * [terraform](https://www.terraform.io/)

### nice to have
  * [terraform for vsc](https://github.com/mauve/vscode-terraform)
  * [terraform-config-inspect](https://github.com/hashicorp/terraform-config-inspect)

## Provider Requirements
## Providers

| Name | Version |
|------|---------|
| aws | 3.26.0 |
| terraform | 0.12 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:-----:|
| create\_appmesh\_mesh |  |  | `true` |  |
| app\_mesh\_name |  |  | `tapestry` |  |
| app\_mesh\_spec |  |  | `true` |  |
| app\_mesh\_spec\_egress\_filter |  | `ALLOW\_ALL` | |  |
| app\_mesh\_tags |  |  |  |  |
| create\_appmesh\_virtual\_node |  | `bool` | `true` |  |
| appmesh\_virtual\_node\_name | `value` | `string` | `tapestry` |  |
| appmesh\_virtual\_node\_backend | `value` | `any` |  |  |
| appmesh\_virtual\_node\_backend\_defaults | `value` | `any` |  |  |
| appmesh\_virtual\_node\_listener | `value` | `bool` | `true` |  |
| appmesh\_virtual\_node\_listener\_port | `value` | `number` | `80` |  |
| appmesh\_virtual\_node\_listener\_protocol | `value` | `string` | `http` |  |
| appmesh\_virtual\_node\_listener\_connection\_pool | `value` | `bool` | `false` |  |
| appmesh\_virtual\_node\_listener\_connection\_pool\_grpc | `value` | `any` |  |  |
| appmesh\_virtual\_node\_listener\_connection\_pool\_http | `value` | `any` |  |  |
| appmesh\_virtual\_node\_listener\_connection\_pool\_http2 | `value` | `any` |  |  |
| appmesh\_virtual\_node\_listener\_connection\_pool\_tcp | `value` | `any` |  |  |
| appmesh\_virtual\_node\_listener\_health\_check | `value` | `bool` | `true` |  |
| appmesh\_virtual\_node\_listener\_health\_check\_path | `value` | `string` | `null` |  |
| appmesh\_virtual\_node\_listener\_health\_check\_healthy\_threshold | `value` | `number` | `2` |  |
| appmesh\_virtual\_node\_listener\_health\_check\_unhealthy\_threshold | `value` | `number` | `2` |  |
| appmesh\_virtual\_node\_listener\_health\_check\_interval\_millis | `value` | `number` | `6000` |  |
| appmesh\_virtual\_node\_listener\_health\_check\_timeout\_millis | `value` | `number` | `3000` |  |
| appmesh\_virtual\_node\_listener\_outlier\_detection | `value` | `bool` | `true` |  |
| appmesh\_virtual\_node\_listener\_outlier\_detection\_base\_ejection\_duration\_unit | `value` | `string` | `ms` |  |
| appmesh\_virtual\_node\_listener\_outlier\_detection\_base\_ejection\_duration\_value | `value` | `number` | `0` |  |
| appmesh\_virtual\_node\_listener\_outlier\_detection\_interval\_unit | `value` | `string` | `ms` |  |
| appmesh\_virtual\_node\_listener\_outlier\_detection\_interval\_value | `value` | `number` | `0` |  |
| appmesh\_virtual\_node\_listener\_outlier\_detection\_max\_ejection\_percent | `value` | `number` | `0` |  |
| appmesh\_virtual\_node\_listener\_outlier\_detection\_max\_server\_errors | `value` | `number` | `1` |  |
| appmesh\_virtual\_node\_listener\_timeout | `value` | `bool` | `true` |  |
| appmesh\_virtual\_node\_listener\_timeout\_grpc | `value` | `any` |  |  |
| appmesh\_virtual\_node\_listener\_timeout\_http | `value` | `any` | |  |
| appmesh\_virtual\_node\_listener\_timeout\_http2 | `value` | `any` | |  |
| appmesh\_virtual\_node\_listener\_timeout\_tcp | `value` | `any` | |  |
| appmesh\_virtual\_node\_listener\_tls | `value` | `bool` | `false` |  |
| appmesh\_virtual\_node\_listener\_tls\_certificate\_acm | `value` | `any` | `false` |  |
| appmesh\_virtual\_node\_listener\_tls\_certificate\_file | `value` | `any` | `false` |  |
| appmesh\_virtual\_node\_listener\_tls\_mode | `value` | `string` | `DISABLED` |  |
| appmesh\_virtual\_node\_logging | `value` | `any` |  |  |
| appmesh\_virtual\_node\_service\_discovery | `value` | `any` |  |  |
| appmesh\_virtual\_node\_tags | `value` | `any` |  |  |
| create\_appmesh\_virtual\_router | `wheather want to create appmash virtual router or not.` | `bool` | `true` |  |
| appmesh\_virtual\_router\_name | `value` | `string` | `tapestry` |  |
| appmesh\_virtual\_router\_port | `value` | `number` | `8080` |  |
| appmesh\_virtual\_router\_protocol | `value` | `string` | `http` |  |
| appmesh\_virtual\_router\_tags | `value` | `any` | | |
| create\_appmesh\_virtual\_service | `wheather want to create appmesh virtual service or not.` | `bool` | `true` |  |
| appmesh\_virtual\_service\_name | `value` | `string` | `tapestry` | |
| appmesh\_virtual\_service\_provider | `value` | `bool` | `true` | |
| appmesh\_virtual\_service\_provider\_virtual\_router | `value` | `bool` | `false` | |
| appmesh\_virtual\_service\_provider\_virtual\_node | `value` | `bool` | `false` | |
| appmesh\_virtual\_service\_tags | `value` | `any` | | |
| create\_appmesh\_virtual\_gateway | `value` | `bool` | `true` |  |
| appmesh\_virtual\_gateway\_name | `value` | `string` | `tapestry` |  |
| appmesh\_virtual\_gateway\_backend\_defaults | `value` | `any` |  |  |
| appmesh\_virtual\_gateway\_listener | `value` | `bool` | `true` |  |
| appmesh\_virtual\_gateway\_listener\_port | `value` | `number` | `80` |  |
| appmesh\_virtual\_gateway\_listener\_protocol | `value` | `string` | `http` |  |
| appmesh\_virtual\_gateway\_listener\_connection\_pool | `value` | `bool` | `false` |  |
| appmesh\_virtual\_gateway\_listener\_connection\_pool\_grpc | `value` | `any` |  |  |
| appmesh\_virtual\_gateway\_listener\_connection\_pool\_http | `value` | `any` |  |  |
| appmesh\_virtual\_gateway\_listener\_connection\_pool\_http2 | `value` | `any` |  |  |
| appmesh\_virtual\_gateway\_listener\_connection\_pool\_tcp | `value` | `any` |  |  |
| appmesh\_virtual\_gateway\_listener\_health\_check | `value` | `bool` | `true` |  |
| appmesh\_virtual\_gateway\_listener\_health\_check\_path | `value` | `string` | `null` |  |
| appmesh\_virtual\_gateway\_listener\_health\_check\_healthy\_threshold | `value` | `number` | `2` |  |
| appmesh\_virtual\_gateway\_listener\_health\_check\_unhealthy\_threshold | `value` | `number` | `2` |  |
| appmesh\_virtual\_gateway\_listener\_health\_check\_interval\_millis | `value` | `number` | `6000` |  |
| appmesh\_virtual\_gateway\_listener\_health\_check\_timeout\_millis | `value` | `number` | `3000` |  |
| appmesh\_virtual\_gateway\_listener\_tls | `value` | `bool` | `false` |  |
| appmesh\_virtual\_gateway\_listener\_tls\_certificate\_acm | `value` | `any` |  |  |
| appmesh\_virtual\_gateway\_listener\_tls\_certificate\_file | `value` | `any` |  |  |
| appmesh\_virtual\_gateway\_listener\_tls\_mode | `value` | `string` | `DISABLED` |  |
| appmesh\_virtual\_gateway\_logging | `value` | `any` |  |  |
| appmesh\_virtual\_gateway\_tags | `value` | `any` |  |  |


## Outputs

| Name | Description |
|------|-------------|
| cluster\_arn| The Amazon Resource Name (ARN) that identifies the cluster | 
| capacity\_provider\_name| Name of the provisioned capacity provider | 
| capacity\_provider\_id| id of capacity provider | 
| capacity\_provider\_arn| The Amazon Resource Name (ARN) that identifies the capacity provider | 
| cluster\_name| Name of cluster|
| cluster\_id| id of cluster | 
| ecs\_service\_name| Name of The service |
| ecs\_service\_id| id of ecs service | 
|  ecs\_service\_iam\_role| The ARN of IAM role used for ELB | 
| ecs\_service\_cluster| The Amazon Resource Name (ARN) of cluster which the service runs on | 
| ecs\_service\_desired\_count| The number of instances of the task definition | 
| aws\_ecs\_task\_definition\_arn| Full ARN of the Task Definition (including both family and revision). | 
| aws\_ecs\_task\_definition\_family| The family of the Task Definition.| 
|aws\_ecs\_task\_definition\_revision| The revision of the task in a particular family. | 
| autoscaling\_group\_arn| aws autoscaling group arn | 

