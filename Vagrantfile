# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "opscode-ubuntu-14.04"
  # config.vm.box_check_update = false
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true

    # Customize the amount of memory on the VM:
    vb.memory = "2048"
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo sh -c "echo 'set grub-pc/install_devices /dev/sda' | debconf-communicate"
    sudo apt-get update
    sudo apt-get upgrade -y
    sudo apt-get install -y git wget build-essential linux-headers-server
    sudo apt-get install -y linux-headers-$(uname -r)
    sudo apt-get install -y language-pack-ja
    sudo update-locale LANG=ja_JP.UTF-8
    sudo apt-get install -y xubuntu-desktop
    sudo sh -c "echo '[SeatDefaults]' > /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf"
    sudo sh -c "echo 'user-session=ubuntu' >> /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf"
    sudo sh -c "echo 'allow-guest=false' >> /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf"
    sudo sed -i 's/XKBLAYOUT="us"/XKBLAYOUT="jp"/' /etc/default/keyboard
    sudo sed -i 's/XKBOPTIONS=""/XKBOPTIONS="lv3:ralt_switch"/' /etc/default/keyboard
    sudo loadkeys jp
    sudo sh -c "echo 'Asia/Tokyo' > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata"
    sudo wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb -O google-chrome-stable_current_amd64.deb
    sudo apt-get install -y libappindicator1 libindicator7
    sudo dpkg -i google-chrome-stable_current_amd64.deb
  SHELL

  # vbox addition
  config.vbguest.auto_update = true
  config.vbguest.no_remote = false
end
