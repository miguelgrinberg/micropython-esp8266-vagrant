# micropython-esp8266-vagrant

This project contains tools to simplify the building of the MicroPython
firmware for the ESP8266 microcontroller.

## Vagrant VM

The build environment is installed in a Vagrant VM. To be able to do this,
you need to install [Vagrant](https://www.vagrantup.com/) and 
[VirtualBox](https://www.virtualbox.org/wiki/Downloads).

To create the VM, simply run:

    $ vagrant up

This command will create an Ubuntu VM, download and build the ESP8266
cross-compiler, and finally download and build MicroPython. This takes a long
time. Just as a reference, the process takes about 20 minutes on a relatively
modern Mac laptop.

When the command completes, you will find a *micropython* directory, which
thanks to Vagrant is also accessible inside the VM as */vagrant/micropython*.
The firmware for the ESP8266 is stored in *micropython/ports/esp8266/build*.

To stop the VM without destroying it, enter:

    $ vagrant halt

And then to restart it:

    $ vagrant up

Note that on a restart, this command is fairly fast. You will need to also
issue it if you restart your system without having properly halted the VM.

If you want to completely delete the VM, run:

    $ vagrant destroy

Normally there is no need to do this, but if you need to log in to the VM,
the command is:

    $ vagrant ssh

## Installing Packages from PyPI

The main reason why it is usually necessary to build a custom firmware is to
install custom dependencies that are too big to be installed as source code
directly on a device running a stock firmware.

To add a custom package to the firmware, run the following command:

    $ ./upip install <package> ...

Note that only packages specifically written for MicroPython can be installed.
The packages will be installed to the *micropython/ports/esp8266/modules*
directory, which is pre-compiled and added to the firmware. After adding new
packages, the firmware needs to be rebuilt.

## Building the Firmware

If you need to build the firmware (typically after adding or removing custom
packages), issue the following command:

    $ ./build

## Cloning MicroPython

If you want to start from scratch, you can delete the *micropython* directory
and then clone it again with the command:

    $ ./clone

This will get a fresh copy of the MicroPython repository and its dependencies,
and leave it ready for the firmware to be built.
