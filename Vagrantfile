# -*- mode: ruby -*-
# vi: set ft=ruby :

# Environmental variables
PROXY = "10.144.1.10"
PROXY_PORT = "8080"

# Checking required vagrant plugins
required_plugins =%w( vagrant-proxyconf vagrant-vbguest )

plugin_installed = false
required_plugins.each do |plugin|
  if !Vagrant.has_plugin?(plugin)
    system("vagrant plugin install #{plugin}")
    plugin_installed = true
  end
end
if plugin_installed
  puts "Plugins has been installed, run 'vagrant up' again."
  exit
end

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "bento/ubuntu-16.04"
  # config.vm.box = "bento/centos-7.2"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip:"172.28.128.159"#, auto_config: false
  # config.vm.network "private_network", type: "dhcp"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder ".", "/home/vagrant/mentat"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox"
  config.vm.provider "virtualbox" do |vb|
    config.ssh.username = "vagrant"
    config.ssh.password = "vagrant"
    # Display the VirtualBox GUI when booting the machine
    #vb.gui = true
    #   # Customize the amount of memory on the VM:
    vb.cpus = "4"
    vb.memory = "4096"

    # https://github.com/chef/bento/issues/688
    vb.customize ["modifyvm", :id, "--cableconnected1", "on"]

    config.proxy.http     = "http://#{PROXY}:#{PROXY_PORT}/"
    config.proxy.https    = "https://#{PROXY}:#{PROXY_PORT}/"
    config.proxy.no_proxy = "172.28.128.159,localhost,127.0.0.0/8,10.0.2.15/24,172.17.0.1/16,*.local,127.0.0.1,10.32.0.0/12,10.244.0.0/16"

    config.vbguest.auto_update = false
  end
  # config.vm.provision "shell", path: "installDocker.sh", privileged: false
  config.vm.hostname = 'KubesTest'

  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  #config.vm.provision "shell", inline: <<-SHELL

  #SHELL
end
