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
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "generic/debian11"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

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
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    # Setting up repos
    apt-get update
    apt-get upgrade
    apt-get install -y gpg
    wget -q -O - https://archive.kali.org/archive-key.asc | apt-key add
    echo "deb http://http.kali.org/kali kali-rolling main non-free contrib" >> /etc/apt/sources.list
    apt-get update

    # Installing packages
    apt-get install -y neovim gdb git python3-pip feh ripgrep strace python3-venv htop libgmp3-dev libmpc-dev
    pip install ropper ropgadget pwntools tqdm

    # radare2
    sudo -u vagrant git clone https://github.com/radareorg/radare2 /home/vagrant/radare2 --depth 1
    sudo -u vagrant /home/vagrant/radare2/sys/install.sh
    sudo -u vagrant r2pm init
    sudo -u vagrant r2pm -ci install r2ghidra

    # pwndbg
    git clone https://github.com/pwndbg/pwndbg /opt/pwndbg
    pushd /opt/pwndbg
    sudo -u vagrant ./setup.sh
    popd

    # Rsactftool
    git clone https://github.com/Ganapati/RsaCtfTool /opt/RsaCtfTool
    pip install -r /opt/RsaCtfTool/requirements.txt

    # Heavy packages
    apt-get install -y ghidra openjdk-11-jre
    apt-get install -y xfce4 xfce4-goodies thunar-archive-plugin dbus-x11 qt5dxcb-plugin

    # The angr directory
    sudo -u vagrant mkdir /home/vagrant/angr
    pushd /home/vagrant/angr
    sudo -u vagrant python3 -m venv .venv
    sudo -u vagrant bash -c 'source .venv/bin/activate && pip install angr-management'
    popd

    # Nix
    sudo -u vagrant bash -c "curl -L https://nixos.org/nix/install | sh"

    echo "export TERM=xterm-256color" >> /home/vagrant/.bashrc
  SHELL
end
