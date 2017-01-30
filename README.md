# Web environment

This Vagrant profile installs Php, Nginx, MySQL and others, using the Ansible provisioner.

The roles install these software in the guest machine:
* php 7.0
* nginx 1.10
* mysql 5.7
* xdebug
* ssl-cert
* composer

## Box

The box proposed is a [bento/ubuntu-16.04](https://github.com/chef/bento), you can use any box defining it in [vm_config.yml](config/sample/vm_config_sample.yml).

```
name: bento/ubuntu-16.04
```
The URL that the configured box can be found at:
```
url: http://of-your-box
```

### Requirements

* [VirtualBox](https://www.virtualbox.org)
* [Vagrant](https://www.vagrantup.com) 1.9 or later
* [Vagrant Host Manager plugin](https://github.com/devopsgroup-io/vagrant-hostmanager)

> Ansible is installed into guest machine, it is not required into your host


## How to use it

This repo uses other repositories as a git submodules, so to properly clone do the following:

```
git clone --recursive https://github.com/lluisi/web-environment.git && cd web-environment
```

Rename and configure the following sample files as your needs:


```
config/sample/vm_config_sample.yml
config/sample/host_aliases_sample.yml
config/sample/synced_folder_sample.yml
```

```
config/sample/vars/php_sample.yml
config/sample/vars/nginx_sample.yml
config/sample/vars/mysql_sample.yml
config/sample/vars/xdebug_sample.yml
config/sample/vars/ssl_sample.yml
```

into *config/*

And finally:
```
vagrant up
```