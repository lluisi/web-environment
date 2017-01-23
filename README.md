# Web environment

A vm provisioned with Ansible ready to be used

### Requirements

* [VirtualBox](https://www.virtualbox.org)
* [Vagrant](https://www.vagrantup.com) 1.9 or later
* [Vagrant Host Manager plugin](https://github.com/devopsgroup-io/vagrant-hostmanager)


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
```

And finally:
```
vagrant up
```