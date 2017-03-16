# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.synced_folder ".", "/vagrant", type: "rsync",
    rsync__exclude: ".git/"
  config.vm.box = "ubuntu-16.04"
  config.vm.box_check_update = true

  %w(barbican).each do |node|
    config.vm.define node do |vmdef|
      vmdef.vm.box = "ubuntu-16.04"
      vmdef.vm.hostname = node
      vmdef.vm.provider "parallels" do |vm|
        vm.name = node
        vm.check_guest_tools = false
        vm.memory = 4096
        vm.cpus = 4
      end
    end
  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/site.yml"
  end
end
