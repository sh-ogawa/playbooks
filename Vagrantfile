# -*- mode: ruby -*-
# vi: set ft=ruby :

require './vagrant/env.rb'
local = LocalEnv.new

Encoding.default_external = 'UTF-8'
box      = 'centos/7'
hostname = 'local7'
domain   = 'local7.test'
ip       = local.get 'ip',  '172.24.70.11'
ram      = local.get 'ram', '1024'
cpu      = local.get 'cpu', '1'

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = box
  config.vm.hostname = domain
  config.vm.network 'private_network', ip: ip

  config.vm.provider 'virtualbox' do |vb|
    vb.customize [
        'modifyvm', :id,
        '--name', hostname,
        '--memory', ram,
        '--cpus', cpu
    ]
  end

  config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provision/site.yml"
      ansible.verbose = "vvv"
  end

end
