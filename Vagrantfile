# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2004"
  config.vm.provider "hyperv"
  # config.vm.box_check_update = false
  config.vm.synced_folder ".", "/vagrant" # NOTE: On Hyper-V this will create an SMB share and require the user's credentials.
  config.vm.boot_timeout = 600

  config.vm.provider "hyperv" do |hv|
    hv.vmname = "ansible-control-node"
    hv.cpus = 2
    hv.memory = 2048
    hv.linked_clone = true
  end

  # basic box/machine normalization
  config.vm.provision "normalize", type: "ansible_local" do |ansible|
    ansible.playbook = "provision/normalize.yml"
  end
  # ansible installation + tweaks
  config.vm.provision "ansible", type: "ansible_local" do |ansible|
    ansible.playbook = "provision/ansible.yml"
  end
end
