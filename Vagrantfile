# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.define "nebulahost" do |nebulahost|
    nebulahost.vm.network "forwarded_port", guest: 2633, host: 2633, auto_correct: true
  end

  config.vm.define "dockerhost" do |dockerhost|
    dockerhost.vm.network "forwarded_port", guest: 9869, host: 9869, auto_correct: true
    dockerhost.vm.network "forwarded_port", guest: 2474, host: 2474, auto_correct: true
  end

  config.ssh.insert_key = false
  config.ssh.private_key_path = ["~/.ssh/id_rsa", "~/.vagrant.d/insecure_private_key"]
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"

  #config.vm.network "public_network",  bridge: "en0: Wi-Fi (AirPort)"
  config.vm.network "private_network", type: "dhcp", virtualbox__intnet: true

  config.vm.provision :ansible do |ansible|
    ansible.verbose = true
    ansible.playbook = "playbook.yml"
  end
end
