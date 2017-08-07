# Vagrant-guide
#### A repository for understanding vagrant concepts
---

### Vagrant
![alt text](/images/vagrant_image.png)
<br />

### Vagrant frequently used commands 
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
![alt text](/images/vagrant_img_02.png)
<br />

```   
# -*- mode: ruby -*-
# vi: set ft=ruby :
$script = <<-SCRIPT
  sudo apt-get -y update
  sudo apt-get install -y nginx
  sudo service nginx start
SCRIPT

###################################
Vagrant.configure("2") do |config|
    # webserver server
    config.vm.define "webserver" do |webserver|
      webserver.vm.box = "minimum/ubuntu-trusty64-docker"
      webserver.ssh.insert_key = false
      webserver.vm.network "private_network", ip: "192.168.10.101",
        auto_config: true
        #virtualbox__intnet: "ansible-vagrant"
      webserver.vm.network "forwarded_port", guest: 80 , host: 4000, host_ip: "127.0.0.1"
      webserver.vm.hostname = "webserver"
      webserver.vm.provision "shell", inline: "sed 's/127\.0\.0\.1.*webserver.*/192\.168\.10\.101 webserver/' -i /etc/hosts"
      webserver.vm.provision "shell", inline: $script
      webserver.vm.provider "virtualbox" do |vb|
        # Customize VM
        vb.name = "webserver"
        vb.memory = "1024"
        vb.cpus = "2"
      end
    end
    #########################
    ### Add another box #####
    #########################
end
```
