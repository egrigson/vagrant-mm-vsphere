# vagrant-mm-vsphere
A multi-machine Vagrant configuration

These files were created to allow users to use Vagrant (http://www.vagrantup.com) to quickly and relatively easily provision multiple VMs in a vSphere environment. The configuration was tested using Vagrant 1.8.1, vSphere 6.0, and the [Vagrant vSphere plugin](https://github.com/nsidc/vagrant-vsphere).

## Contents
**README.md**: This file you're currently reading.

**servers.yaml**: This YAML file contains a list of VM definitions and associated configuration data. It is referenced by Vagrantfile when Vagrant instantiates the VMs.

**Vagrantfile**: This file is used by Vagrant to spin up the virtual machines. This file is fairly extensively commented to help explain what's happening. You'll have to edit this for your environment, substituting your vCenter, username/password, etc.

**vcenter.yaml.EXAMPLE**: This YAML file contains details for your vCenter instance, including credentials. You'll need to amend this file accordingly and save it as vcenter.yaml in same directory as your Vagrantfile and servers.yaml file (drop the EXAMPLE).
