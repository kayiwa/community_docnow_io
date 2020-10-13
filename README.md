# community_docnow_io

**Community Docnow Installer** is the ansible installer for [community.docnow.io](community.docnow.io) but can be used to install the [DocNow Appraisal Application](https://github.com/docnow/docnow) with a few modifications. This repository assumes a remote UNIX like OS host. We are using the [Google Cloud Platform](https://cloud.google.com) Virtual Machine in this repository. 

* [System requirements](#system-requirements)
* [Installing](#installing)

## Controller System Requirements

* Ansible (check for version on [Pipfile](Pipfile))
* Python  (check for verion on [.tool-versions](.tool-versions))

## Remote System Requirements

* Unix-like OS (**Windows isn't fully supported**);
* Node 12.*
* Web-server (Passenger (tested heavily on) Nginx);
* Database (PostgreSQL);
* Key/Value Store (Redis);


## Installing

* On your Ansible Controller System make sure you've installed [Ansible](https://ansible.com)

* Clone this repository :wink: and `cd` into the cloned repository

* Copy [group_vars/gcp/prod.yml.example](group_vars/gcp/prod.yml.example) to `group_vars/gcp/prod.yml`

	* if you look at [.gitignore](.gitignore) you will note the the new `group_vars/gcp/prod.yml` file will not be committed

	* if you will be using a [bastion host](https://www.wikiwand.com/en/Bastion_host) -we recommend this- to connect to your virtual machine

	* if you do not intend to use a bastion host you can ignore this step


* Copy [hosts.example](hosts.example) to a new file `hosts` with `cp hosts.example hosts`

	* if you look at [.gitignore](.gitignore) you will note the the new `hosts` file will not be committed

	* edit the file with the IP address of your Virtual Machine. 


* Install docnow with the following by running the step below two times: 

```bash
ansible-playbook -i hosts playbook/community_docnow.yml
```

* Yes that's right. There is a known bug where the first time this runs it will error out during the `""install modules""` task. If you run it a second time the step will not error out. Upon completion go to the IP address you entered in your `hosts` file. 