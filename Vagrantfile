# -*- mode: ruby -*-
# # vi: set ft=ruby :
 
# Specify minimum Vagrant version and Vagrant API version
Vagrant.require_version ">= 1.6.0"
VAGRANTFILE_API_VERSION = "2"
 
# Require YAML module
require 'yaml'
 
# Read YAML files with server and vCenter details.
# Use the full path to ensure 'vagrant --global-status' still works.
servers = YAML.load_file(File.join(File.dirname(__FILE__),'servers.yaml'))
vcenter = YAML.load_file(File.join(File.dirname(__FILE__),'vcenter.yaml'))
 
# Create boxes
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
 
# configure VM defaults (global for all VMs)
config.vm.box = "vsphere-dummy"
config.vm.synced_folder ".", "/vagrant", disabled: true

# define provider specific defaults (vCenter info)
config.vm.provider :vsphere do |vsphere|
  vsphere.host = 			vcenter["vcenter_srv"]
  vsphere.compute_resource_name = 	vcenter["cluster"]
  vsphere.user = 			vcenter["username"]
  vsphere.password =			vcenter["password"]
  vsphere.insecure =			vcenter["secure"] 
end
 
# Iterate through entries in YAML file
  servers.each do |servers|

    # Use multi-machine definition
    config.vm.define servers["name"] do |srv|

      # define generic per-VM settings
      srv.vm.network "private_network", ip: servers["ip"]
      srv.vm.hostname = servers["name"]

      # define provider specific, per-VM settings
      srv.vm.provider :vsphere do |vsphere|
        vsphere.template_name = 	servers["template"]
        vsphere.name = 			servers["name"]
        vsphere.memory_mb = 		servers["ram"]
        vsphere.data_store_name = 	servers["datastore"] 
        vsphere.vm_base_path = 		servers["vm_path"] 
      end
    end
  end
end
