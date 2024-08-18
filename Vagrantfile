# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
  config.vm.box = 'generic/oracle8'  # Substitua por "oracle9" quando disponível

  config.vm.provider 'libvirt' do |libvirt|
    libvirt.memory = 2048
    libvirt.cpus = 2
  end

  config.vm.define 'podman-lab' do |podman_lab|
    podman_lab.vm.network 'private_network', ip: '192.158.200.10'
    podman_lab.vm.network 'forwarded_port', guest: 22, host: 2222, id: 'ssh'

    podman_lab.vm.provision 'ansible' do |ansible|
      ansible.compatibility_mode = '2.0'
      ansible.playbook = 'setup_environment.yml'
      ansible.config_file = './ansible.cfg'
      ansible.inventory_path = './inventories/development'
    end
  end
end
