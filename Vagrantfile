# -*- mode: ruby -*-
# vi: set ft=ruby :
#

$script = <<-SCRIPT
set -ex
sudo apt-get update -y
sudo apt-get install -y make unrar-free autoconf automake libtool gcc g++ gperf \
    flex bison texinfo gawk ncurses-dev libexpat-dev python-dev python python-serial \
    sed git unzip bash help2man wget bzip2 libtool-bin libffi-dev pkg-config
git clone --recursive https://github.com/pfalcon/esp-open-sdk.git
cd esp-open-sdk
git submodule update --init
make
cd ..
echo "export PATH=~/esp-open-sdk/xtensa-lx106-elf/bin/:/vagrant:\$PATH" >> ~/.profile
echo "export ESP_SDK=~/esp-open-sdk/xtensa-lx106-elf/xtensa-lx106-elf/sysroot/usr" >> ~/.profile
source ~/.profile
cd /vagrant
if [[ ! -d micropython ]]; then
    ./clone
fi
./build
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.provision "shell", inline: $script, privileged: false, keep_color: true
end
