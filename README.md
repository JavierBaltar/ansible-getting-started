# ansible-getting-started

<p align="center">
  <a href="#Getting-Started">Getting Started</a> •
  <a href="#Prerequisites">Prerequisites</a> •
  <a href="#Installing">Installing</a> •
  <a href="#Next-Steps">Next Steps</a> •
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


## Useful Commands
### List group nodes


`# ansible group-name --list-hosts`



![](ciscoDevnetSandboxes.gif)

#### Toolkit

- Python. I am using Python 2 and PyCharm IDE.
- A CUCM instance
- AXLSQLToolkit 
- zeep
- A Coffee mug 

## Modules
#### Export to CSV 

```yaml
import csv
 
callmanagerdata = [["customer", "version"],
          ['CustomerA', '10.5'],
          ['CustomerB', '11.5']]
 
File = open('callmanager-data.csv', 'w')
with File:
    writer = csv.writer(File)
    writer.writerows(callmanagerdata)
     
print("Writing complete!")
```

#### Export to SQLite

```python
import sqlite3
con_obj = sqlite3.connect("callmanager-data.db")
with con_obj:
            cur_obj = con_obj.cursor()
            cur_obj.execute("""CREATE TABLE cucm_version(customer text, version text)""")

print ("Table created!")
```

## Related

* [Cisco Administrative XML (AXL)](https://developer.cisco.com/site/axl/) - AXL is a Soap based API that enables remote provisioning of Unified CM

 

## Authors

* **Javier Baltar** - *Initial work* - [GitHub](https://github.com/JavierBaltar)

## Licence
