---
layout: post
author: Angel
date: 2023-02-07T20:49:05-05:00
title: "Setup a VM Server with Proxmox VE"
tags: ["virtualization", "proxmox", "lxc", "linux", "homelab", "containers"]
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

[Proxmox](https://www.proxmox.com/en/) is a powerful, open-source virtualization management platform that allows you to create and manage virtual machines (VMs) and containers on a single server. It is a popular choice for home labbing, where enthusiasts use it to create and test different configurations of operating systems, applications, and network setups.

In this article, I'll guide you through the steps required to set up a Proxmox server for home labbing.

## Requirements

- A 64-bit CPU with Intel VT/AMD-V virtualization support
- At least 4GB of RAM (8GB or more is recommended)
- At least 16GB of storage space for the operating system and Proxmox installation
- At least one Ethernet port for network connectivity

## Setup

### Download and Install Proxmox

Head over to the [Downloads](https://www.proxmox.com/en/downloads/category/iso-images-pve) section on Proxmox's site and download the installation ISO.

Once you've downloaded the ISO file, create a bootable USB drive using a tool like [Rufus](https://rufus.ie/) or [Etcher](https://www.balena.io/etcher).

Next, boot your server from the installation media and follow the prompts to install Proxmox. 

You'll need to configure network settings, disk partitioning, and user accounts during the installation process.

### Web Interface

After installing Proxmox, you should be able to access the Proxmox web interface by navigating to `https://<your-server's-IP-address>:8006` in your web browser. 

Log in with the `root` username and the password you created during the installation process.

Click on the "Datacenter" node in the left sidebar, you should now be able to see an overview of your node. 

![img](https://static.packt-cdn.com/products/9781788397605/graphics/3b7849f5-30af-4046-8d72-34dc6c9040d2.png)

## Workflow

### Create Virtual Machines and Containers

To create a virtual machine, click on the `Create VM` button in the Proxmox web interface.

![img](https://www.linuxbabe.com/wp-content/uploads/2020/08/proxmox-create-vm.png)

You'll need to provide details about the virtual machine, including the operating system, disk size, and memory allocation. 

![img](https://nguvu.org/images/160716-001-create-vm.png)

You can also configure network settings and attach ISO images or virtual disks to the virtual machine.

Similarly, to create a container, click on the `Create CT` button in the Proxmox web interface. 

[Linux containers (LXC)](https://linuxcontainers.org/) are lightweight and use fewer resources than virtual machines. Proxmox utilizes LXC for container management.

### Manage Virtual Machines and Containers

From the web interface, you can start, stop, and delete virtual machines and containers, as well as view their resource usage and network statistics.

### Backups

You can also [create backups](https://pve.proxmox.com/wiki/Backup_and_Restore) of your virtual machines and containers, either manually or automatically. Backups are always full backups - containing the VM/CT configuration and all data. 

Backups can be started via the GUI or via the `vzdump` command line tool.

#### CLI Examples:

Simply dump guest 777 - no snapshot, just archive the guest private area and configuration files to the default dump directory (usually /var/lib/vz/dump/).

```
vzdump 777
```

Use rsync and suspend/resume to create a snapshot (minimal downtime).

```
vzdump 777 --mode suspend
```

Backup all guest systems and send notification mails to root and admin.

```
vzdump --all --mode suspend --mailto root --mailto admin
```

Use snapshot mode (no downtime) and non-default dump directory.

```
vzdump 777 --dumpdir /mnt/backup --mode snapshot
```

Backup more than one guest (selectively)

```
vzdump 101 102 103 --mailto root
```

Backup all guests excluding 101 and 102

```
vzdump --mode suspend --exclude 101,102
```

Restore a container to a new CT 600

```
pct restore 600 /mnt/backup/vzdump-lxc-777.tar
```

Restore a QemuServer VM to VM 601

```
qmrestore /mnt/backup/vzdump-qemu-888.vma 601
```

Clone an existing container 101 to a new container 300 with a 4GB root file system, using pipes

```
vzdump 101 --stdout | pct restore --rootfs 4 300 -
```

## Remove Subscription Notice

To get rid of the message, open a shell under the root user and type in the snippet below.

```bash
sed -Ezi.bak "s/(Ext.Msg.show\(\{\s+title: gettext\('No valid sub)/void\(\{ \/\/\1/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service
```

## Similar VM Platforms and Software

### [VMWare ESXi](https://www.vmware.com/products/esxi-and-esx.html)
An enterprise-class, type-1 hypervisor developed by VMware for deploying and serving virtual machines.

### [KVM (Kernel-based Virtual Machine)](https://www.linux-kvm.org/page/Main_Page)

KVM is a popular open-source virtualization solution for Linux that provides a type 1 hypervisor and supports running multiple virtual machines on a single physical server. 

It is currently the underlying platform that powers Proxmox's virtual machine functionality.

### [QEMU (Quick EMUlator)](https://www.qemu.org/)

A generic and open source machine emulator and virtualizer.

It can also leverage KVM to run VMs at near native speed.

### [Microsoft Hyper-V](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/)

Hyper-V is a type 1 hypervisor that is included with the Windows Server operating system.

### [Oracle VirtualBox](https://www.virtualbox.org/)

VirtualBox is a popular open-source virtualization solution that can run on a variety of operating systems, including Windows, Linux, and MacOS.

### [Citrix Hypervisor (formely XenServer)](https://docs.citrix.com/en-us/citrix-hypervisor/8-2.html)

Citrix Hypervisor is a type 1 hypervisor that provides similar virtualization capabilities and is designed for enterprise use.

### [VMware Workstation](https://www.vmware.com/products/workstation-pro.html)

VMware Workstation is a type 2 hypervisor that runs on top of an existing operating system.

Each of these virtualization platforms have their own strengths and weaknesses, the best choice will depend on the specific needs of the user or organization.

## Conclusion

Setting up a Proxmox server for home labbing is a great way to experiment with different configurations of operating systems, applications, and network setups. 

With Proxmox, you can create and manage virtual machines and containers on a single server, without the need for additional hardware.

## Learn More

- [Official Docs & Manuals](https://pve.proxmox.com/pve-docs/)
- [Proxmox Getting Started Guide](https://www.proxmox.com/en/proxmox-ve/get-started)
- [Proxmox Tutorial](https://forum.proxmox.com/threads/proxmox-beginner-tutorial-how-to-set-up-your-first-virtual-machine-on-a-secondary-hard-disk.59559/)
- [Phoenixnap](https://phoenixnap.com/kb/install-proxmox)