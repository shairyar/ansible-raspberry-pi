# Prerequests

* Make sure [ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html) is installed


# Stucture
* `ansible.cfg` lets ansible know the inventory file to use. The [default location](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#how-to-build-your-inventory) of inventory file is `/etc/ansible/hosts`.
* We can also let ansible know which inventory file to use by defining it inside `ansible.cfg`, this way we do not have to use the `-i` flag all the time.
* `inventory.yml` contains the group of hosts.
* Directory `playbooks` contains all playbooks. `main.yml` imports other playbook.

## Playbooks

### Secure the Raspberry pi
Run this as the first playbook as this is meant to secure the Ubuntu serer by setting up an SSH based authentication and disable the password based authentication. Once this run successfully you do not need to run this again, unless you are adding another host in inventory.
```
ansible-playbook playbooks/secure.yml --check --ask-pass
```

`--ask-pass` will ask for a password, enter the password of a system you are SSHing into.

### Dependencies

#### Variables
Rename the file `etc/ansible/vars.example.yml` to `etc/ansible/vars.yml` and setup the values.
#### User
Create a user that will do deployment, after securing the server this is the first thing you should do as the app and it depencidens shoud be managed by app user so later on there are not permission issues.
```
ansible-playbook playbooks/setup/user/add.yml
```

In case you need to remove a user at any point, run the following playbook.
```
ansible-playbook playbooks/setup/packages.yml
```

#### Install ruby dependencies
```
ansible-playbook playbooks/setup/user/remove.yml
```
# Commands

## Dry run
Dry run any playbook with the `--check` flag for example

```
ansible-playbook playbooks/secure.yml --check
```

## Display inventory
```
ansible-inventory --list
```
## Update

To update all hosts

```
ansible-playbook playbooks/update.yml
```

## Shutdown

To shutdown all hosts

```
ansible-playbook playbooks/shutdown/run.yml
```

## Ping

### All hosts
```
ansible -m ping all -i inventory.yml
```

or

```
ansible -m ping all
```

### Webservers

```
ansible -m ping webservers -i inventory.yml
```
or
```
ansible -m ping webservers
```

### ToDo
- [ ] Find out how to manage dependencies `ansible-galaxy`
- Secureing Raspberry pi
  - [x] Add SSH key to the PI
  - [x] Disable password based login
- [ ] Use template
  - For setting hostnames
    - [ ] Webserver
    - [ ] Database
    - [ ] Redis
- [ ] Implement collections
- [ ] Shutdown specific host
- [ ] Deployment
  - [x] Add deploy user
  - [x] Remove deploy user
  - [ ] Dependencies
