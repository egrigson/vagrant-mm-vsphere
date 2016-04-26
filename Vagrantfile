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
 
  # Iterate through entries in YAML file
  servers.each do |servers|

    # configure VM defaults (global for all VMs)
    config.vm.box = "vsphere-dummy"
    config.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.define servers["name"] do |srv|

      # configure per VM parameters
      #srv.vm.box = "vsphere-dummy"
      srv.vm.network "private_network", ip: servers["ip"]
      srv.vm.hostname = servers["name"]
      srv.vm.provider :vsphere do |vsphere|

        # define provider specific environment constants
        vsphere.host = 			vcenter["vcenter_srv"]
        vsphere.compute_resource_name = vcenter["cluster"]
        vsphere.user = 			vcenter["username"]
        vsphere.password =		vcenter["password"]
        vsphere.insecure =		vcenter["secure"] 

        # define provider specific, per-VM settings
        #the following vary based on the imported YAML file
        vsphere.template_name = 	servers["template"]
        vsphere.name = 			servers["name"]
        vsphere.memory_mb = 		servers["ram"]
        vsphere.data_store_name = 	servers["datastore"] 
        vsphere.vm_base_path = 		servers["vm_path"] 

      end
    end
  end
end
