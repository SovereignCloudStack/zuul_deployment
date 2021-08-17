# Zuul-CI deployment

This repository contains the SCS Zuul-CI installation setup.
Zuul-CI is a gating system which goes beyond normal CI-CD pipeline functionality.


## How to add a repository

If you want to add your SCS repository to zuul, you also have to create a PR in here.
The file to touch is *ansible/main.yml*. In the playbooks **role** section
you'll find a single role. From there, go to
```yaml
vars.tenants[0].tenant.source.scszuulapp.untrusted-projects
```
and add your repository in here. Preferably in alphabetical order.


## Setup

Installation steps


### Github App

In oder to have Zuul-CI working with GitHub you need to setup a GitHub app.
A guide on how to setup this app can be found here:
https://github.com/tibeerorg/zuul_setup


### Infrastructure as Code (IaC)

Done via Terraform.
Export an os `OS_CLOUD` variable with the corresponding value of your OpenStack clouds.yaml to deploy.
```bash
cd terraform
terraform apply -auto-approve
```


### Provisioning

Done via Ansible. Automatically performed on changes in main branch.
```bash
cd ansible
ansible-playbook --extra-vars "webhook_token=webhooksecretvalue db_user_pass=userpassword db_root_pass=rootpassword" main.yaml
```


## License

Apache License 2.0
