---
layout: post
author: Angel
date: 2023-03-23T23:41:00-05:00
title: "Quick Intro To Powershell"
tags: ["windows", "powershell", "scripting", "automation", "sysadmin"]
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

## Overview

PowerShell is a command-line scripting language developed by Microsoft that is designed to automate administrative tasks and manage system configurations. It provides a powerful framework for managing Windows-based systems and automating repetitive tasks.

They are written in the PowerShell scripting language, which is based on the .NET framework. The language includes features such as variables, loops, conditionals, and functions, which allow you to write scripts to perform a wide range of tasks.

In this guide, I'll guide you through the process of getting started with PowerShell, and provide some practical examples of how you can use it to perform some system administration tasks.

## Getting Started

To get started with PowerShell, you'll need to open the PowerShell console on your Windows machine. You can do this by clicking on the Start menu and typing "PowerShell" in the search bar.

Once you have opened the PowerShell console, you can start entering commands. PowerShell commands are called `cmdlets`, and they are structured in a verb-noun format. 

For example, to display a list of all the processes running on your machine, you would enter the following command:

```powershell
Get-Process
```

This will display a list of all the running processes, including their names, process IDs, and memory usage.

## Practical Examples

### Checking Disk Space

One of the most common tasks for system administrators is checking the disk space on their servers. PowerShell makes this task easy with the following cmdlet:

```powershell
Get-PSDrive | Where-Object {$_.Provider -like "*FileSystem"} | Format-Table Name, Used, Free, @{Name="Capacity";Expression={("{0:N2}" -f (($_.Used + $_.Free) / 1GB)) + " GB"}}
```

### Restarting a Service

If you need to restart a service on your machine, you can do so easily with PowerShell. 

For example, to restart the Windows Update service, you would enter the following command:

```powershell
Restart-Service -Name wuauserv
```

### Creating a User Account

You can also use PowerShell to create a new user account on your machine. The following command creates a new user account named `John` with the password `P@ssw0rd`:

```powershell
New-LocalUser -Name "John" -Password (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force)
```

### Removing Old Files

Finally, PowerShell can also be used to remove old files from your machine. The following command removes all files in the `C:\Temp` directory that are older than 30 days:

```powershell
Get-ChildItem "C:\Temp" -Recurse | Where-Object {$_.LastWriteTime -lt (Get-Date).AddDays(-30)} | Remove-Item -Force
```

### Moving Files by File Extension

This is a PowerShell script that moves files of a given file extension from a source directory to a destination directory on the OS. 

It prompts the user for input to set the source directory path, the destination directory path, and the file extension to filter files.

```powershell
$sourcePath = Read-Host "Enter the source directory path containing the files to be moved"
$destinationPath = Read-Host "Enter the destination directory path where the files will be moved"
$extension = Read-Host "Enter the file extension to filter files (e.g. *.txt)"

Get-ChildItem $sourcePath -Filter $extension |
ForEach-Object {
    $newPath = Join-Path $destinationPath $_.Name
    Move-Item $_.FullName $newPath -Force
}
```

### More Scripts

You can check out more scripts that have been developed by the community on [GitHub](https://github.com/fleschutz/PowerShell), and also some provided by Microsoft [here](https://learn.microsoft.com/en-us/powershell/scripting/samples/sample-scripts-for-administration?view=powershell-7.3).

## Conclusion

PowerShell is a valuable tool for system administrators, enabling them to automate tasks and streamline their Windows environment. 

With its powerful capabilities and user-friendly interface, PowerShell is an essential tool for any Windows-based IT environment.

## Learn More

- [Windows PowerShell Survival Guide](https://social.technet.microsoft.com/wiki/contents/articles/183.powershell-survival-guide.aspx)
- [MS introduction to PowerShell](https://learn.microsoft.com/en-us/training/modules/introduction-to-powershell/)
- [Guru99](https://www.guru99.com/powershell-tutorial.html)
- [Official PowerShell Documentation](https://learn.microsoft.com/en-us/powershell/)
- [Some good examples](https://www.spguides.com/powershell-examples/)


