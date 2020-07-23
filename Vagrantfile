Vagrant.require_version ">= 1.8.0"

Vagrant.configure(2) do |config|

  config.vm.box = "debian/jessie64"

  config.vm.provider "virtualbox" do |vb|
     vb.memory = "1024"

  end

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = true
    ansible.playbook = "provisioning/site.yml"
  end

end
