---
layout: post
author: Angel
date: 2023-03-28T14:00:38-05:00
title: "Quick Data Backup Guide"
tags: ["backups", "guide", "recovery"]
showToc: true
TocOpen: false
hidemeta: false
comments: true
#canonicalURL: "https://canonical.url/to/page"
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

Data is arguably one of the most important assets in our modern world. We use computers, smartphones, and other devices to store and access our personal and professional information. 

However, these devices are not immune to failures or accidents. In the event of a hard drive crash, theft, or other catastrophic event, having a backup of your data is critical. 

We will discuss the importance of backups, the 3-2-1 method, and how to backup your Linux, Windows, and Mac machines so that you can rest assured that your data is safe.

## Why Backups Are Important

We've all heard the horror stories of data being deleted or being lost by ransomware. When it comes to preparing for potential data loss or corruption, there are a couple key strategies one could use that could minimize the impact of being severely affected.

Backups provide a way to protect your data against any potential for loss in the future.

## Methods / Strategies

### 3-2-1 Backup Method

The 3-2-1 backup method is a simple but effective strategy for protecting your data. It involves creating three copies of your data, storing it in two different formats, and keeping one copy off-site. Here is how it works:

- **Three copies of your data**: This means that you have three copies of your data in case one or two copies become inaccessible or corrupted.
- **Two different storage types**: This means that you store your data in two different types of storage media, such as a hard drive and a cloud-based storage service. This protects against the risk of both storage types failing at the same time.
- **One copy stored offsite**: This means that you store one copy of your data in an offsite location, such as a cloud-based storage service or a physical location away from your primary storage site. This protects against the risk of data loss due to a physical disaster or theft.

### Incremental Backups

This backup method only backs up changes made since the last backup. This means that it takes less time and storage space than a full backup.

### Differential Backups

This backup method backs up all changes made since the last full backup. This means that it takes more time and storage space than an incremental backup but less than a full backup.

### Continuous Data Protection Method

This backup method automatically backs up changes in real-time, ensuring that the most up-to-date data is always backed up.

### Cloud Backups

This backup method stores your data on a remote server over the internet, providing an offsite backup solution that can be accessed from anywhere.

### Local Backups

This backup method involves backing up your data to a local storage device such as an external hard drive or USB drive.

It's important to note that each backup method has its own strengths and weaknesses, so it's essential to choose a backup method that suits your specific needs and circumstances.

## Basic Backup Guide For Your Machines

### How to Backup Your Windows Machine

Windows is the most popular operating system used by consumers and businesses. Here are the steps to backup your Windows machine:

1. Connect an external hard drive to your Windows machine.
2. Click on the Start menu and type "backup and restore" in the search box.
3. Click on "Backup and Restore (Windows 7)" and then click on "Set up backup."
4. Follow the prompts to select the files and folders you want to backup and choose your external hard drive as the backup destination.
5. Click on "Save settings and run backup" to start the backup process.

### How to Backup Your Mac Machine

Mac OS is a popular operating system used by many creative professionals. Here are the steps to backup your Mac machine:

1. Connect an external hard drive to your Mac machine.
2. Click on the Apple menu and select "System Preferences."
3. Click on "Time Machine."
4. Click on "Select Backup Disk" and choose your external hard drive as the backup destination.
5. Click on "Back Up Now" to start the backup process.

### How to Backup Your Linux Machine

Linux is a popular operating system used by many servers and developers.

Here are some steps you can take to backup your Linux machine:

1. Connect an external hard drive to your Linux machine.
2. Open a terminal window and type the following command to create a backup of your entire system: 

```bash
sudo tar cvpzf /backup.tar.gz --exclude=/backup.tar.gz --exclude=/proc --exclude=/tmp --exclude=/mnt --exclude=/dev --exclude=/sys /
```

3. Wait for the backup process to complete.
4. Copy the backup file to your external hard drive.

You could also utilize a bash script if you wish, as mentioned in one of my [previous articles](/posts/2023-03/quick-bash-scripting/#performing-backups).

```
#!/bin/bash

backup_dirs=("/etc" "/home" "/boot")
dest_dir="/backup"
backup_date=$(date +%b-%d-%y)

echo "Starting backup of: ${backup_dirs[@]}"

for i in "${backup_dirs[@]}"; do
    sudo tar -Pczf /tmp/$i-$backup_date.tar.gz $i
    if [ $? -eq 0 ]; then
        echo "$i backup succeeded."
    else
        echo "$i backup failed."
    fi
done

sudo mkdir -p $dest_dir
sudo mv /tmp/*.gz $dest_dir

echo "Backup is done."
```

## Scheduling

Make sure you have a backup schedule and keep your backup copies in a safe and secure location.

## Testing Your Backups

In addition to backing up your data, it's also important to test your backups regularly. This ensures that you can recover your data in case of a disaster. You can do this by restoring your backups to a different machine or location and checking if all the files are present and accessible. For a more realistic scenario, you could also simulate data loss and go through the process of recovering your data from there.

## My Strategies for my Lab

As of the writing of this post, I would say my current strategy is not a one size fits all approach, I try and mix some of these strategies together, but otherwise, you may do whatever works best for your environment.

#### Monitoring

I usually keep an eye for any SMART failures on my NAS's RAID 1, I have alerts enabled through my NAS which alert me if SMART detects any potential failures with any of the drives. 

#### Synology Hyper Backup

I keep incremental backups of some of the basic files from my SMB and NFS shares with Synology's Hyper-Backup, and also utilize a cloud backup with [Sync]() and [pCloud]() as my providers.

#### Encryption

My uploaded backups are encrypted with [Cryptomator]() and I only backup the most important data to the cloud, such as financial documents, identity documents, personal media like pictures or videos, notes, and other small sized data. 

#### Large Media

For all other large media, I try and take the 3-2-1 approach, but not fully. I have (1x) 12 TB external HDD, and (1x) 14 TB external HDD which keep an incremental and encrypted backup of all my other data.

#### Multi Location

Some drives are stored at my residence, I also have (1x) 2 TB drive with a copy of my encrypted cloud uploads that are updated every 3-6 months at another location that is not my residence.

Although my approach is not perfect, I am constantly working my way towards adopting more of the best practices.

## Conclusion

In conclusion, backups are essential for protecting your data against loss. By following any of the above backup methods and regularly backing up your data, you can definitely make a difference, and ensure that your important files are safe and recoverable in case of a disaster. 

So, don't wait until it's too late, start backing up your data today.

### Learn More

- [3-2-1 Strategy from Backblaze](https://www.backblaze.com/blog/the-3-2-1-backup-strategy/)
- [r/Datahoarder's Backups Wiki](https://www.reddit.com/r/DataHoarder/wiki/backups/)
- [List of Backup Software](https://en.wikipedia.org/wiki/List_of_backup_software)
