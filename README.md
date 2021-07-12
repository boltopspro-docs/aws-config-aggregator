<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/aws-config-aggregator/blob/master/README.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

# AWS Config Aggregator CloudFormation Blueprint

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

This blueprint creates an [AWS Config Aggregator](https://docs.aws.amazon.com/config/latest/developerguide/setup-aggregator-console.html).  This aggregates AWS Config data from multiple regions and multiple accounts. This does not enable Config, it just sets up the Aggregator.

Related Blueprints:

* [boltopspro/aws-config-aggregator](https://github.com/boltopspro-docs/aws-config-aggregator)
* [boltopspro/aws-config-bucket](https://github.com/boltopspro-docs/aws-config-bucket)
* [boltopspro/enable-aws-cloudtrail](https://github.com/boltopspro-docs/enable-aws-cloudtrail)
* [boltopspro/enable-aws-config](https://github.com/boltopspro-docs/enable-aws-config)
* [boltopspro/enable-aws-guardduty](https://github.com/boltopspro-docs/enable-guardduty)

## Usage

1. Add blueprint to Gemfile
2. Configure: configs/aws-config-aggregator values
3. Deploy

## Add

Add the blueprint to your lono project's `Gemfile`.

```ruby
gem "aws-config-aggregator", git: "git@github.com:boltopspro/aws-config-aggregator.git"
```

## Configure

First you want to configure the [configs](https://lono.cloud/docs/core/configs/) files. Use [lono seed](https://lono.cloud/reference/lono-seed/) to configure starter values quickly.

    LONO_ENV=development lono seed aws-config-aggregator

To deploy to additional environments:

    LONO_ENV=production  lono seed aws-config-aggregator

The generated files in `config/aws-config-aggregator` folder look something like this:

    configs/aws-config-aggregator/
    ├── params
    │   ├── development.txt
    │   └── production.txt
    └── variables
        ├── development.rb
        └── production.rb

The default name of the Aggregator is the stack name.  You can change the name with params:

    ConfigurationAggregatorName=my-Aggregator

To set the accounts and regions, use variables:

```ruby
@account_ids = ["111111111111", "222222222222"]
@aws_regions = ["us-west-2", "us-east-1"]
```

## Deploy

Use the [lono cfn deploy](http://lono.cloud/reference/lono-cfn-deploy/) command to deploy. Example:

    LONO_ENV=development lono cfn deploy aws-config-aggregator-development --blueprint aws-config-aggregator --sure
    LONO_ENV=production  lono cfn deploy aws-config-aggregator-production  --blueprint aws-config-aggregator --sure
