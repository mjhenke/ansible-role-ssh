# -*- mode: ruby -*-
# vi: set ft=ruby :

# This guide is optimized for Vagrant 1.9 and above.
Vagrant.require_version ">= 1.9"

role = File.basename(File.expand_path(File.dirname(__FILE__)))

boxes = [
  {
    :name => "ubuntu-1404",
    :box => "ubuntu/trusty64",
    :ip => '10.0.1.11',
    :cpu => "50",
    :ram => "256"
  }
]
#  },
#  {
#    :name => "ubuntu-1604",
#    :box => "ubuntu/xenial64",
#    :ip => '10.0.1.12',
#    :cpu => "50",
#    :ram => "256"
#  }
#]

Vagrant.configure("2") do |config|
  boxes.each do |box|
    config.vm.define box[:name] do |instance|
      instance.vm.box = box[:box]
      instance.vm.hostname = "ansible-#{role}-#{box[:name]}"

      instance.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--cpuexecutioncap", box[:cpu]]
        vb.customize ["modifyvm", :id, "--memory", box[:ram]]
      end

      instance.vm.network :private_network, ip: box[:ip]

      instance.vm.provision :ansible do |ansible|
        # ansible.playbook = "tests/python.yml"
        ansible.playbook = "tests/main.yml"
        ansible.extra_vars = { ansible_user: 'vagrant' }
        ansible.verbose = "vv"
      end
    end
  end
end
