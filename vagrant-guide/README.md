![alt text](/images/vagrant_image.png)

<br />


### Vagrant up flow 
---
![alt text](/images/vagrantup-flow.png)
<br />


### Vagrant frequently used commands 
---
```shell

$vagrant -h # Prints help 

$vagrant init # Initializes a default vagrant file in the present directory. 

$vagrant ini ubuntu/trusty64 # This will create a Vagrantfile with the specified basebox

$vagrant ssh-config # Gives you detail of your ssh-configuration used by vagrant to get you access to the VM

$vagrant up --provider virtualbox # Download and start a virtual machine and use virtualbox for managing the VM. This can be replaced with VMWare or any other virtualization software

$vagrant ssh [VM-name for multibox setup] # Connect to the virtual machine using SSH 

$vagrant provision # Run a provisioner to configure the VM. ( Ansible, CHEF, Puppet, Shell ) 

$vagrant status # Show status on running machines 

$vagrant global-status # Useful with multi machine setup

$vagrant reload # Reload your VM to pick changes in configuration

$vagrant halt # Stop the VMs 

$Vagrant destroy # Stop and clean boxes. This should take your VM back to pristine state

```

### Vagrantfile explanation
---
![alt text](/images/vagrantfile-flow.png)
<br />

```shell
/* 
The API version for vagrant. 
Two versions are supported - 1 & 2
Version 1 is prior to vagrant version 1.1 and 2 is post 1.1 
When loading Vagrantfiles, Vagrant uses the proper configuration object for each version, and properly merges them, just like any other configuration.
*/

Vagrant.configure("2") do |config|
end
```

```shell
/*
Basebox refers to virtual image 
Basebox is hosted on vagrant cloud 
*/
config.vm.box = "bento/ubuntu-16.04"

```

```shell
/* 
Vagrant networks
Vagrant supports both public/private networks
config.vm.network is the method call to get started with Vagrant networking 
*/

# Example private network with static IP 
config.vm.network :private_network, ip: "10.0.0.12", auto_config: true # auto_config: true helps with port collisions when running multi network machines

# Example private network with DHCP
config.vm.network "private_network", type: "dhcp", auto_config: true # This will automatically assign an IP address from the reserved address space

# Public network will bridge adapter to a particular Network interface
# Example public network with DHCP 
config.vm.network "public_network" # This will automatically assign an IP address. 

# NOTE: 
- If more than one adapter is available on the machine, vagrant will prompt to select one of the adapters or a specific adapter can be specified
- Public networks on Vagrant should be avoided due to security issues. 

config.vm.network "public_network", bridge: "en1: Wi-Fi (AirPort)"

# Port-forwarding 
config.vm.network "forwarded_port", guest: 80, host: 8080 # This will allow access to application running on port 80 inside the VM by accessing port 8080 on the host machine. 

# NOTE:
The behavior for port forwarding on private networks is bit unclear to. Please follow SO post: https://stackoverflow.com/questions/45533628/vagrant-unable-to-reach-nginx-via-private-ip to track this. 


