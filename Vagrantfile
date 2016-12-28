# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "bento/ubuntu-16.04"
  # config.vm.box = "bento/centos-7.2"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = false


  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip:"172.28.128.159"
  #, auto_config: false
  # config.vm.network "private_network", type: "dhcp"

  config.vm.hostname = "kube-cluster-master"

  config.vm.provider "virtualbox" do |vb|
    config.ssh.insert_key = true
    config.ssh.username = "vagrant"
    config.ssh.password = "vagrant"
    # Customize the amount of memory on the VM:
    vb.cpus = "4"
    vb.memory = "4096"

    # https://github.com/chef/bento/issues/688
    vb.customize ["modifyvm", :id, "--cableconnected1", "on"]

    config.vbguest.auto_update = false
  end

  config.vm.provision "ansible" do |ansible|
        ansible.limit = "all"
        ansible.sudo = true
        ansible.playbook = "./playbooks/deploy-cluster.yml"
        ansible.raw_arguments = "-v"
        ansible.inventory_path = "./inventories/vagrant.ini"
  end

  #SHELL
end
