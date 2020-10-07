Ansible Playbooks: 

* workstation-setup: Creates my standard Workstation setup
** multiple roles: 
** common: general setup (installs vim, chrome, git, setups up bashrc, etc)    
** developer: setup for android development.
*** execute:
*** ansible-playbook -i workstations site.yml -K 
*** ansible-playbook -i workstations site.yml --skip-tags "developer" -K

* misc
** execute:
** ansible -i workstations -m ping all
** ansible -i workstations -m setup all -a 'filter=ansible_*'
** ansible -i workstations -m command all -a "cat /proc/version" 
