# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "boxcutter/ubuntu1604"

  # Filesystem configuration. Share the current folder as "/vagrant" on the guest VM
  # config.vm.synced_folder "./", "/vagrant"
  config.vm.synced_folder "./", "/vagrant", type: 'nfs'
  config.vm.synced_folder "/Users/voomac/Workspace", "/home/vagrant/workspace", type: 'nfs'

  config.ssh.forward_agent = true

  config.vm.define "base-node" do |base|


    base.vm.network :forwarded_port, guest: 3000, host:3000

    # this is needed for nfs to work
    config.vm.network "private_network", type: "dhcp"

    base.vm.host_name = "vagrant.machine"

    base.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.verbose = 'vvv'
    end
  end
end
