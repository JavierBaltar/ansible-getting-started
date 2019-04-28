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

```yaml
- name: Remove users from the system.
  user:
    name: "{{ item }}"
    state: absent
    remove: yes
  with_items:
    - userA
    - userB
```

### With_nested

Define variables
```yaml
users_with_items:
  - name: "userA"
    personal_directories:
      - "old_files"
      - "maps"
      - "usb_files"
  - name: "userB"
    personal_directories:
      - "old_files"
      - "backup"
      - "storage"

common_directories:
  - "docs"
  - "media"
 ```
 
 ```yaml
 - name: Create common users directories using
  file:
    dest: "/home/{{ item.0.name }}/{{ item.1 }}"
    owner: "{{ item.0.name }}"
    group: "{{ item.0.name }}"
    state: directory
  with_nested:
    - "{{ users_with_items }}"
    - "{{ common_directories }}"
```

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
```yaml
- name: Sending message to Slack Channel
    slack:
      token: '{{ slack_token }}'
      channel: "#companynameAnsible"
      domain: "companyname.slack.com"
      parse: "full"
      color: "good"
      msg: 'The changes is completed on {{ inventory_hostname }}.'
 ```

#### Twilio

```yaml
- name: Send an SMS to multiple phone numbers when the change is completed
    twilio:
      msg: The configuration change is completed!
      account_sid: XXXXXXXXXXX
      auth_token: XXXXXXXXXXX
      from_number: +34XXXXXXXXX
      to_number:
        - +34XXXXXXXX1
        - +34XXXXXXXX2
    delegate_to: localhost
```

## Related

* [Ansible Modules](https://docs.ansible.com/ansible/latest/modules/modules_by_category.html) - List of Ansible modules
 

## Authors

* **Javier Baltar** - *Initial work* - [GitHub](https://github.com/JavierBaltar)

## Licence
