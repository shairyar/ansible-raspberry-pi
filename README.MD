# Prerequests

* Make sure [ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html) is installed


# Stucture
* `ansible.cfg` lets ansible know the inventory file to use. The [default location](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#how-to-build-your-inventory) of inventory file is `/etc/ansible/hosts`.
* We can also let ansible know which inventory file to use by defining it inside `ansible.cfg`, this way we do not have to use the `-i` flag all the time.
* `inventory.yml` contains the group of hosts.
* Directory `playbooks` contains all playbooks. `main.yml` imports other playbook.


# Commands

## Check
Dry run any playbook with the `--check` flag for example `ansible-playbook playbooks/secure.yml --check`

## Display inventory
`ansible-inventory --list`

## Pinging

### All hosts
`ansible -m ping all -i inventory.yml` or `ansible -m ping all`

### Webservers

`ansible -m ping webservers -i inventory.yml` or `ansible -m ping webservers`

## Playbook
Ping hosts via playbook `ansible-playbook playbooks/main.yml`

### Secure the Raspberry pi
Run this as the first playbook as this is meant to secure the Raspberry pi by setting up an SSH based authentication and disable the password based authentication. Once this run successfully you do not need to run this again, unless you are adding another host in inventory.
```
ansible-playbook playbooks/secure.yml --ask-pass
```

### ToDo
- [ ] Find out how to manage dependencies `ansible-galaxy`
- Secureing Raspberry pi
  - [*] Add SSH key to the PI
  - [*] Disable password based login
- [ ] Use template
  - For setting hostnames
    - [ ] Webserver
    - [ ] Database
    - [ ] Redis
