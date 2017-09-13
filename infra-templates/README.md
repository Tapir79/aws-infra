# Programmable Infrastructure Templates

This directory contains the necessary cloud infrastructure definitions for Pythia as [AWS CloudFormation](https://aws.amazon.com/cloudformation/) templates.

## Prerequisites

These CF templates require administrator access to AWS Management Console.

## Provisioning AWS Infrastructure

 1. Login to AWS console
 1. Navigate to [AWS CloudFormation console](https://eu-west-1.console.aws.amazon.com/cloudformation/home)
 1. Create stack from templates in this directory in this order. Wait for each creation to finish _(status: `CREATE_COMPLETE`)_ before moving to next one.
    1. [`delphi-networking.json`](delphi-networking.json) _("Delphi" environment)_ This template creates AWS VPC and related networking resources such as route table and security groups.
    1. [`jenkins-cluster.json`](jenkins-cluster.json) This template adds Jenkins cluster to Delphi.
    1. [`docker-cluster.json`](docker-cluster.json) This template adds Docker cluster to Delphi.
 1. Configure SSH proxying:
    ```bash
    Host 10.*.*.*
        User centos
        IdentityFile ~/.ssh/Pythia_QA.pem
        ProxyCommand ssh -q -W %h:%p pythia-qa-bastion
    
    Host pythia-qa-bastion
        HostName <BASTION_IP_HERE>
        User centos
        IdentityFile ~/.ssh/Pythia_QA.pem
        ForwardAgent yes
    ```
    Replace `<BASTION_IP_HERE>` with IP in the `Outputs` section of the `delphi-networking` CloudFormation Stack labeled _"BastionHostIP"_
 1. Execute [infra-provisioning](../infra-provisioning/) playbook as described in its README.

    > This configuration file is usually located at path `~/.ssh/config`. However depending on your OS/environment the actual path may differ.
