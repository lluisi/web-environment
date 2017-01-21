Vagrant.require_version ">= 1.9.0"

require 'yaml'
dir = File.dirname(File.expand_path(__FILE__))

if !File.file?("#{dir}/config/vm_config.yml")
  print "Please rename and configure #{dir}/config/sample/vm_config_sample.yml to #{dir}/config/vm_config.yml to continue\n"
  exit
end

if !File.file?("#{dir}/config/synced_folder.yml")
  print "Please rename and configure #{dir}/config/sample/synced_folder_sample.yml to #{dir}/config/synced_folder.yml to continue\n"
  exit
end

if !File.file?("#{dir}/config/host_aliases.yml")
  print "Please rename and configure #{dir}/config/sample/host_aliases_sample.yml to #{dir}/config/host_aliases.yml to continue\n"
  exit
end

vm_config = YAML.load_file("#{dir}/config/vm_config.yml")
synced_folder = YAML.load_file("#{dir}/config/synced_folder.yml")
host_aliases = YAML.load_file("#{dir}/config/host_aliases.yml")

Vagrant.configure(2) do |config|

  config.vm.box = "#{vm_config['box']['name']}"
  if !vm_config["box"]["url"].nil?
    config.vm.box_url = "#{vm_config['box']['url']}"
  end
  config.vm.define "#{vm_config['vm']['name']}"
  config.vm.network :private_network, ip: "#{vm_config['vm']['network']['private_network']}"
  config.vm.hostname = "#{vm_config['vm']['hostname']}"
  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  config.vm.provider :virtualbox do |v|
      v.name = "#{vm_config['vm']['name']}"
      v.memory = "#{vm_config['vm']['memory']}"
      v.cpus = "#{vm_config['vm']['cpus']}"
      v.customize [
          "modifyvm", :id,
          "--natdnshostresolver1", "on",
          "--cableconnected1", "on",
      ]
  end

  config.vm.provision :ansible_local do |ansible|
    ansible.install_mode = "pip"
    ansible.playbook = "playbook.yml"
    ansible.sudo = true
    ansible.verbose = false
    ansible.limit = 'all'
  end

  synced_folder.each do |i, folder|
    if folder['source'] != '' && folder['target'] != ''
      config.vm.synced_folder "#{folder['source']}", "#{folder['target']}", id: "#{i}", type: "#{folder['type']}"
    end
  end

  if Vagrant.has_plugin?('vagrant-hostmanager')
    hosts = Array.new()
    host_aliases.each do |host_alias|
      hosts.push(host_alias)
    end

    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.manage_guest = false
    config.hostmanager.ignore_private_ip = false
    config.hostmanager.include_offline = true
    config.hostmanager.aliases = hosts
  end

end