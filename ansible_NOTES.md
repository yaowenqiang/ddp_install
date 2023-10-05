Ad HOC  server management

+ func
+ pssh
+ cluster-ssh
+ parallel-ssh

Configuration management

+ chef
+ puppet


Deployments and orchestration

+ fabric
+ capistrano


Provisioning tools

+ terraform
+ head
+ cloud formation

> https://codespaces.schoolofdevops.com
> https://github.com/yaowenqiang/ansible-bootcamp-code.git

# ansible config files precedence

+ p1 command line flags
+ p2 ANSIBLE_CONFIG
+ p3 ./ansible.cfg
+ p4 ~/ansible.cfg
+ p5 /etc/ansible/ansible.cfg

> ansible-config dump
> ansible-config list

> ssh devops@lb

> pip install pipx
> pipx install --include-deps ansible
> pipx ensurepath

## Host patterns

### wildcards

+  all
+  *
+  app*
+  *.example.com

### hosts/groups

+ app1
+ app1:app2
+ db
+ app:lb

### subscripts

+ app[0]
+ app[-1]
+ prod[0:2]
+ prod[2:]

### Exclusion

+ 'prod!db'

### intersection

'prod:&app'

### regex

+ '~(app|db).*'



### --limit


> ansible all -m ping --limit lb
> ansible all -m ping
> ansible '*' -m ping
> ansible app* -m ping
> ansible app1:app2 -m ping
> ansible app1:app2:lb -m ping
> ansible prod -m ping # groups 
> ansible 'prod!db' -m ping # exclude db group 
> ansible 'prod!db!app' -m ping 
> ansible 'app[0]' -m ping 
> ansible '~(app|db).*' -m ping 
> ansible '~(app|db).*' -m ping  --limit app1


[prod:children]
app
db
lb

running on one host at a time


ansible all -f 1 -a 'free'

ansible all  -a  hostname
ansible all  -a  'uname -a'
ansible all  -b  -a  'yum install -y vim' # using sudo mode

ansible all  -b  -a  'useradd abc' 

## Modules

> python3 -m pip install --user ansible

> ansible-doc --list

> ansible app -m yum -s -a 'name=ntp stat=installed'

> ansible-doc --help
> ansible-doc --list
> ansible-doc --user
> ansible-doc -s user

## install package using module

> ansible app -m yum -a 'name=vim stat=present'

### common modules


Packages 

+ yum
+ apt
+ gem
+ pip

Files

+ copy
+ fetch
+ template

System

+ user
+ group
+ cron
+ mount
+ ping
+ ping

Utilities

+ debug
+ assert
+ wait_for

Commands

+ command
+ shell
+ expect


#### add  group

> ansible prod -m  group -b -a 'name=admin stat=present gid=7045'

### add user

> ansible prod -m  user -b -a 'name=abc stat=present uid=7001 group=admin'

### copy files

> ansible prod -m  copy  -a 'src=test.txt dest=/tmp/test.txt mode=0644'

### Commands modules

Core 

+ raw - bypass modules subsystem and execute raw ssh command
+ command - execute a command on a remote node without shell
+ shell - execute a command on a remote node with /bin/sh
+ script - copy a script to the remote node and also execute it
+ expect - execute a interactive command and auto respond to prompts

command 

+ does not use shell
+ does not have access to env
+ ><  | ; & operators will not work

shell

+ invokes /bin/sh
+ has access to env, variables
+ ><  | ; & operators will wor 


> ansible app -m command -a 'free'
> ansible app -m command -a 'free | grep -i swap'
> ansible app -m command -a 'free' | grep  -i swap
> ansible app -m shell -a 'free' | grep  -i swap
> ansible app -m shell -vvvv -a 'free' | grep  -i swap

### create dir 

> ansible app -m command -a 'mkdir /tmp/dir1' # command will fail if dir exists
> ansible app -m command -a 'mkdir /tmp/dir1 creates=/tmp/dir1' # command will skip if dir exists

## ansible-console

> ansible-console -b
> ansible-console -b prod

> ? shell # get help for shell module

> list-hosts
> setup

# playbooks

## yaml

> https://www.yamllint.com

## apply playbooks

> ansible-playbook config.yml --syntax-check

### listing hosts and tasks

> ansible-playbook config.yml --list-hosts
> ansible-playbook config.yml --list-tasks
> ansible-playbook config.yml --list-tags

### dry run

> ansible-playbook config.yml --check

## apply

> ansible-playbook config.yml

## step by step execution

> ansible-playbook config.yml --step

## retry

> ansible-playbook config.yml --limit @/tmp/system.retry

## start-at-task

> ansible-playbook config.yml  --start-at-task='task name'

## limit hosts

> ansible-playbook config.yml  --limit app


# Roles

## ansible-galaxy


> ansible-galaxy init --init-path roles/ apache

> ansible-galaxy init --offline --init-path roles/ apache
> ansible-galaxy --help

> ansible-playbook app.yml

# templates

## variable precedence

+ -e switch
+ rule vars
+ playbook vars
+ host vars
+ group vars
+ role defaults


### hash behavior

> ansible-config dump | grep -i hash


## Registered variables

