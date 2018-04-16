# Using the module with an existing Route53 zone

If you already have a Route53 hosted zone for the domain, the `aws_route53_zone` data source should be used to find the zone ID.

```hcl
data "aws_route53_zone" "zone" {
    name = "example.com."
}

module "route53_o365" {
    source = "tiguard/route53-o365/aws"

    domain          = "example.com"
    zone_id         = "${data.aws_route53_zone.zone.zone_id}"
    ms_txt          = "ms12345678"
    enable_exchange = true
    enable_sfb      = true
    enable_mdm      = true
}
```