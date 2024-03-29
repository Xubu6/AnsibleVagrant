# -*- mode: ruby -*-
# vi: set ft=ruby :

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
  # config.vm.box = "base"
  config.vm.box = "ubuntu/focal64"   # Ubuntu 18.04 (use focal64 for 20.04)
   
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
     vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "2048"
  end
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
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL

  # Note, the actions when performed inside an inline shell are by default
  # executed as root user unless you provide the privileged: false option
  #
  # So if I do the following, the directories will be owned by root and
  # we don't want that. So we could pass a privileged: false option after
  # the ending SHELL. But I am showing a different way to do it by
  # defining a separate shell script that gets called. See below.
  #config.vm.provision "shell", inline: <<-SHELL
  #    mkdir -p /home/vagrant/.ssh
  #    mkdir -p /home/vagrant/.ansible
  #    mkdir -p /home/vagrant/.config
  #    mkdir -p /home/vagrant/.config/openstack
  #SHELL

  # The shell provisioner can also accept a script that will be executed in
  # the guest in user mode (by default). See the bootstrap.sh script
  # where we create the above directories and they all will execute
  # as the user "vagrant" by default 
  config.vm.provision "shell", path: "bootstrap.sh"

  # let's copy our pem file to the vagrant created guest. Change the file name
  # as appropriate in your case and also the file path based on where on your
  # host you have stored this file.
  #
  # Note that I am on Windows m/c and so have used the Windows path to
  # the source. I created an equivalent directory structure on my Windows
  # file system as Linux with .ssh, etc directories.
  config.vm.provision "file", source: "~/.ssh/team16.pem", destination: "~/.ssh/team16.pem"
  config.vm.provision "file", source: "./.ansible.cfg", destination: "~/.ansible.cfg"
  config.vm.provision "file", source: "./MyInventory", destination: "~/.ansible/MyInventory"
  config.vm.provision "file", source: "./clouds.yaml", destination: "~/.config/openstack/clouds.yaml"
  config.vm.provision "file", source: "./consumer.py", destination: "~/consumer.py"
  config.vm.provision "file", source: "./server.properties", destination: "~/server.properties"

  
  # make sure the permissions on the  pem file are not too open.
  # Note, here I show you using inline and privileged: false so the inline
  # action actually happens as the user vagrant.
  # Moreover, we also show a diff approach to put the inline code in
  # a block, and then use the block name. 
  # Change file name as appropriate. Replace this with your pem file.
  $script = <<-SCRIPT
     chmod go-rwx ~/.ssh/team16.pem
  SCRIPT
  config.vm.provision "shell", inline: $script, privileged: false

  # We now use the Ansible provisioner
  #
  # in the following, install= true will install ansible in the
  # created or provisioned guest vm. Once ansible is installed, any
  # additional configuration we plan to do will be taken from the
  # supplied playbook. Moreover, we can also tell ansible which
  # Inventory file it should use. This inventory file will appear in the
  # /vagrant directory (which is the same directory on your host that has
  # the vagrantfile but is mounted as /vagrant in the guest machine)
  #
  # Please note that the get facts about cloud will fail because we haven't
  # installed openstacksdk and ansible galaxy plugin. All those steps
  # are left for you to fill up
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook_master.yml"
    ansible.verbose = true
    ansible.install = true  # installs ansible (and hence python on VM)
    ansible.limit = "all"
    ansible.inventory_path = "MyInventory"  # inventory file
  end
end
