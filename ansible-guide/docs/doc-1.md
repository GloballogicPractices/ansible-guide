## Ansible-command

- ```ansible``` is a quick way of getting started with Ansible.
- Lets you execute ansible commands when you don't need to save those commands
- [ad-hoc-commands](http://docs.ansible.com/ansible/latest/intro_adhoc.html)

#### Trying ansible command with Vagrant

```shell
$ vagrant ssh-config # Taking our webserver

Host webserver

testserver ansible_ssh_host=127.0.0.1 ansible_ssh_port=2222 \
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /Users/$USER/.vagrant.d/insecure_private_key
  IdentitiesOnly yes
  LogLevel FATAL

# Try to ssh using the privatek key

$ ssh vagrant@127.0.0.1 -p 2222 -i /Users/$USER/.vagrant.d/insecure_private_key # Should get you in the webserver machine

```
#### Ansible needs to know your infrastructure

In order for Ansible to configure our infrastructure for us, we need to provide Ansible with some details such as
- Private key location
- Hosts and roles they play
- And many other things based on the environment

How do we do all this?

#### Ansible Inventory

- Each server needs a name or way of being identified by Ansible.
- We can use the hostname of the server, or you can give it an alias
- We can pass some additional arguments to tell Ansible how to connect to the VM.
* Example

```
# Create a directory
# CD to that directory
# Create an inventory file # A file that provides information about machines to be configure. ( Dynamic inventory to be visited later )
$ cat > /home/$USER/ansible/playbooks/hosts
# Paste below content
“myfirstserver ansible_ssh_host=127.0.0.1 ansible_ssh_port=2222 \ # If this was aws instance ansible_ssh_host=ec2-x-x-y.compute-1.amazonaws.com
 ansible_ssh_user=vagrant \
 ansible_ssh_private_key_file=${PRIVATE_KEY_FILE_OBTAINED_THROUGH_VAGRANT_SSH_CONFIG_COMMAND}
 ”
```

#### First step

```shell
$ ansible myfirstserver -i /home/$USER/ansible/playbooks/hosts -m ping

/*
ansible is the executuable command being called
-i flag tells ansible about the inventory file location
-m flag tells ansible module to be called which is the ping module in this case # Modules to be discussed later
*/

NOTE:
ssh by default has host key verification enabled. This allows instances we connect to, to be tracked. You may see a warning which needs to be bypassed.

# OUTPUT
myfirstserver | success >> {
    "changed": false,
    "ping": "pong"
}

# In case of error please run

$ ansible myfirstserver -i /home/$USER/ansible/playbooks/hosts -m ping -vv # This will print details of steps being executed by Ansible
