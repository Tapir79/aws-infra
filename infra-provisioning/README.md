# Software Provisioning

All software provisioning is done with [Ansible](https://www.ansible.com/).

> Contrary to more traditional setups, in Pythia Ansible does not manage the hardware inventory. Instead hardware provisioning is done with scripts in the [infra-templates/](../infra-templates/) directory.

## Prerequisites

 - [Ansible 2.x (_latest_) is installed](http://docs.ansible.com/ansible/latest/intro_installation.html). There are multiple ways to install Ansible depending on platform.
 - Ansible Galaxy dependencies have been installed. To do so, execute
    ```sh
    ansible-galaxy install -r requirements.yml
    ```
 - User has [AWS Acess Key ID and Secret Access Key](http://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys) with following AWS Managed Policies assigned:
   - `AmazonEC2ReadOnlyAccess`, `AmazonRDSReadOnlyAccess`
 - Infrastructure resources have been provisioned using [infra-templates](../infra-templates)

## Running provisioning scripts

 1. Set your AWS Access Key ID and Secret Access Key as environment variables _(see [AWS CLI: Environment Variables](http://docs.aws.amazon.com/cli/latest/userguide/cli-environment.html))_
 1. To provision Delphi environment, execute the [`delphi.yml`] script with Ansible by running the command below:
    ```sh
    ansible-playbook -i ec2.py delphi.yml
    ```
    > You may add -v, -vv or -vvvv to increase the debug output of Ansible.
    
    During execution you may see something similar to following a few times:
    
    > The authenticity of host '52.16.211.132 (52.16.211.132)' can't be established.
    >  ECDSA key fingerprint is SHA256:UG81jtF5S8vsJNmmTtvpOkPAprk3+OqgVxkYN7vs4+Q.
    >  Are you sure you want to continue connecting (yes/no)?
    
    For each of these, type _"yes"_ (without quotes) and hit enter

## Files in this Directory

 - [`ansible.cfg`](ansible.cfg) contains a few modifications to Ansible defaults, mainly to enable development on macOS environments
 - [`requirements.yml`](requirements.yml) External Ansible Roles requirements
 - [`ec2.py`](ec2.py) and [`ec2.ini`](ec2.ini) Ansible dynamic inventory, see below.
 - [`support.yml`](support.yml) Playbook for Support VPC

## External components

### Ansible Inventory

This repository uses the Ansible Contrib EC2 dynamic inventory script to connect to AWS

https://github.com/ansible/ansible/tree/devel/contrib/inventory

To learn more about dynamic inventories, read [Ansible Docs: Dynamic Inventory](http://docs.ansible.com/ansible/latest/intro_dynamic_inventory.html)

### Oracle JDK Installation Roles

Pythia uses exclusively Oracle Java for its runtimes. To make things easier, the playbook utilizes [ansiblebit.oracle-java](https://github.com/ansiblebit/oracle-java) Roles available at [Ansible Galaxy](https://galaxy.ansible.com/ansiblebit/oracle-java/) for its installation.
