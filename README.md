# AWS Infrastructure

This repository contains all scripts, code and templates for setting up Pythia environments by following the principles of [Infrastructure as Code](https://en.wikipedia.org/wiki/Infrastructure_as_Code) _(also known as Programmable Infrastructure)_.

Each subdirectory contains one step in the bigger process. For more details about each step refer to README in each subdirectory in addition to the short descriptions below. The actual deployment process is described in full in the project wiki.

## [`./infra-templates`](/infra-templates)

Contains executable descriptions of the infrastructure hardware, networking, databases etc. [quasi](http://www.dictionary.com/browse/quasi)physical resources.

## [`./infra-provisioning`](/infra-provisioning)

Contains scripts and definitions for [provisioning](https://en.wikipedia.org/wiki/Provisioning) the required software on project's hardware.
