# -*- mode: ruby -*-
# vi: set ft=ruby :

API_VERSION = "2"
VB_CPUS = "2"
VB_MEMORY = "1024"

Vagrant.configure(API_VERSION) do |config|

  config.vm.box = "centos7"
  config.vm.box_url = "https://f0fff3908f081cb6461b407be80daf97f07ac418.googledrive.com/host/0BwtuV7VyVTSkUG1PM3pCeDJ4dVE/centos7.box"

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  config.vm.define 'centos7' do |node|
    node.vm.hostname = 'vagrant-centos7'
    node.vm.network :private_network, ip: '10.1.1.10'
    node.hostmanager.aliases = [
      "vagrantbox.dev",
      "phpmyadmin.vagrantbox.dev"
    ]
  end

  config.vm.provision "ansible" do | ansible |
    ansible.sudo = true
    ansible.playbook = ".ansible/main.yml"
  end

#  config.vm.synced_folder ".", "/vagrant", :nfs => true

  config.vm.provider "virtualbox" do |v|
    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
#    v.memory = VB_MEMORY
#    v.cpus = VB_CPUS
  end  
end
