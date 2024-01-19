# -*- mode: ruby -*-
# vi: set ft=ruby :

box = "centos/7"

if Vagrant::VERSION == '1.8.5'
  ui = Vagrant::UI::Colored.new
  ui.error 'Unsupported Vagrant Version: 1.8.5'
  ui.error 'Version 1.8.5 introduced an SSH key permissions bug, please upgrade to version 1.8.6+'
  ui.error ''
end

Vagrant.configure("2") do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.boot_timeout = 999999
  config.ssh.insert_key = false
  config.vm.box_check_update = false
  config.vm.provider :libvirt do |libvirt|
  # Don't forget to create your storage pool
    libvirt.storage_pool_name="test-libvirt"
    libvirt.driver="kvm"
    libvirt.uri="qemu:///system"
  end
  config.vm.define :test_machine do |node|
    node.vm.box = box
    node.vm.network :private_network, ip: "10.10.10.11"
    node.vm.network :forwarded_port, guest: 22, host: 24011, auto_correct: true
    node.vm.provider "libvirt" do |d|
      d.memory = 1024
      d.graphics_type = "none"
      d.cpus = 1
    end
  end
end
