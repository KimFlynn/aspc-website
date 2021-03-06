# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Make sure VirtualBox is provider
  ENV['VAGRANT_DEFAULT_PROVIDER'] = 'virtualbox'

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/trusty64"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network :forwarded_port, guest: 3000, host: 3000 # Rails developer server

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network :private_network, ip: "192.168.33.10" # commented because of startup hangs on Pomona wifi

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network :public_network # commented because of startup hangs on Pomona wifi

  # Install rvm and ruby
  config.vm.provision :shell, path: "vagrant/lib/install-rvm.sh", args: "stable", privileged: false
  config.vm.provision :shell, path: "vagrant/lib/install-ruby.sh", args: "2.6.3 bundler", privileged: false

  # Custom initialization - the meat and potatos
  config.vm.provision :shell, :path => "vagrant/init/init.sh"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  # config.vm.synced_folder ".", "/vagrant", :nfs => true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.

  config.vm.provider :virtualbox do |vb|
    vb.memory = 1024
  end

  # Use the default insecure private key for SSH (don't need security for this local box)
  config.ssh.insert_key = false
  config.ssh.private_key_path = '~/.vagrant.d/insecure_private_key'

  # Forward local SSH keys to Vagrant
  config.ssh.forward_agent = true

end
