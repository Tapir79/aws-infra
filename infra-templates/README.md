# Programmable Infrastructure Templates

This directory contains the necessary cloud infrastructure definitions for Pythia as [AWS CloudFormation](https://aws.amazon.com/cloudformation/) templates.

## Prerequisites

These CF templates require administrator access to AWS Management Console.

## Files in this Directory

 - [`delphi-vpc.json`](delphi-vpc.json) "Delphi" is the application runtime VPC which is present in all environments. It contains all EC2 resources for Docker, S3 bucket, RDS instances etc. needed to actually run the applications.
 - [`support-vpc.json`](support-vpc.json) Support VPC contains [Bastion host](https://en.wikipedia.org/wiki/Bastion_host) for administrative access and necessary build infrastructure.
