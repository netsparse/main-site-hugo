---
layout: post
author: Angel
date: 2023-04-06T16:35:08-05:00
title: "Automate Your Infrastructure With Ansible"
tags: ["ansible", "automation", "IaC", "homelab", "linux"]
description:
showToc: true
TocOpen: false
hidemeta: false
comments: true
disableHLJS: false # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
draft: false
---

Automating your infrastructure with Ansible can be a game-changer for any organization looking to streamline their processes and reduce manual labor. 

[Ansible](https://www.ansible.com/) is an open-source automation tool that allows you to automate tasks such as configuration management, application deployment, and orchestration of infrastructure resources, using a declarative language to describe the desired state of a system.

One of the key benefits of Ansible is its simplicity and ease of use. 

Here's a quick overview from [Fireship.io](https://fireship.io/).

{{< ytlazy xRMPKQweySE >}}

## Components

### Inventory

An Ansible inventory file is a configuration file that contains a list of hosts and groups that Ansible can manage. The inventory file specifies the target hosts that Ansible should execute tasks against, and can be used to define host-specific variables and group-specific variables.

An inventory file is written in `INI` or `YAML` format, and can include the following information:

- Hostnames or IP addresses of target hosts
- Connection parameters such as the SSH username, SSH port, or WinRM settings
- Group definitions, which allow hosts to be grouped together and managed collectively
- Variables, which can be assigned to individual hosts or groups

For example, an inventory file might look like this:

```ini
[webservers]
web1.example.com
web2.example.com

[databases]
db1.example.com
db2.example.com

[all:vars]
ansible_user=ubuntu
```

### Playbooks

An Ansible playbook is a set of instructions that define the desired state of a system, and the steps required to achieve that state. 

Playbooks are also written in `YAML` format.

A typical playbook consists of one or more "plays", each of which specifies a set of tasks to be executed on a target host or group of hosts. 

Each task defines a set of actions to be performed, such as installing a package, editing a configuration file, or executing a command. 

Tasks are executed in a sequential order by utilizing the declarative syntax in `YAML` to determine the order of execution and the dependencies between tasks.

Playbooks can also include variables, which can be used to define reusable values or parameters that can be passed between tasks or plays. 

For example, here is a playbook which checks for updates on a remote Ubuntu host:

```yml
---
- name: Check for updates on Ubuntu
  hosts: 192.168.2.100
  become: true
  
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
    
    - name: Check for updates
      apt:
        upgrade: dist
        update_cache: yes
```

## Getting Started

### Windows
Ansible can be installed on Windows using Windows Subsystem for Linux (WSL) or a virtual machine (VM).

- If you don't already use WSL, follow the instructions on [Microsoft's website](https://docs.microsoft.com/en-us/windows/wsl/install-win10) on setting up a WSL machine.
- Install a Linux distribution such as Ubuntu or Debian from the Microsoft Store, or use [this guide]().
- Once you have your Linux machine up and running, run:

```
sudo apt update
sudo apt install ansible -y
```

### Mac OS

If you are using Mac OS, you can use [Homebrew](https://brew.sh/), a popular package manager for Mac OS. 

```
brew install ansible
```

### Ubuntu/Debian-based

If you are on Ubuntu, or any Debian-based system, you can use the `apt` package manager.

```
sudo apt update
sudo apt install ansible -y
```

Verify Ansible is installed and working:

```
ansible --version
```

```
ansible [core 2.11.4]
  config file = None
  configured module search path = ['/home/devops/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/share/lib64/python3.6/site-packages/ansible
  ansible collection location = /home/devops/.ansible/collections:/usr/share/ansible/collections
  executable location = /home/devops/.local/bin/ansible
  python version = 3.6.12 (default, Sep 15 2020, 12:49:50) [GCC 4.8.5 20150623 (Red Hat 4.8.5-37)]
  jinja version = 2.11.3
  libyaml = True
```

### SSH Keys

Make sure you have access to your hosts with ssh keys.

You can generate a key-pair with:

```
ssh-keygen
```

Then you can copy the keys to the control node with:

```
ssh-copy-id username@remote_host
```

If you need more information, check out this [short guide](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-20-04).

## Setup

### Inventory File

You can start by creating an **inventory file** that lists the IP addresses or hostnames of the machines you want to manage, keep in mind this can be done in both `INI` or `YAML` format. 

In this case, we'll create one in an `.ini` file. 

`inventory.ini`

```ini
[webservers]
192.168.2.100
192.168.2.101
```

### Playbook

Then create your `playbook` file to "describe" the desired state of your infrastructure. 

`playbook.yml`

```yml
---
- hosts: webservers
  become: true
  tasks:
    - name: Install Apache web server
      apt:
        name: apache2
        state: present

```

3. Run the playbook by using `ansible-playbook -i <inventory> <playbook>`.

```
ansible-playbook -i inventory.ini playbook.yml
```

This will run the playbook and configure the machines listed in the inventory file.

## Practical Uses

### Provisioning Multiple Servers

You can create a playbook that defines the desired configuration for any number of new servers defined in your `inventory` file, and run it to deploy them automatically without the need for manual configuration, which definitely saves you time, and reduces the likeliness of errors.

### Deploying Applications

Ansible can also be used to deploy applications automatically across a variety of hosts. 

#### Apache Example

For example, we can setup a simple Apache server to run on a given host in our inventory. This can further be extended if we need to run this on multiple hosts in our inventory file.

```yml
---
- name: quick-apache-1
  hosts: 192.168.2.100
  become: true

  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install Apache2 package
      apt:
        name: apache2
        state: present

    - name: Enable Apache2 service
      service:
        name: apache2
        enabled: yes
        state: started

    - name: Create index.html file
      copy:
        content: "Hello, world!"
        dest: /var/www/html/index.html
```

The above playbook should setup an Apache web server on host `192.168.2.100`.

Ansible will let us know when the playbook has been completed and report back a status update like below:

```
PLAY [quick-apache-1] ****************************************************************

TASK [Gathering Facts] ***************************************************************
ok: [192.168.2.100]

TASK [Update apt cache] ***************************************************************
changed: [192.168.2.100]

TASK [Install Apache2 package] ********************************************************
changed: [192.168.2.100]

TASK [Enable Apache2 service] *********************************************************
changed: [192.168.2.100]

TASK [Create index.html file] *********************************************************
changed: [192.168.2.100]

PLAY RECAP ****************************************************************************
192.168.2.100              : ok=5    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0     
```

### Managing Network Devices

Ansible can also be used to manage network devices, such as switches and routers. 

You can create a playbook that defines the desired configuration for your network devices. 

This makes it easy to manage your network infrastructure and ensures consistency across your devices.

#### Managing Edgerouter X Firewall Rules

For example, we can modify firewall rules and manage our Edgerouter X from a playbook file.

```yml
---
- name: Configure EdgeRouter X firewall
  hosts: 192.168.2.1
  gather_facts: no
  become: true
  
  vars:
    firewall_rules:
      - rule_number: 10
        action: accept
        protocol: tcp
        destination_port: 22
      - rule_number: 20
        action: accept
        protocol: tcp
        destination_port: 80
      - rule_number: 30
        action: accept
        protocol: tcp
        destination_port: 443
      - rule_number: 40
        action: drop
        protocol: all
        source: 192.168.2.0/24
        state: new

  tasks:
    - name: Add firewall rules
      edgemax_firewall:
        rule_number: "{{ item.rule_number }}"
        action: "{{ item.action }}"
        protocol: "{{ item.protocol }}"
        destination_port: "{{ item.destination_port }}"
        source: "{{ item.source | default(omit) }}"
        state: "{{ item.state | default(omit) }}"
      with_items: "{{ firewall_rules }}"
```

## Conclusion

In conclusion, automating your infrastructure with Ansible can save time, reduce errors, and make your life easier. 

You can easily provision new servers, deploy applications, and manage your network devices all from within a file.

## Learn More

If you wish to learn more, make sure to check out the [official documentation](https://docs.ansible.com/ansible/latest/getting_started/index.html), and the community's [self-paced lab training](https://www.ansible.com/products/ansible-community-training).