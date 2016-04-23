# -*- mode: ruby -*-
# # vi: set ft=ruby :

# Specify minimum Vagrant version and Vagrant API version
Vagrant.require_version ">= 1.6.0"
VAGRANTFILE_API_VERSION = "2"

# Require YAML module
require 'yaml'

# Read YAML file with box details
servers = YAML.load_file('servers.yaml')

# Create boxes
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Iterate through entries in YAML file
  servers.each do |servers|
    config.vm.define servers["name"] do |srv|

      # configure per VM parameters
      srv.vm.box = "vsphere-dummy"
      srv.vm.network "private_network", ip: servers["ip"]
      srv.vm.hostname = servers["name"]
      srv.vm.synced_folder ".", "/vagrant", disabled: true
      srv.vm.provider :vsphere do |vsphere|

        # define provider specific environment constants
        vsphere.host = 'complab-vc.complab.eng.vmware.com'
        vsphere.compute_resource_name = '6.0'
        vsphere.user = 'egrigson@complab'
        vsphere.password = 'Jarmila3!'
        vsphere.insecure = true
        vsphere.vm_base_path = '/users/Grigson'
        vsphere.data_store_name = 'complab-prmb-ds01'

        # define provider specific per-VM settings
        #the following vary based on the imported YAML file
        vsphere.template_name = servers["template"]
        vsphere.name = servers["name"]
        vsphere.memory_mb = servers["ram"]

      end
    end
  end
end
