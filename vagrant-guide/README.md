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

$vagrant halt # Stop the VMs 

$Vagrant destroy # Stop and clean boxes. This should take your VM back to pristine state

```

### Vagrantfile explanation
---
![alt text](/images/vagrantfile-flow.png)
<br />
