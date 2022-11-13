servers=[
  {
    :hostname => "masternode",
    :ip => "192.168.50.4",
    :box => "rockylinux/8",
    :version => "4.0.0",
    :ram => 2524,
    :cpu => 2,
    :role => "master"
  },
  {
    :hostname => "workernode",
    :ip => "192.168.50.9",
    :box => "rockylinux/8",
    :version => "4.0.0",
    :ram => 1048,
    :cpu => 1,
    :role => "worker"
  }
]

Vagrant.configure("2") do |config|
  servers.each do |machine| 
    config.vm.define machine[:hostname] do |subconfig|
      subconfig.vm.box = machine[:box]
      subconfig.vm.box_version = machine[:version]
      subconfig.vm.hostname = machine[:hostname] 
      subconfig.vm.network "public_network"
      subconfig.vm.network "private_network" ,ip: machine[:ip]
    end 
    config.vm.provider "#{machine[:hostname]}1" do |vb|
      vb.memory = machine[:ram]
      vb.cpus = machine[:cpu]
    end
    config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "ansible_playbook/playbook.yml"
      ansible.extra_vars ={
            node: machine[:role],
            hostname: machine[:hostname],
            ip: machine[:ip]
          }
    end
  end
end