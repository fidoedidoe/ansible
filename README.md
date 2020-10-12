## Ansible Playbooks: 
---

#### workstation-setup: Creates a standard Workstation setup

Ansible roles:
- common: general setup (installs vim, chrome, git, setups up bashrc, etc)
- developer: additional setup if android development is needed
- aws_instance_start
- aws_instance_stop
- aws_instance_gather_info

Run playbook:
```
ansible-playbook -i workstations site.yml --ask-become-pass
ansible-playbook -i workstations site.yml --skip-tags "developer" --ask-become-pass
ansible-playbook -i workstations site.yml --skip-tags "developer" --ask-become-pass --syntax-check
ansible-playbook -i workstations site.yml --skip-tags "developer" --ask-become-pass --check --diff
ansible-playbook -i workstations site.yml --skip-tags "developer" --ask-become-pass --list-hosts
ansible-playbook -i workstations site.yml --limit workstation_01 --skip-tags "developer" --ask-become-pass
ansible-playbook -i inventory_aws_ec2.yml -i workstations site.yml --tags "aws_gather_info, common" --ask-become-pass
```
---
#### aws-instances: start/stop instances using dynamic inventory

roles:
- start_aws_instances: 
- stop_aws_instances: 

Run ansible-inventory:
```
ansible-inventory -i inventory_aws_ec2.yml --graph
```

Run playbook:
```
ansible-playbook -i inventory_aws_ec2.yml site.yml --tags "start_instances"
ansible-playbook -i inventory_aws_ec2.yml site.yml --tags "stop_instances"
```
---
#### misc ad-hoc ansible  

Run ansible ad-hoc  examples:
```
ansible -i workstations -m ping all                            # Ping all hosts
ansible -i workstations -m setup all -a 'filter=ansible_*'     # list host facts 
ansible -i workstations -m command all -a "cat /proc/version"  # get hosts kernel version 
```
