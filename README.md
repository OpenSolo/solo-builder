# solo-builder

**WARNING - WORK IN PROGRESS**

**This code is a work in progress and may be full of bugs still. DO NOT use this unless you want to experiment and troubleshoot.**

## Quick start guide
You may find the following "quick start" guide useful.  You can find the [Open Solo Quick Start Guide](http://ardupilot.org/dev/docs/solo-opensolo-quickstart.html) on ardupilot.org.

## Using vagrant in Windows

This method will uses [vagrant](https://www.vagrantup.com/downloads.html) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads) to create a pre-configured virtual machine.  This VM becomes the build environment, and is managed/executed via the Windows command line.

#### Initiate Build
1. Open an elevated Windows command prompt (run command prompt as administrator) and go to the solo-builder repository.
Example: `>cd /github/solo-builder`

2. If this is the initial setup of the VM, install the Vagrant Guest Ansible Plugin: `>vagrant plugin install vagrant-guest_ansible`

3. Start the Vagrant virtual machine with `>vagrant up`. The first time you start the Vagrant VM, it will go through a lengthy initial setup. If `>vagrant up` fails, run `>vagrant provision` to try provisioning your VM again.

4. Once the Vagrant VM is up, you can start the build with all default settings with `>vagrant ssh -c "/vagrant/builder.sh"`


#### Build Options
You can run the build with any of these options using this syntax.

`>vagrant ssh -c "/vagrant/builder.sh -a [github acccount] -[repository name] -b [branch name]"`
* **-a** to redirect to a different github account. If not specified, it will use the OpenSolo github account.
* **-r** to redirect to a different repository. If not specified, it will use 3dr-arm-yocto-bsp.
* **-b** to redirect to a different branch. If not specified, it will use master.
* **EXAMPLE:** `> vagrant ssh -c "/vagrant/builder.sh -a Pedals2Paddles  -b v0.1.0"` will use Matt's GitHub account, the default repo name (3dr-arm-yocto-bsp) since the -r option wasn't specified, and the branch called v0.1.0

#### Completed files
When the build completes, the script will copy the relevant files to a date/time stamped directory in your github solo-builder directory. This allows you to access them easily from within Windows.
* 3dr-solo.tar.gz and solo.md5
* 3dr-controller.tar.gz and controller.md5


#### Notes:
* The first time you run this build, or if you've changed repositories, it will stop during beginning of the configuration and prompt you to restart the build. This is normal as some components needed to be exported first. If you are promoted to run the build again, do it (`vagrant ssh -c "/vagrant/builder.sh [options]"`). 
* The fist time you run the build or after changing repositories, it will take a very long time to complete. Anywhere from 2-6 hours. 


## Using docker

DOCKER IS UNTESTED OUTSIDE 3DR , USE VAGRANT FOR NOW.
 
Works in Docker and boot2docker. 
Copy `id_rsa` and `solo-builder.pem` to this directory (sorry). Then run

```
docker build -t 3drobotics/solo-builder .
```

Then run

```
docker run -i 3drobotics/solo-builder su -l ubuntu /solo-build/builder.sh
```

TODO: write a script that gets the files off after

## Using something else

`playbook.yml` is an ansible file for an Ubuntu 14.04 distro. `builder.sh` is the build script for a user named `ubuntu`. Make it happen!

## Repos

3dr Private:

* https://github.com/3drobotics/mavlink-solo
* https://github.com/3drobotics/sculpture_proprietary
* https://github.com/3drobotics/solo-gimbal
* https://github.com/3drobotics/artoo
* https://github.com/3drobotics/SoloLink

Public:

* https://github.com/3drobotics/imx6-uboot
* https://github.com/3drobotics/imx6-linux
* https://github.com/3drobotics/MAVProxy
* https://github.com/3drobotics/stm32loader
* https://github.com/3drobotics/ardupilot-solo

* https://github.com/OpenSolo/ardupilot-solo
* https://github.com/OpenSolo/sololink
* https://github.com/OpenSolo/artoo
* https://github.com/OpenSolo/imx6-uboot
* https://github.com/OpenSolo/imx6-linux
* https://github.com/OpenSolo/3dr-arm-yocto-bsp
* https://github.com/OpenSolo/meta-3dr
* https://github.com/OpenSolo/dronekit-python-solo
* https://github.com/OpenSolo/sololink-python
* https://github.com/OpenSolo/solo-builder
* https://github.com/OpenSolo/3dr-yocto-bsb-base
* https://github.com/OpenSolo/stm32loader
* https://github.com/OpenSolo/MAVProxy


