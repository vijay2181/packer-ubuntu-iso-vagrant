# packer-ubuntu-iso-vagrant

## How to use Packer to create Ubuntu 18.04 Vagrant boxes

```
- i have windows 10 os, install below tools with versions

D:\PACKER\UBUNTU-PACKER>vagrant --version
Vagrant 2.2.16

D:\PACKER\UBUNTU-PACKER>packer --version
1.7.7

virtual box version: 6.1.22
```

```
goto this folder and do cmd

D:\PACKER\UBUNTU-PACKER

```

execute
```
packer build build.json
```

- in the vm gui you will get below promt, click on ok

![image](https://github.com/vijay2181/packer-ubuntu-iso-vagrant/assets/66196388/85e2a5f1-a9e0-4823-b9ba-59544f41cb0f)

click on continue

![image](https://github.com/vijay2181/packer-ubuntu-iso-vagrant/assets/66196388/60bc3de2-79c4-4b85-a004-48dc45b790c7)


- after installing scripts, shut down the machine, then post processors will be excuted and vagrant box image will be output to output/ubuntu-20.04.box

execute nelow command to to add box to vagrant 

```
D:\PACKER\UBUNTU-PACKER>vagrant box add --name ubuntu20.04 file:///D:/PACKER/UBUNTU-PACKER/output/ubuntu-20.04.box
```

Finally, in any other directory, we can create a Vagrantfile:

```
$ cat > Vagrantfile << 'EOF'
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu20.04"
  config.ssh.password = "vagrant"

  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
  end
end

EOF
```

```
$ vagrant up && vagrant ssh
```
