VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "alvistack/ubuntu-24.04"
  config.vm.provider :vmware_desktop

  nodes = {
    "master-node" => "192.168.56.13",
    "worker-node1" => "192.168.56.14"
    # "worker-node2" => "192.168.56.12"
  }

  nodes.each do |name, ip|
    config.vm.define name do |node|
      node.vm.hostname = name
      node.vm.network "private_network", ip: ip

      node.vm.provider :vmware_desktop do |v|
        v.memory = 6144
        v.cpus = 2
      end
      node.vm.synced_folder ".", "/vagrant", disabled: true
      node.vm.provision "shell", inline: <<-SHELL
        # Update and install Python
        export DEBIAN_FRONTEND=noninteractive
        apt-get update -y
        apt-get upgrade -yq
        apt-get install -y python3 python3-pip python-is-python3
      SHELL
    end
  end
end
# This Vagrantfile sets up a Kubernetes cluster with one master node and one worker node.

# VAGRANTFILE_API_VERSION = "2"

# Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
#   config.vm.box = "alvistack/ubuntu-24.04"
#   config.vm.provider :vmware_desktop

#   nodes = {
#     "master-node" => "192.168.56.13",
#     "worker-node1" => "192.168.56.14"
#     # "worker-node2" => "192.168.56.12"
#   }

#   nodes.each do |name, ip|
#     config.vm.define name do |node|
#       node.vm.hostname = name
#       node.vm.network "private_network", ip: ip

#       node.vm.provider :vmware_desktop do |v|
#         v.memory = 6144
#         v.cpus = 2
#       end

#       node.vm.synced_folder ".", "/vagrant", disabled: true

#       node.vm.provision "shell", inline: <<-SHELL
#         # Update and install Python
#         export DEBIAN_FRONTEND=noninteractive
#         apt-get update -y
#         apt-get upgrade -yq
#         apt-get install -y python3 python3-pip python-is-python3
#       SHELL
#     end
#   end

#   # Run the Ansible playbook after all VMs are up
#   config.vm.provision "ansible_local", run: "always" do |ansible|
#     ansible.playbook = "/vagrant/ansible/site.yml"  # Change this path to your actual playbook path
#     ansible.limit = "all"
#   end
# end
