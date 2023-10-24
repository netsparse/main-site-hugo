---
layout: post
author: Angel
date: 2023-09-23T08:55:23-05:00
title: "Spin Up Cloud Resources with AWS and Terraform (Incomplete)"
tags: ["aws", "cloud", "ec2", "terraform"]
description:
showToc: true
TocOpen: false
hidemeta: false
comments: true
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
draft: true
---

EC2 instances are virtual machines that are rented out by Amazon Web Services (AWS) to users who need computing resources in the cloud, they can be configured with different operating systems, hardware configurations, and software applications to meet a wide range of computing needs.

In this guide, we'll implement an EC2 instance on AWS utilizing Terraform.

If you are new to Terraform or want to learn more, check out my previous post on [Getting Started with Terraform](/posts/get-started-with-terraform). 

## Prerequisites

Before getting started with Terraform, you need to have the following:

- An account with a cloud provider (e.g., AWS, Azure, Google Cloud)
- Terraform installed on your machine
- Basic knowledge of the provider's services you will be using
- A text editor (e.g., VS Code, Atom, Sublime)

## Setup

### Provider Credentials

To interact with a cloud provider using Terraform, you need to provide your provider credentials in a `provider.tf` file. 

For example, with AWS, you need to set your AWS access key and secret key.

```
provider "aws" {
  access_key = "YOUR_AWS_ACCESS_KEY"
  secret_key = "YOUR_AWS_SECRET_KEY"
  region     = "us-west-2"
}
```

**Note: It's best practice to store your credentials in environment variables, rather than hardcoding them in the configuration file.**

### Define Resources

Let's create an EC2 instance in AWS.

```
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "ExampleInstance"
  }
}
```

In the above example, we define an EC2 instance with the `ami` and `instance_type` attributes. 

We also define a `tags` attribute.

### Initialize and Apply

After defining your infrastructure, you need to initialize the Terraform configuration by running the following command:

```
terraform init
```

This command downloads the necessary provider plugins and sets up the backend to store the state of your infrastructure.

Once initialization is complete, you can apply the configuration by running:

```
terraform apply
```

This command will create the EC2 instance. 

You'll be prompted to confirm the changes before Terraform proceeds.

### View Your Infrastructure

To view your infrastructure, you can use the AWS console or the AWS CLI. 

You can also use Terraform to output the attributes of your resources by running:

```
terraform output
```

This command will display the attributes of the `aws_instance.example` resource, including the instance ID, public IP address, and more.

## Conclusion

In this guide, we covered the basic steps to get started with HashiCorp Terraform. 

We defined a provider, created an EC2 instance, initialized the configuration, applied the changes, and viewed the output. 

With Terraform, you can define and manage your infrastructure as code, making it easier to manage, replicate, and scale your infrastructure.

## Learn More

Also make sure to check out HashiCorp's [official documentation](https://developer.hashicorp.com/terraform/intro), and [tutorials](https://developer.hashicorp.com/terraform/tutorials).