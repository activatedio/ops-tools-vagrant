# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  VAGRANT_COMMAND = ARGV[0]
  if VAGRANT_COMMAND == "ssh"

    is_windows = (ENV['OS'] == 'Windows_NT')
    username = ENV[is_windows ? 'USERNAME' : 'USER' ]
    config.ssh.username = username

  end

  config.vm.box = "geerlingguy/ubuntu1604"

  config.vm.provider :virtualbox do |v|
    v.name = "opstools"
    v.memory = 2048
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.hostname = "opstools"
  config.vm.network :private_network, ip: "34.33.33.10"

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :opstools do |opstools|
  end

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.inventory_path = "provisioning/inventory"
    ansible.sudo = true
  end

end
