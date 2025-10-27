---
date: '2025-07-30T21:22:33-04:00'
draft: false
title: 'Vagrant'
tags:
  - Virtualization
categories:
  - blog
---
# First setup your vagrant file

To begin, you'll need to configure your Vagrantfile. You can refer to the official [vagrant documentation](https://developer.hashicorp.com/vagrant/docs/boxes)

First, install Vagrant and VirtualBox using the following commands:

```sh
sudo apt install vagrant
sudo apt install virtualbox
```

Vagrant is a powerful tool that allows you to manage and run virtual machines (VMs) using your preferred virtualization software. It provides a consistent and efficient way to work with VMs, regardless of the underlying virtualization technology.
![explication](/images/posts/vagrant/explication.png)

## How to use vagrant

You need to create a VagrantFile here is an example

```sh title="VagrantFile"
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_version = "20191107.0.0"
end
```

## Example complex config

```sh
Vagrant.configure("2") do |config|
  (1..2).each do |i|
    config.vm.define "master#{i}" do |master|
      master.vm.box = "almalinux/9"
      master.vm.network "private_network", ip: "192.168.10.1#{i}"
      # master.ssh.host = "192.168.10.1#{i}"
      master.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
      master.vm.provider "virtualbox" do |v|
        v.memory = 4096
        v.cpus = 2
      end
    end
  end
end
```
