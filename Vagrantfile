Vagrant.require_version ">= 1.8.0"

Vagrant.configure(2) do |config|

  config.vm.box = "centos/8"

  config.vm.provider "virtualbox" do |vb|
     vb.memory = "1024"

  end

# Server
  config.vm.define "server" do |server|
    server.vm.hostname = "server"
    server.vm.box = "centos/8"
  end

# Peer 1
  config.vm.define "peer1" do |p1|
    p1.vm.hostname = "peer1"
    p1.vm.box = "debian/jessie64"
  end


  config.vm.provision "ansible" do |ansible|
    ansible.verbose = true
    ansible.playbook = "provisioning/site.yml"
    ansible.groups = {
      "servers" => ["server"],
      "peer_group_1" => ["peer1"],
      "peers:children" => ["peer_group_[1-100]"]
    }

    ansible.host_vars = {
      "server" => {"ansible_become_pass" => 'vagrant' },
      "peer1" => {"ansible_become_pass" => 'vagrant' }
    }
  end

end
