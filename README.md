# IAC
Using Pipelines to Manage Environments with Infrastructure as Code - Jenkins, Ansible, AWS

This repository shows a very simple example of using Jenkins pipeline to manage AWS Cloud Environment with Ansible Playbooks and roles. It refers some code from my another repo https://github.com/devopscripts/aws which is a sample code of using Ansible to setup AWS VPC, Subnet, Security Group, EC2, ELB2 and etc from scratch.

This repo has two branch, just want to keep it as simple, master and development. The development branch is used to develop infrastructure codes, ansible playbooks and roles in this case. The master branch contains the code after testing merged from development branch.

Jenkins pipeline has two stages: deploy-test and deploy-prod(as I said to keep it simple). Everytime infrastructure engineer commits a change to development branch, Jenkins will start the pipeline to build. In this case, deploy-test will be executed and deploy-prod will be skipped.

When deploy-test is successful, we may want to consider merge to the master and deploy to production environment. Of course, we should perform code review with co-workers before doing that. When development code is merged to master branch, Jenkins will start the pipelien again. But this time, the deploy-prod will be execute and deploy-test will be skipped.

To deploy code to different environments test and prod, different ansible variables input are used in this example. Production variables are placed in prodvar.yml, and test variables are placed in testvar.yml.
