# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "chef/ubuntu-13.10"

  config.vm.network "private_network", ip: "192.168.111.10"
  
  config.vm.network "forwarded_port", guest: 9200, host: 9200
  config.vm.network "forwarded_port", guest: 80, host: 80

  config.vm.synced_folder '.', '/vagrant'
  
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end
end
