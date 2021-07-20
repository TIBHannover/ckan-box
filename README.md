# Ckan Box

Configuration of the Ckan Box via ansible.

Documentation see also
* https://docs.ckan.org/en/2.9/

## Installation on local system for testing

Prerequisites
* [Git](https://git-scm.com/downloads)
* [Vagrant](https://www.vagrantup.com/downloads.html)
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

Perform the following steps in the terminal (Linux / macOS) or in the GitBash (Windows).
```
git clone https://github.com/TIBHannover/ckan-box.git
cd 
vagrant up
```
At the first start the script aborts with an error message, because vagrant is not able to reset the ssh connection. Then simply run ansible again with
```
vagrant reload --provision
```

When the installation is complete (a few minutes, depending on the download speed), the index can be opened in the browser:
http://192.168.10.55


## Direct usage of Ansible
Use playbook_frontend.yml for frontend server installation, playbook_backend.yml for standalone backend server installation and playbook.yml for cloned server installation.

* Frontend installation further requires specifying the installation directory, inventory file for root privileges on that directory and backend mongodb_ip.
* It is also possible to customize branding variables, docker compose and docker files from group_vars.
* It is assumed that the same user name will be used both on frontend and backend machines. 
* A proper /etc/exports file should be provided as backend_exports_file including the lines below. The lines should be modified according to network:


/home/user/ts-neo4j-data  X.X.X.X(rw,sync,no_root_squash,no_subtree_check)
/home/user/ts-downloads  X.X.X.X(rw,sync,no_root_squash,no_subtree_check)

