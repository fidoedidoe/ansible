## Ansible Playbooks: 
---

#### workstation-setup: Creates a standard Workstation setup

Ansible roles:
- common: general setup (installs vim, chrome, git, setups up bashrc, etc)
- developer: additional setup if android development is needed
- aws_ec2_start
- aws_ec2_stop
- aws_ec2_gather_info

Run playbook:
```
ansible-playbook -i virtualbox.yml site.yml --ask-become-pass
ansible-playbook -i virtualbox.yml site.yml --skip-tags "developer" --ask-become-pass
ansible-playbook -i virtualbox.yml site.yml --skip-tags "developer" --ask-become-pass --syntax-check
ansible-playbook -i virtualbox.yml site.yml --skip-tags "developer" --ask-become-pass --check --diff
ansible-playbook -i virtualbox.yml site.yml --skip-tags "developer" --ask-become-pass --list-hosts
ansible-playbook -i virtualbox.yml site.yml --limit workstation_01 --tags "common, developer" --ask-become-pass
ansible-playbook -i virtualbox.yml -i inventory_aws_ec2.yml site.yml --tags "common" --ask-become-pass
```
Run ansible-inventory:
```
ansible-inventory -i virtualbox.yml --graph
ansible-inventory -i inventory_aws_ec2.yml --graph
```
---
#### aws-instances: start/stop instances using dynamic inventory

roles:
- aws_ec2_provision: 
- aws_ec2_info:
- aws_ec2_start:
- aws_ec2_stop:
- aws_ec2_terminate: 

Run playbook:
```
ansible-playbook -i inventory_aws_ec2.yml site.yml --tags="aws_ec2_provision"
ansible-playbook -i inventory_aws_ec2.yml site.yml --tags="aws_ec2_info"
ansible-playbook -i inventory_aws_ec2.yml site.yml --tags="aws_ec2_start"
ansible-playbook -i inventory_aws_ec2.yml site.yml --tags="aws_ec2_stop"
ansible-playbook -i inventory_aws_ec2.yml site.yml --tags="aws_ec2_terminate"
```
---
#### misc ad-hoc ansible  

Run ansible ad-hoc  examples:
```
ansible -i workstations -m ping all                            # Ping all hosts
ansible -i workstations -m setup all -a 'filter=ansible_*'     # list host facts 
ansible -i workstations -m command all -a "cat /proc/version"  # get hosts kernel version 
```