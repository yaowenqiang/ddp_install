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






