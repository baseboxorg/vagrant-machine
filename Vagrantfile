# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "boxcutter/ubuntu1604"

  # Filesystem configuration. Share the current folder as "/vagrant" on the guest VM
  # config.vm.synced_folder "./", "/vagrant"
  config.nfs.map_uid = 501
  config.nfs.map_gid = 20

  config.vm.synced_folder "./", "/vagrant", type: 'nfs'
  config.vm.synced_folder "/Users/voomac/Workspace", "/home/vagrant/workspace", type: 'nfs'

  config.ssh.forward_agent = true

  config.vm.define "base-node" do |base|
    config.vm.network :private_network, ip: '33.33.66.66'
    base.hostmanager.enabled = true
    base.hostmanager.manage_host = true
    base.hostmanager.manage_guest = true
    base.hostmanager.ignore_private_ip = false
    base.hostmanager.include_offline = true
    base.vm.network :forwarded_port, guest: 3000, host:3000
    base.hostmanager.aliases = %w(base.localdomain base.node)
    
    base.vm.host_name = "base.node"

    base.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.verbose = 'vvv'
    end
  end
end
