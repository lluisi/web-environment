# Web environment

This Vagrant profile installs Php, Nginx, MySQL and others, using the Ansible provisioner.

The roles install these software in the guest machine:
* php 7.0 => [geerlingguy/ansible-role-php](https://github.com/geerlingguy/ansible-role-php)
* nginx 1.10 => [jdauphant/ansible-role-nginx](https://github.com/jdauphant/ansible-role-nginx)
* mysql 5.7 => [geerlingguy/ansible-role-mysql](https://github.com/geerlingguy/ansible-role-mysql)
* xdebug => [geerlingguy/ansible-role-php-xdebug](https://github.com/geerlingguy/ansible-role-php-xdebug)
* ssl-cert => [jdauphant/ansible-role-ssl-certs](https://github.com/jdauphant/ansible-role-ssl-certs)
* composer => [geerlingguy/ansible-role-composer](https://github.com/geerlingguy/ansible-role-composer)
* redis => [DavidWittman/ansible-redis](https://github.com/DavidWittman/ansible-redis)
* nodejs => [geerlingguy/ansible-role-nodejs](https://github.com/geerlingguy/ansible-role-nodejs)


### Requirements

* [VirtualBox](https://www.virtualbox.org)
* [Vagrant](https://www.vagrantup.com) 1.9 or later
* [Vagrant Host Manager plugin](https://github.com/devopsgroup-io/vagrant-hostmanager)

> Ansible is installed into guest machine, it is not required into your host


## How to use it

Clone the repo:

```
git clone https://github.com/lluisi/web-environment.git && cd web-environment
```

## Configuration

> Rename and configure sample files into *provision/config/*

### vm_config.yml

```
provision/config/sample/vm_config_sample.yml
```
Configure your VM as your needs:

```
box:
    name: your-box
    url: http://the-url-of-your-box
vm:
    name: web-environment
    hostname: web.env
    memory: 1024
    cpus: 1
    network:
        private_network: 192.168.57.101
```

### host_aliases.yml


```
provision/config/sample/host_aliases_sample.yml
```
Define as many hosts as you need for your own development projects:

```
- my-project-a.local
- my-project-b.local
```

### host_synced_folder.yml

```
provision/config/sample/synced_folder_sample.yml
```
Sync your local folders with your VM:

```
my-project-a:
    type: nfs
    source: ../my-project-a
    target: /var/www/my-project-a

my-project-b:
    type: nfs
    source: ../my-project-b
    target: /var/www/my-project-b
```

### Variables


```
provision/config/sample/vars/php_sample.yml
provision/config/sample/vars/nginx_sample.yml
provision/config/sample/vars/mysql_sample.yml
provision/config/sample/vars/xdebug_sample.yml
provision/config/sample/vars/ssl_sample.yml
```


And finally:
```
vagrant up
```