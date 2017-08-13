### Ansible playbook or plays

A playbook in Ansible is a list of plays and each play can be made up one or more tasks. An example would make things more clear

```shell

# A playbook that consists of two plays

# Play - 1
- name: Setup Nginx
  hosts: webservers-nginx
  become: True
  # This play consists of 5 tasks
  tasks:
    - name: install nginx   # Task 1
      apt: name=nginx update_cache=yes

    - name: copy nginx config file # Task 2
      copy: src=files/nginx.conf dest=/etc/nginx/sites-available/default

    - name: enable configuration # Task 3
      file: >
        dest=/etc/nginx/sites-enabled/default
        src=/etc/nginx/sites-available/default
        state=link

    - name: copy index.html # Task 4
      template: src=templates/index.html.j2
               dest=/usr/share/nginx/html/index.html mode=0644

    - name: restart nginx # Task 5
      service: name=nginx state=restarted

# Play - 2
- name: Setup apache
  hosts: webservers-apache
  become: True
  tasks:
    - name: install apache # Task 1
      apt: name=apache2 update_cache=yes

    - name: copy index.html # Task 2
      template: src=templates/index.html.j2
               dest=/var/www/html/index.html mode=0644

    - name: restart apache # Task 3
      service: name=apache2 state=restarted

```

Every play must contain
- A set of hosts to configure
- A set of tasks to be executed on those hosts
