# Build A Phish

Table of contents 
------------------
  * [Overview](#overview)
  * [Features](#features)
  * [Containers](#containers)
  * [Setup](#setup)
  * [Usage](#usage)
  
## Overview

Build a Phish consist of a Ansible playbook to deploy a phishing engagement in the cloud. The Playbook combines both Terraform & Ansible to deploy and configure virtual machines for different use cases. This playbook is highly customizable and includes operational security out of box. The design of this playbook is much more then automation. This playbook implements real world TTP’s to improve OPSEC, lower operational cost and speedup deployment time. This project is the real-world demonstration from the Black Hills Information Security Webcast “How to Build a Phishing Engagement - Coding TTP's”

## Features

* Pure Ansible playbook with low dependencies and easy modification.
* Security from the ground up
* Docker containers for each application.
* Designed around a phishing engagement

## Containers

- Evilginx2
- Gophish
- Nginx

## Cloud Providers

- Digital Ocean
- Azure

## Webcast

Coming Soon

## Blog Post

Coming Soon

## Requirements

 - Ansible
 - Terraform
 - (optional) Secrets Provider cli
    - lpass
    - op
    - bw
 - MacOS or Linux. I have not tested with Windows though it SHOULD work.

## Setup

1. Install Ansible & Terraform
   
   `brew install terraform ansible`

2. Git clone this repo 

    `git clone https://github.com/ralphte/build_a_phish`

3. Customize the variables inside the vars folder.
4. Create API keys for both Digital Ocean & Azure.

    - Digital Ocean API Key https://www.digitalocean.com/docs/apis-clis/api/create-personal-access-token/#:~:text=To%20generate%20a%20personal%20access,the%20Generate%20New%20Token%20button.

    - Azure CLI https://docs.microsoft.com/en-us/cli/azure/install-azure-cli


## Usage
 
Create

`ansible-playbook deploy.yml --tags phish`

Destroy

`ansible-playbook destroy.yml --tags phish`

Secrets

You have three choices

1. Hard code (Don't do this)
2. Use a Secrets CLI https://docs.ansible.com/ansible/latest/collections/community/general/lastpass_lookup.html
3. Use Ansible Vaults https://docs.ansible.com/ansible/latest/user_guide/vault.html

### Evilginx2

If you would like to modify the phishlet or change lures, please edit the following files.

`roles\evilginx2-docker\templates\config.yaml.j2`

`roles\evilginx2-docker\templates\o365.yaml.j2`

You can check the evilginx logs for session data with the following command.

`docker logs evilginx2`

### Gophish

You can access gophish via the hostname set for "gophish_admin_hostname"

To get the password on first login check the docker logs

`docker logs gophish`

## Development

Does none of this work for you? Submit a issue and I will see what the problem is.

Want to add a cool new feature shoot me that sweet pull request.


## Acknowledgements

Gophish https://getgophish.com/

Evilginx https://github.com/kgretzky/evilginx2

Ansible roles from https://github.com/geerlingguy


## License

MIT.
