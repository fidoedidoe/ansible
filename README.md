## Ansible Playbooks: 

###### workstation-setup: Creates my standard Workstation setup

**Ansible roles:**
- common: general setup (installs vim, chrome, git, setups up bashrc, etc)
- developer: additional setup if android development is needed

**Run playbook:**
```
ansible-playbook -i workstations site.yml --ask-become-pass
ansible-playbook -i workstations site.yml --skip-tags "developer" --ask-become-pass
```

###### misc ad-hoc ansible  
**execute examples:**
```
ansible -i workstations -m ping all                            # Ping all hosts
ansible -i workstations -m setup all -a 'filter=ansible_*'     # list host facts 
ansible -i workstations -m command all -a "cat /proc/version"  # get hosts kernel version 
```
