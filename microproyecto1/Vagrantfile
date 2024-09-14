# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  if Vagrant.has_plugin? "vagrant-vbguest"
    config.vbguest.no_install = true
    config.vbguest.auto_update = false
    config.vbguest.no_remote = true
  end

  #Recursos asignados a las maquinas
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 1
  end

  #Serv uno
  config.vm.define "servuno" do |node|
    node.vm.box = "bento/ubuntu-22.04"
    node.vm.hostname = "servuno"
    node.vm.network "private_network", ip: "192.168.100.2"
    node.vm.network :forwarded_port, guest: 22, host: 2202, id: 'ssh'
    node.vm.provision "ansible_local" do |ansible|
      ansible.install_mode = "default"
      ansible.playbook = "config/servuno/playbook.yml"
    end
  end
  #Serv dos 2
  config.vm.define "servdos" do |node|
    node.vm.box = "bento/ubuntu-22.04"
    node.vm.hostname = "servdos"
    node.vm.network "private_network", ip: "192.168.100.3"
    node.vm.network :forwarded_port, guest: 22, host: 2203, id: 'ssh'
    node.vm.provision "ansible_local" do |ansible|
      ansible.install_mode = "default"
      ansible.playbook = "config/servdos/playbook.yml"
    end
  end
  #Balanceador HAProxy
  config.vm.define "balanceador" do |node|
    node.vm.box = "bento/ubuntu-22.04"
    node.vm.hostname = "balanceador"
    node.vm.network "private_network", ip: "192.168.100.4"
    node.vm.network :forwarded_port, guest: 22, host: 2204, id: 'ssh'
    node.vm.provision "ansible_local" do |ansible|
      ansible.install_mode = "default"
      ansible.playbook = "config/balanceador/playbook.yml"
    end
  end
end
