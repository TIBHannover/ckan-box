# coding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

# Configuration variables.
VAGRANTFILE_API_VERSION = "2"

#### Name and domain ####
DOMAIN  = 'ckan'
name = 'ckan-box'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = true

    config.vm.define name do |machine|

      machine.vm.box = 'debian/buster64'
      machine.vm.box_version = "10.4.0"

      ##### #####

      ## Define the hardware  #####
      machine.vm.provider "virtualbox" do |vbox|
        vbox.gui    = true
        vbox.cpus   = 2
        vbox.memory = 2048
        vbox.name   = name
      end

      ######

      ### Network configuration ###
      machine.vm.hostname = name + DOMAIN
      machine.vm.network "private_network",  ip: "192.168.10.55"
      ####

      machine.vm.provision "shell", inline: "sudo timedatectl set-timezone Europe/Amsterdam", run: "always"

      ## Ansible Provision ###
      machine.vm.provision "ansible_local" do |ansible|
          ansible.playbook = "playbook-ckan.yml"
          ansible.install_mode = "pip3"
          ansible.verbose = "vvv"
        end

    end


end
