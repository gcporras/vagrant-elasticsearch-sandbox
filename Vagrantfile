# -*- mode: ruby -*-
# vi: set ft=ruby :

require "yaml"

# Import Vagrant configuration files
vagrant_config = YAML.load(File.open(File.join(File.dirname(__FILE__), "vagrantconfig.yml"), File::RDONLY).read)
begin
  local_config = YAML.load(File.open(File.join(File.dirname(__FILE__), "vagrantconfig_local.yml"), File::RDONLY).read)
  if local_config
    vagrant_config.merge!(local_config)
  end
rescue Errno::ENOENT
end

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

# Verify vagrant-hostupdater  plugin is installed
unless Vagrant.has_plugin?("vagrant-hostsupdater")
  raise 'vagrant-hostsupdater is not installed! Please run the following command on your terminal:
         "vagrant plugin install vagrant-hostsupdater"'
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "trusty64"
  config.vm.box_url = "https://vagrantcloud.com/ubuntu/trusty64/version/1/provider/virtualbox.box"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  config.ssh.forward_agent = true


  # elasticsearch-Master service server.
  config.vm.define "elasticsearch-server" do |service|
    # If you change this name please change also the value in elasticsearch_proxy_hostname
    service.vm.hostname = "elasticsearch.local"

    # Create a private network, which allows host-only access to the machine
    # using a specific IP.
    service.vm.network "private_network", ip: vagrant_config['network_ip']

    # Provider-specific configuration (VirtualBox):
    config.vm.provider "virtualbox" do |vb|
    # Use VBoxManage to customize the VM. For example to change memory:
      vb.customize ["modifyvm", :id, "--memory", vagrant_config['memory']]
      vb.customize ["modifyvm", :id, "--cpus", vagrant_config['cpus']]
    end

    # Provisioning configuration for Ansible.
    service.vm.provision "ansible" do |ansible|
      ansible.inventory_path = "ansible/hosts"
      ansible.playbook = "ansible/site.yml"
      ansible.limit = "elasticsearch"
    end
  end

end
