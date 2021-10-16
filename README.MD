# Prerequests

* Make sure [ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html) is installed


# Stucture
* `ansible.cfg` lets ansible know the inventory file to use. The [default location](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#how-to-build-your-inventory) of inventory file is `/etc/ansible/hosts`.
* We can also let ansible know which inventory file to use by defining it inside `ansible.cfg`, this way we do not have to use the `-i` flag all the time.
* `inventory.yml` contains the group of hosts.
* Directory `playbooks` contains all playbooks. `main.yml` imports other playbook.


# Commands

## Display inventory
`ansible-inventory --list`

## Pinging

### All hosts
`ansible -m ping all -i inventory.yml` or `ansible -m ping all`

### Webservers

`ansible -m ping webservers -i inventory.yml` or `ansible -m ping webservers`

### Playbook
Ping hosts via playbook `ansible-playbook playbooks/main.yml`

### ToDo
- [ ] Use template
  - For securing PI
    - [ ] Disable password based login
  - For setting hostnames
    - [ ] Webserver
    - [ ] Database
    - [ ] Redis
