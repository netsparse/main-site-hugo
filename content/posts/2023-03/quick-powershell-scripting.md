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

[PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.3) is a command-line scripting language developed by Microsoft that is designed to automate administrative tasks and manage system configurations. It provides a powerful framework for managing Windows-based systems and automating repetitive tasks.

Scripts are written in the [PowerShell scripting language](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.3), which is based on the [.NET framework](https://dotnet.microsoft.com/en-us/). 

The language includes features such as variables, loops, conditionals, and functions, which allow you to write scripts to perform a wide range of tasks.

In this guide, I'll guide you through the process of getting started with PowerShell, and provide some practical examples of how you can use it to perform some common tasks.

## Getting Started

Click on the `Start` menu and type "PowerShell" in the search bar.

or

Press `Win`+`X`, you may see underlines under the options. Press `I`, PowerShell will open.

`Win`+`X` `A` for an elevated prompt

Once you have opened the PowerShell console, you can start entering commands. 

PowerShell commands are called `cmdlets`, and they are structured in a verb-noun format. 

### Check PS Version

To verify which version of PowerShell you are running, run:

```powershell
$PSVersionTable
```

### List Running Processes

For example, to display a list of all the processes running on your machine, you would enter the following command:

```powershell
Get-Process
```

This will display a list of all the running processes, including their names, process IDs, and memory usage.


### Execution Policy

The execution policy is designed to prevent a user from unknowingly running a script. Although not a security boundary, it prevents accidental launching of scripts.

```powershell
Get-ExecutionPolicy
```

PowerShell scripts can't be run at all when the execution policy is set to `Restricted`. This is the default setting on all Windows client operating systems.

If you need to set the execution policy, run `Set-ExecutionPolicy` with the recommended `RemoteSigned` policy.

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
```

## Quick Practical Examples

### Checking Disk Space

```powershell
Get-PSDrive | Where-Object {$_.Provider -like "*FileSystem"} | Format-Table Name, Used, Free, @{Name="Capacity";Expression={("{0:N2}" -f (($_.Used + $_.Free) / 1GB)) + " GB"}}
```

### Restarting a Service

For example, to restart the Windows Update service, you would enter the following command:

```powershell
Restart-Service -Name wuauserv
```

### Creating a User Account

The following command creates a new user account named `John` with the password `P@ssw0rd`:

```powershell
New-LocalUser -Name "John" -Password (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force)
```

### Removing Old Files

The following command removes all files in the `C:\Temp` directory that are older than 30 days:

```powershell
Get-ChildItem "C:\Temp" -Recurse | Where-Object {$_.LastWriteTime -lt (Get-Date).AddDays(-30)} | Remove-Item -Force
```

### Moving Files by File Extension

This is a PowerShell script that moves files of a given file extension from a source directory to a destination directory on the OS all while promting for user input. 

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

## Conclusion

PowerShell is a valuable tool for system administrators, enabling them to automate tasks and streamline their Windows environment. 

With its powerful capabilities and user-friendly interface, it is an essential tool for any Windows-based IT environment.

## Learn More

- [Windows PowerShell Survival Guide](https://social.technet.microsoft.com/wiki/contents/articles/183.powershell-survival-guide.aspx)
- [MS introduction to PowerShell](https://learn.microsoft.com/en-us/training/modules/introduction-to-powershell/)
- [Guru99](https://www.guru99.com/powershell-tutorial.html)
- [Official PowerShell Documentation](https://learn.microsoft.com/en-us/powershell/)
- [PowerShell Overview](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.3)
- [Some good examples](https://www.spguides.com/powershell-examples/)

## Resources & More Scripts

- [Powershell Gallery](https://www.powershellgallery.com/)
- [PDQ Powershell Scanners](https://github.com/pdqcom/PowerShell-Scanners)
- [Community GitHub Collection](https://github.com/fleschutz/PowerShell)
- [Microsoft](https://learn.microsoft.com/en-us/powershell/scripting/samples/sample-scripts-for-administration?view=powershell-7.3)
- More to come...
