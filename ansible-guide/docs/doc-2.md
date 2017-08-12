### Ansible configuration

We can configure Ansible using different methods. Convention is use ```ansible.cfg``` as the file name. Order of configuration parsing

```shell
- export ANSIBLE_CONFIG=/path/to/ansible.cfg # Environment variable
- ansible.cfg # In the current directory
- .ansible.cfg # In ~/. ( home ) directory
- /etc/ansible/ansible.cfg
```

Sample configuration file

```shell
[defaults]
remote_user=ec2-user  # User which has ssh permission on target machines
host_key_checking = False # This way you don't get prompted for accepting host key. This however could have security implications. Please read documentation
inventory = /Users/my-generic-user/my-work/ansible-code/hosts/ # Location of inventory file
# Enabling pipelining reduces the number of SSH operations required to
# execute a module on the remote server. This can result in a significant
# performance improvement when enabled, however when using "sudo:" you must
# first disable 'require-tty' in /etc/sudoers
pipelining = True
timeout = 25
retry_files_enabled = False
connect_timeout = 30
connect_retries = 30

# Below settings are relevant for cases where you have a private/public network and ansible is to be executed from a specific machine in public subnet with restrictive permissions
[ssh_connection]
ssh_args = -F /Users/my-generic-user/my-work/ansible-code/ssh.cfg -o UserKnownHostsFile=/dev/null
control_path = ~/.ssh/ansible-%%r@%%h:%%p
private_key_file = /Users/my-generic-user/.ssh/myprivate-keys.pem

```


[Ansible-config-document](http://docs.ansible.com/ansible/latest/intro_configuration.html)
[Ansibe-config-exmaple](https://raw.githubusercontent.com/ansible/ansible/devel/examples/ansible.cfg)


### Exercise

- Setup ansible.cfg
- Find uptime of the target machine using ansible command ( ) # Hint: Use [command](http://docs.ansible.com/ansible/latest/command_module.html) module
- Tail /var/log/syslog # Hint: You may have to use elevated privileges to do this
- Install apache or nginx using ansible command. # Hint: Use [apt](http://docs.ansible.com/ansible/latest/apt_module.html) module

#### NOTE:

- Modules are the ones that do the actual work in ansible. They are like pluggable components that allow you perform actions on target hosts. Example modules
 - command
 - ping
 - apt
 - yum
 and many more
