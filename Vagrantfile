# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.hostname = "smart-on-fhir"
  config.vm.box = "bento/ubuntu-16.04"

# Gateway
  config.vm.network :forwarded_port, guest: 9070, host: 9070
# Sandbox Manager
  config.vm.network :forwarded_port, guest: 9075, host: 9075
# API Server
  config.vm.network :forwarded_port, guest: 9080, host: 9080
# Persona-API Server
  config.vm.network :forwarded_port, guest: 9081, host: 9081
# Auth Server
  config.vm.network :forwarded_port, guest: 9085, host: 9085
# Persona-Auth Server
  config.vm.network :forwarded_port, guest: 9086, host: 9086
# Messaging Server
  config.vm.network :forwarded_port, guest: 9087, host: 9087
# PWM Server
  config.vm.network :forwarded_port, guest: 9088, host: 9088
# Apps Server
  config.vm.network :forwarded_port, guest: 9090, host: 9090
# LDAP
  config.vm.network :forwarded_port, guest: 389, host: 1389
# PWM Server
  config.vm.network :forwarded_port, guest: 9095, host: 9095

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "5120"
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    vb.customize ["modifyvm", :id, "--cableconnected1", "on"]
  end

  config.vm.provision "fix-no-tty", type: "shell" do |s|
    s.privileged = false
    s.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
  end

  config.vm.provision "ansible" do |ansible|
#    ansible.verbose="vvvv"
#    ansible.tags=["smart-platform"]
#    ansible.tags=["api-dstu2-all"]
    ansible.tags=["sandbox-manager-all"]
#    ansible.playbook = "provisioning/site.yml"
    ansible.playbook = "provisioning/playbook-rebuild-databases.yml"
#    ansible.playbook = "provisioning/playbook-rebuild-app-code.yml"
  end

  # If you are running the build on a Windows host, please comment out the
  # "ansible" provisioner above and use this "shell" provisioner:
  #
  # config.vm.provision "shell", path: "provisioning/provision-on-guest.sh"

end
