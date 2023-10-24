---
layout: post
author: Angel
date: 2023-08-19T12:45:54-05:00
title: "Manage Your Cloud Resources With Terraform"
tags: ["aws", "cloud", "ec2", "terraform"]
showToc: true
TocOpen: false
hidemeta: false
comments: true
#canonicalURL: "https://canonical.url/to/page"
disableHLJS: false # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
draft: false
---

[Terraform](https://www.terraform.io/) is a tool that allows you to define, manage, and provision resources in the cloud. 

It uses a declarative syntax to define infrastructure resources as code, which allows you to make it easier to track changes, instead of relying on the traditional UI of the provider.

In this guide, we will cover the basics of getting started with Terraform.

Here's a quick overview from [Fireship.io](https://fireship.io/).

{{< ytlazy tomUWcQ0P3k >}}


## Components

### Providers 

Providers are plugins that Terraform uses to interact with a cloud provider. 

- Examples include AWS, Google Cloud Platform, and Azure.

### Resources

Resources are the infrastructure components that you manage with Terraform. 

- Such as EC2 instances, S3 buckets, and VPCs.

### Data Sources 

Data sources are read-only resources that allow you to fetch information about existing infrastructure. 

Including the list of available AMIs in AWS, or the IP address of a DNS server.

### Modules 

Modules are reusable Terraform configurations that can be used to manage a set of related resources. They enable you to create your own abstractions and encapsulate complex infrastructure components.

## Terraform File Types

Terraform uses the [HashiCorp Configuration Language (HCL)](https://developer.hashicorp.com/terraform/language) to define your infrastructure. 

HCL is a configuration language that is easy to read and write, and enables you to define complex configurations in a human-readable format.

Terraform files typically have a `.tf` extension, there are two main types.

- **Main Configuration Files**: These files define the infrastructure you want to create or manage. They typically contain the provider and resource blocks that define the cloud provider you are using and the resources you want to create or manage.
- **Module Files**: These files define reusable modules that can be used across multiple Terraform configurations.

## Example `.tf` Files

### Provider Configuration

This configuration sets up the AWS provider and specifies the region to use.

```hcl
provider "aws" {
  region = "us-east-1"
}
```

### Instance Resources

This configuration creates an EC2 instance in AWS with the specified AMI and instance type, and assigns it the name "Web Server".

```hcl
resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "Web Server"
  }
}
```

### Module Configuration

This configuration creates a module named `"web_servers"` that uses a module located in the `./modules/ec2-instances` directory. 

It specifies that it wants to create two instances of type `t2.micro`.

```hcl
module "web_servers" {
  source = "./modules/ec2-instances"

  instance_count = 2
  instance_type  = "t2.micro"
}
```

## Get Started

### Installation

Grab the latest release for your platform [here](https://developer.hashicorp.com/terraform/downloads).

### Requirements
- A Linux, macOS, or Windows system
- Basic knowledge of [HCL syntax](https://developer.hashicorp.com/terraform/language/syntax/configuration)
- An account with any supported [provider](https://registry.terraform.io/browse/providers)

## Workflow

### Setup a Provider

To get started with Terraform, create a new directory and create a file named `provider.tf` with a similar structure as below:

```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```
Input the information for your specific `provider`, `region`, `ami` and `instance_type`.

In this example, we are creating an EC2 instance in the `us-west-2` region using `ami-0c55b159cbfafe1f0` and the `t2.micro` instance type.


### Initialize

To initialize the working directory, run the following:

```
terraform init
```

This will download the necessary plugins and initialize the Terraform backend.

### Validate

To validate the Terraform configuration:

```
terraform validate
```
This will validate the syntax and configuration of your Terraform files.

### Plan

Preview the changes that Terraform will make:

```
terraform plan
```

### Apply

To apply the Terraform configuration:

```
terraform apply
```

This will create the infrastructure resources defined in your Terraform configuration.

### Review

Review the changes that Terraform made to your infrastructure:

```
terraform show
```

### Destroy

To destroy the infrastructure resources:

```
terraform destroy
```

## Conclusion

In this guide, we have covered the basics of getting started with Terraform.

It is a powerful tool that enables you to manage your cloud resources in a repeatable and consistent way. 

By using Terraform, you can define your infrastructure as code, and manage it like any other software project by defining your providers, resources, data sources, and modules, with the use of `.tf` files and `HCL`.

## Learn More

For more info, make sure to check out the [official documentation](https://developer.hashicorp.com/terraform/intro), and [tutorials](https://developer.hashicorp.com/terraform/tutorials).

### Additional

- [Tutorial Library](https://developer.hashicorp.com/tutorials/library?product=terraform)
- [Terraform Registry](https://registry.terraform.io/)
- [Yevgeniy Brikman's Terraform Up & Running](https://www.terraformupandrunning.com/?ref=ybrikman-home)