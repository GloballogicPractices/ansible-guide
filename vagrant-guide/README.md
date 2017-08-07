### Vagrant
![alt text](/images/vagrant_image.png)
<br />
---


### Vagrant up flow 
---
![alt text](/images/vagrantup-flow.png)
<br />

---


### Vagrant frequently used commands 
---
```
$vagrant -h # Prints help 

$vagrant init # Initializes a default vagrant file in the present directory. 

$vagrant up --provider virtualbox # Download and start a virtual machine and use virtualbox for managing the VM. This can be replaced with VMWare or any other virtualization software

$vagrant ssh [VM-name for multibox setup] # Connect to the virtual machine using SSH 

$vagrant provision # Run a provisioner to configure the VM. ( Ansible, CHEF, Puppet, Shell ) 

$vagrant status # Show status on running machines 

$vagrant halt # Stop the VMs 

$Vagrant destroy # Stop and clean boxes. This should take your VM back to pristine state

```

### Vagrantfile explanation
---
![alt text](/images/vagrant_img_02.png)
<br />
