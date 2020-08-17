Vagrant.require_version ">= 1.8.0"

Vagrant.configure(2) do |config|

  # Define Boxes
  config.vm.define "server" do |server|
    server.vm.box = "centos/8"
  end
  config.vm.define "node1" do |node1|
    node1.vm.box = "ubuntu/trusty64"
  end

  config.vm.provider "virtualbox" do |vb|
     vb.memory = "1024"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "auto"
    ansible.verbose = true

    # Call the default playbook.
    ansible.playbook = "provisioning/site.yml"

    # Optionally filter tags (string or array of strings)
    ansible.tags = ["wireguard"]

    # Set of inventory groups to be included in the auto-generated inventory file.
    ansible.groups = {
      "servers" => ["server"],
      "servers:vars" => {"ansible_sudo_pass" => "vagrant"},
      "peers"  => ["node1"]
    }

    # default password for vagrant boxes to allow sudo priviledges
    ansible.extra_vars = {
      ansible_sudo_pass: "vagrant"
    }
  end

end
