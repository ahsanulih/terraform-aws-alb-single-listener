# terraform-aws-alb-single-listener

[![Terraform Version](https://img.shields.io/badge/Terraform%20Version->=0.13.0,<=0.13.7-blue.svg)](https://releases.hashicorp.com/terraform/)
[![Release](https://img.shields.io/github/release/traveloka/terraform-aws-alb-single-listener.svg)](https://github.com/traveloka/terraform-aws-alb-single-listener/releases)
[![Last Commit](https://img.shields.io/github/last-commit/traveloka/terraform-aws-alb-single-listener.svg)](https://github.com/traveloka/terraform-aws-alb-single-listener/commits/master)
[![Issues](https://img.shields.io/github/issues/traveloka/terraform-aws-alb-single-listener.svg)](https://github.com/traveloka/terraform-aws-alb-single-listener/issues)
[![Pull Requests](https://img.shields.io/github/issues-pr/traveloka/terraform-aws-alb-single-listener.svg)](https://github.com/traveloka/terraform-aws-alb-single-listener/pulls)
[![License](https://img.shields.io/github/license/traveloka/terraform-aws-alb-single-listener.svg)](https://github.com/traveloka/terraform-aws-alb-single-listener/blob/master/LICENSE)
![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.png?v=103)

## Table of Content

* [terraform-aws-alb-single-listener](#terraform-aws-alb-single-listener)
   * [Table of Content](#table-of-content)
   * [Description](#description)
   * [Examples](#examples)
   * [Terraform Version](#terraform-version)
   * [Requirements](#requirements)
   * [Providers](#providers)
   * [Modules](#modules)
   * [Resources](#resources)
   * [Inputs](#inputs)
   * [Outputs](#outputs)
   * [Contributing](#contributing)
   * [Authors](#authors)
   * [License](#license)

## Description
A terraform module which provisions a DNS record that points to an Application LB with a single listener

## Examples

* [Frontend, Backend, and Default Tags ](https://github.com/traveloka/terraform-aws-alb-single-listener/tree/master/examples/frontend-backend-and-default-tgs)
* [Simple ALB Single Listener](https://github.com/traveloka/terraform-aws-alb-single-listener/tree/master/examples/simple)

## Terraform Version

This module was created on 4/17/2018.
The latest stable version of Terraform which this module tested working is Terraform 0.13.7 on 07/10/2021.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_random_lb"></a> [random\_lb](#module\_random\_lb) | github.com/traveloka/terraform-aws-resource-naming.git | v0.20.0 |
| <a name="module_random_tg"></a> [random\_tg](#module\_random\_tg) | github.com/traveloka/terraform-aws-resource-naming.git | v0.20.0 |

## Resources

| Name | Type |
|------|------|
| [aws_lb.main](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb) | resource |
| [aws_lb_listener.main](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb_listener) | resource |
| [aws_lb_listener_rule.main](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb_listener_rule) | resource |
| [aws_lb_target_group.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb_target_group) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_cluster_role"></a> [cluster\_role](#input\_cluster\_role) | Primary role/function of the cluster. Example value: 'app', 'fe', 'mongod', etc | `string` | n/a | yes |
| <a name="input_description"></a> [description](#input\_description) | Will be used in resources' Description tag | `string` | n/a | yes |
| <a name="input_environment"></a> [environment](#input\_environment) | Will be used in resources' Environment tag | `string` | n/a | yes |
| <a name="input_lb_idle_timeout"></a> [lb\_idle\_timeout](#input\_lb\_idle\_timeout) | The LB's idle timeout | `string` | `60` | no |
| <a name="input_lb_internal"></a> [lb\_internal](#input\_lb\_internal) | Whether the LB will be public / private | `string` | `"1"` | no |
| <a name="input_lb_ip_address_type"></a> [lb\_ip\_address\_type](#input\_lb\_ip\_address\_type) | The LB's ip address type | `string` | `"ipv4"` | no |
| <a name="input_lb_drop_invalid_header_fields"></a> [lb\_drop\_invalid\_header\_fields](#input\_lb\_drop\_invalid\_header\_fields) | The LB's attribute to drop invalid header fields | `string` | `false` | no |
| <a name="input_lb_logs_s3_bucket_name"></a> [lb\_logs\_s3\_bucket\_name](#input\_lb\_logs\_s3\_bucket\_name) | The S3 bucket that will be used to store LB access logs | `string` | n/a | yes |
| <a name="input_lb_name"></a> [lb\_name](#input\_lb\_name) | The name of the LB, will override the default <service\_name>-<lb\_type>-<random\_string> name | `string` | `""` | no |
| <a name="input_lb_security_groups"></a> [lb\_security\_groups](#input\_lb\_security\_groups) | List of security group IDs for the LB | `list(string)` | n/a | yes |
| <a name="input_lb_subnet_ids"></a> [lb\_subnet\_ids](#input\_lb\_subnet\_ids) | List of subnet IDs of the LB | `list(string)` | n/a | yes |
| <a name="input_lb_tags"></a> [lb\_tags](#input\_lb\_tags) | The additional LB tags that will be merged over the default tags | `map(string)` | `{}` | no |
| <a name="input_listener_certificate_arn"></a> [listener\_certificate\_arn](#input\_listener\_certificate\_arn) | The LB listener's certificate ARN | `string` | n/a | yes |
| <a name="input_listener_port"></a> [listener\_port](#input\_listener\_port) | The LB listener's port | `string` | `443` | no |
| <a name="input_listener_protocol"></a> [listener\_protocol](#input\_listener\_protocol) | The LB listener's protocol | `string` | `"HTTPS"` | no |
| <a name="input_listener_rules"></a> [listener\_rules](#input\_listener\_rules) | A map of listener rules for the LB: priority --> {target\_group\_arn:'', conditions:[]}. 'target\_group\_arn:null' means the built-in target group | `map(any)` | `{}` | no |
| <a name="input_listener_ssl_policy"></a> [listener\_ssl\_policy](#input\_listener\_ssl\_policy) | The LB listener's SSL policy | `string` | `"ELBSecurityPolicy-2016-08"` | no |
| <a name="input_product_domain"></a> [product\_domain](#input\_product\_domain) | Abbreviation of the product domain the created resources belong to | `string` | n/a | yes |
| <a name="input_service_name"></a> [service\_name](#input\_service\_name) | The service name that will be used in tags and resources default name | `string` | n/a | yes |
| <a name="input_tg_deregistration_delay"></a> [tg\_deregistration\_delay](#input\_tg\_deregistration\_delay) | The default target group's deregistration delay | `string` | `300` | no |
| <a name="input_tg_health_check"></a> [tg\_health\_check](#input\_tg\_health\_check) | The default target group's health check configuration, will be merged over the default (see locals.tf) | `map(string)` | `{}` | no |
| <a name="input_tg_name"></a> [tg\_name](#input\_tg\_name) | The default target group's name, will override the default <service\_name>-default name | `string` | `""` | no |
| <a name="input_tg_port"></a> [tg\_port](#input\_tg\_port) | The default target group's port | `string` | `5000` | no |
| <a name="input_tg_protocol"></a> [tg\_protocol](#input\_tg\_protocol) | The default target group's protocol | `string` | `"HTTP"` | no |
| <a name="input_tg_protocol_version"></a> [tg\_protocol\_version](#input\_tg\_protocol\_version) | The default target group's protocol version | `string` | `"HTTP1"` | no |
| <a name="input_tg_slow_start"></a> [tg\_slow\_start](#input\_tg\_slow\_start) | Amount time for targets to warm up before the load balancer sends them a full share of requests. The range is 30-900 seconds or 0 to disable. The default value is 0 seconds. | `string` | `0` | no |
| <a name="input_tg_stickiness"></a> [tg\_stickiness](#input\_tg\_stickiness) | The default target group's stickiness configuration | `map(string)` | <pre>{<br>  "cookie_duration": 1,<br>  "enabled": true,<br>  "type": "lb_cookie"<br>}</pre> | no |
| <a name="input_tg_tags"></a> [tg\_tags](#input\_tg\_tags) | The additional Target Group tags that will be merged over the default tags | `map(string)` | `{}` | no |
| <a name="input_tg_target_type"></a> [tg\_target\_type](#input\_tg\_target\_type) | The type of target that you must specify when registering targets with this target group. | `string` | `"instance"` | no |
| <a name="input_vpc_id"></a> [vpc\_id](#input\_vpc\_id) | The default target group's VPC | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_lb_arn"></a> [lb\_arn](#output\_lb\_arn) | The ARN of the ALB |
| <a name="output_lb_arn_suffix"></a> [lb\_arn\_suffix](#output\_lb\_arn\_suffix) | The ARN suffix of the ALB, useful with CloudWatch Metrics |
| <a name="output_lb_dns"></a> [lb\_dns](#output\_lb\_dns) | The DNS name of the load balancer |
| <a name="output_lb_zone_id"></a> [lb\_zone\_id](#output\_lb\_zone\_id) | The canonical hosted zone ID of the load balancer (to be used in a Route 53 Alias record) |
| <a name="output_listener_arn"></a> [listener\_arn](#output\_listener\_arn) | The ARN of the listener |
| <a name="output_listener_id"></a> [listener\_id](#output\_listener\_id) | The ID of the listener |
| <a name="output_tg_arn"></a> [tg\_arn](#output\_tg\_arn) | The arn of the default target group |
| <a name="output_tg_arn_suffix"></a> [tg\_arn\_suffix](#output\_tg\_arn\_suffix) | The arn suffix of the default target group, useful with CloudWatch Metrics |
| <a name="output_tg_name"></a> [tg\_name](#output\_tg\_name) | The name of the target group |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Contributing

This module accepting or open for any contributions from anyone, please see the [CONTRIBUTING.md](https://github.com/traveloka/terraform-aws-alb-single-listener/blob/master/CONTRIBUTING.md) for more detail about how to contribute to this module.

## Authors

* [Salvian Reynaldi](https://github.com/salvianreynaldi)

## License

This module is under Apache License 2.0 - see the [LICENSE](https://github.com/traveloka/terraform-aws-alb-single-listener/blob/master/LICENSE) file for details.
