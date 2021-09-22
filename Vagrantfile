# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :consul01 => {
             :box_name => "oraclelinux/8",
             :net => [
                      {ip: '192.168.100.10', adapter: 3, netmask: "255.255.255.0"},
                     ],
            },
  :consul02 => {
             :box_name => "oraclelinux/8",
             :net => [
                      {ip: '192.168.100.20', adapter: 3, netmask: "255.255.255.0"},
                     ],
            },
  :consul03 => {
             :box_name => "oraclelinux/8",
             :net => [
                      {ip: '192.168.100.30', adapter: 3, netmask: "255.255.255.0"},
                     ],
            },
  :pg01 => {
             :box_name => "oraclelinux/8",
             :net => [
                      {ip: '192.168.100.50', adapter: 3, netmask: "255.255.255.0"},
                     ],
            },
  :pg02 => {
             :box_name => "oraclelinux/8",
             :net => [
                      {ip: '192.168.100.60', adapter: 3, netmask: "255.255.255.0"},
                     ],
            },
}

hosts_file="127.0.0.1\tlocalhost\n"

MACHINES.each do |hostname,config|  
  config[:net].each do |ip|
      hosts_file=hosts_file+ip[:ip]+"\t"+hostname.to_s+"\n"
  end
end

Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|
    config.vm.define boxname do |box|
        box.vm.box = boxconfig[:box_name]
        box.vm.box_url = "https://oracle.github.io/vagrant-projects/boxes/oraclelinux/8.json"
        box.vm.host_name = boxname.to_s
        boxconfig[:net].each do |ipconf|
          box.vm.network "private_network", ipconf
        end
        box.vm.synced_folder '.', '/vagrant', disabled: true
        box.vm.provider "virtualbox" do |v|
          v.memory = 512
          v.cpus = 2
        end
        box.vm.provision "shell" do |shell|
          shell.inline = 'echo -e "$1" > /etc/hosts'
          shell.args = [hosts_file]
        end
        # box.vm.provision "ansible" do |ansible|
        #   ansible.playbook = "playbook.yml"
        # end
    end
  end
end