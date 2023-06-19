# LAMP on Ubuntu

This playbook will install a LAMP environment (**L**inux, **A**pache, **M**ySQL and **P**HP) on an Ubuntu machine. A virtualhost will be created with the options specified in the `vars/default.yml` variable file.

## Settings

- `mysql_root_password`: the password for the MySQL root account.
- `app_user`: a remote non-root user on the Ansible host that will own the application files.
- `http_host`: your domain name.
- `http_conf`: the name of the configuration file that will be created within Apache.
- `http_port`: HTTP port, default is 80.
- `disable_default`: whether or not to disable the default Apache website. When set to true, your new virtualhost should be used as default website. Default is true.


## Running this Playbook

### Setup Ansible (if not already installed)
Reference: 
https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-18-04
https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-1804

# Install Ansible
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible

# Configure Ansible - Setup the inventory file
sudo nano /etc/ansible/hosts

    [servers]
    server1 ansible_host=127.0.0.1

    [all:vars]
    ansible_python_interpreter=/usr/bin/python3

# Verify
ansible-inventory --list -y

Quickstart guide for those already familiar with Ansible:

### 1. Obtain the playbook
```shell
git clone https://github.com/mabdevx/ansible-playbooks.git
cd ansible-playbooks/lamp_ubuntu
```

### 2. Customize Options

```shell
nano vars/default.yml
```

```yml
---
mysql_root_password: "mysql_root_password"
app_user: "your_app_user"
http_host: "your_domain"
http_conf: "your_domain.conf"
http_port: "80"
disable_default: true
```

### 3. Run the Playbook

```command
ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yml
```


# Original Source

https://github.com/do-community/ansible-playbooks