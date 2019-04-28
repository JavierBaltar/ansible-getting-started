# ansible-getting-started

<p align="center">
  <a href="#Inventory">Inventory</a> •
  <a href="#Playbooks">Playbooks</a> •
  <a href="#Roles">Roles</a> •
  <a href="#Loops">Loops</a> •
  <a href="#Modules">Modules</a> •
  <a href="#related">Related</a> •
  <a href="#license">License</a>
</p>


## Inventory
Intentory file location
`$ /etc/ansible/hosts`

### Format

```yaml
[cisco-ios-devices]
10.10.0.1
10.10.0.2

[cisco-nxos-devices]
10.10.20.1
10.10.20.2
```

### Variables

```yaml
[cisco-ios-devices]
10.10.0.1
10.10.0.2

[cisco-ios-devices:vars]
ansible_port=22
ansible_user=netadmin
```

### Grouping

```yaml
[cisco-ios-devices]
10.10.0.1
10.10.0.2

[cisco-nxos-devices]
10.10.20.1
10.10.20.2

[network-devices:children]
cisco-ios-devices
cisco-nxos-devices
```

### Patterns

```yaml
[cisco-nexus-7000]
nexus[01:04].companydomain.com
```

`nexus01.companydomain.com
nexus02.companydomain.com
nexus03.companydomain.com
nexus04.companydomain.com
`

## Playbooks
Intentory file location
`$ /etc/ansible/hosts`

### Handlers

```yaml
---
- hosts: webservers

  tasks: 
    - name: Install Nginx
      apt: pkg=nginx state=installed update_cache=true
      notify:
        - Start Nginx

  handlers:
    - name: Start Nginx
      service: name=nginx state=started

```

## Roles

## Templates


## Loops
### With_items

### With_nested

## Useful Commands
### List group nodes


`# ansible group-name --list-hosts`


## Modules
### Files

#### Archive

```yaml
- name: Backup Directory /var/log/application01/
  hosts: webservers
  tasks:
   - archive:
      path: /var/log/application01/
      dest: "/var/backups/application01-{{ ansible_date_time.date }}.tgz"

```

#### Copy

```yaml
- name: Copy File
  hosts: webserver
  tasks:
   - copy:
      src: /var/log/application01/filename
      dest: "/var/backups/filename
      owner: root
      group: root
      mode: u=r,g=r,o=

```

#### Fetch

```yaml
- name: Copy File from Remote Node
  hosts: webserver
  tasks:
   - fetch:
      src: /var/log/application01/filename
      dest: "/var/backups/
```

### Notifications

#### Slack

#### Twilio

```yaml
# send an SMS to multiple phone numbers about the deployment
# note: replace account_sid and auth_token values with your credentials
# and you have to have the 'from_number' on your Twilio account
- twilio:
    msg: This server configuration is now complete.
    account_sid: ACXXXXXXXXXXXXXXXXX
    auth_token: ACXXXXXXXXXXXXXXXXX
    from_number: +15553258899
    to_number:
      - +15551113232
      - +12025551235
      - +19735559010
  delegate_to: localhost
```

## Related

* [Ansible Modules](https://docs.ansible.com/ansible/latest/modules/modules_by_category.html) - List of Ansible modules
 

## Authors

* **Javier Baltar** - *Initial work* - [GitHub](https://github.com/JavierBaltar)

## Licence
