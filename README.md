# terraform-aws-vpc

## Cloud&Cloud made Terraform Module for AWS Provider

```
module "vpc" {
  source      = "yonetimacademy/vpc/aws"
  version     = "0.0.1"
  tenant      = var.tenant
  name        = var.name
  environment = var.environment

  # VPC Configuration
  cidr_block    = "10.1.0.0/16"
  single_az_nat = false
  pbl_sub_count = [
    {cidr="10.1.8.0/21", zone="b", eip=""}, # 1
    {cidr="10.1.16.0/21", zone="c", eip=""} # 1
  ]
  pvt_sub_count = [
    {cidr="10.1.40.0/21", zone="b"},
    {cidr="10.1.48.0/21", zone="c"}
  ]
  eks_sub_count = [
    {cidr="10.1.72.0/21", zone="b"},
    {cidr="10.1.80.0/21", zone="c"}
  ]
  db_sub_count  = []

  lambda_sub_count = [
    { cidr = "10.1.250.0/24", zone = "a" },
    { cidr = "10.1.251.0/24", zone = "b" }
  ]
}
```

vpc-module---------------
nat.tf --->
lifecycle {
prevent_destroy = false # test den sonra true yap
}

## Notes

1. eip attribute should stay empty if you plan to create new NAT IPs. If you intend to use your existing IP set, you can type-in the Elastic IP allocation id like "eipalloc-053aa42329c5a2784" in each respective subnet map.
