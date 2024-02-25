# my ansible conf files

## commiting changes every now and then
# what this basically does is ping other nodes through connecting to them with ssh using the path fo>
####and -i for inventory and -m is specifying that we're using module ping
ansible all --key-file ~/.ssh/ansible -i inventory -m ping

####to list all hosts
ansible all --list-hosts

####output all the system information for all hosts
ansible all -m  gather_facts
####output all information about specific host
ansible all -m gather_facts --limit 192.168.30.164
####to run any priveleged command we use --become 
####and --ask-become pass for pass promt
ansible all -m apt -a update_cache=true --become --ask-become-pass
####install specific package in this case it's vim-nox
ansible all -m apt -a name=vim-now --become --ask-become-pass
####to install with more than one argument at a time we double "" 
####after the -a arguments flag 
ansible all -m apt -a "name=snapd state=latest" --become --ask-become-pass
####upgrade example
ansible all -m apt -a "upgrade=dist" --become --ask-become-pass
####to run a playbook that contains root priveleges
ansible-playbook  --ask-become-pass nameOfPlaybook.yml
####to list all tags in specific playbook in our case the playbook is site.yml
ansible-playbook --list-tags site.yml
####to run tasks that contains specific tag in our case the tag name is ubuntu
ansible-playbook --tags ubuntu --ask-become-pass site.yml
