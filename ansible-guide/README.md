![alt text](/images/ansible_logo.png)

---

### YAML Primer

YAML - Yet another Markup language or Yaml aint markup language ?
- Yaml is a strict superset of JSON. 
- Much easier to read and interpret thant Json 
- Parsers can be used to understand data structures spurning out of YAML. [Parser](http://yaml-online-parser.appspot.com/)

- Scalars: Strings, Numbers, Literals 
  * key: value 
  
- Maps : K/V pairs but can be nested and complex
  * name: John 
  * location: Denver
  * skills: { core: developer, secondary: cloud }
  
- Sequence: List or arrays 
  * [1,2,3,4]
  * ['fai','gkl','zok']
  
Head over to [YAML-Tutorial](https://learnxinyminutes.com/docs/yaml/) 
  

### Ansible-command

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

##### Ansible Inventory 

