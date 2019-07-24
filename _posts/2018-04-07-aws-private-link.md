---
layout: post
title: AWS Private Link
comments: true /*disqus comments enabled for this post*/
description: Expose your services hosted in Private Data Center over AWS.
keywords: AWS, Private-link, NLB, Target-groups, Route53
---

This post explains how to expose your services hosted in your private data center to AWS accounts over AWS. I assume that you already have some understanding about Amazon Web Services and how things work in the world of AWS Cloud Services.
To begin with let's first understand what is the new Private Link service launched by AWS in re:Invent 2017.

In re:Invent 2017, AWS announced a new service called Private Link. According to the [announcement](https://aws.amazon.com/blogs/aws/new-aws-privatelink-endpoints-kinesis-ec2-systems-manager-and-elb-apis-in-your-vpc/), "AWS PrivateLink is the newest generation of VPC Endpoints which is designed for customers to access AWS services in a highly available and scalable manner, while keeping all the traffic within the AWS network". What this means is, you can create your own VPC endpoint in your AWS account and access services which are hosted in other AWS accounts. This service can be further extended and used to access services via endpoints hosted in your private data center.

In this blog post, I am going to explain how we can expose our service not hosted in AWS, but hosted in your private data center, to other accounts on AWS. So let's begin.

## AWS Direct Connect
AWS Direct Connect is one of the services provided by AWS which enables you to establish a dedicated network connection from your data center to AWS. This service is nothing but a VPN connection from your AWS account to your data center. You need to establish this because this is how your AWS account is going to talk to your service hosted in private data center.

## Architecture
