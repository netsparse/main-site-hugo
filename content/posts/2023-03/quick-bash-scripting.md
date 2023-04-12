---
layout: post
author: Angel
date: 2023-03-21T20:46:08-05:00
title: "Quick Intro To Bash Scripting"
tags: ["linux", "bash", "scripting", "automation", "sysadmin"]
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

[Bash](https://www.gnu.org/software/bash/) scripting is a powerful tool that enables users to automate tasks and streamline workflows in Unix-based operating systems, such as Linux and macOS. 

It can be used for a variety of purposes, including system administration, web development, data analysis, and more. 

Here's a quick overview from [Fireship.io](https://fireship.io/).

{{< ytlazy I4EWvMFj37g >}}

## Components

### Commands

Consist of a series of commands that are executed one after the other. 

These commands can be standard Linux commands or custom commands written specifically for the script.

```bash
echo "Hello World"  # prints "Hello World" to the console
ls /home/user       # lists files in the user's home directory
touch new_file.txt  # creates a new empty file named "new_file.txt"
```

### Variables

Use variables to store and manipulate data. 

Variables can be assigned values, used in arithmetic and string operations, and passed as arguments to commands.

```bash
name="John"
echo "Hello $name"  # prints "Hello John" to the console
number=10
result=$((number + 5))
echo $result        # prints "15" to the console
```

### Control Structures

You can use control structures like if-else statements, loops, and functions to control the flow of execution. 

These structures allow scripts to make decisions, repeat tasks, and perform complex operations.

```bash
if [[ -d "/home/user" ]]; then
  echo "The /home/user directory exists"
else
  echo "The /home/user directory does not exist"
fi

for i in {1..5}; do
  echo $i
done

function say_hello() {
  echo "Hello"
}

say_hello
```

### Input and Output

Bash scripts can read input from various sources, including standard input, command-line arguments, and files. 

They can also write output to standard output, files, and other destinations.

```bash
read -p "What is your name? " name
echo "Hello $name"

cat file.txt      # prints the contents of file.txt to the console
echo "Hello" > file.txt  # writes "Hello" to file.txt
```

### Error Handling

Errors and exceptions using error codes, traps, and logging. 

They can also send email notifications and perform other actions in response to errors.

```bash
command_that_might_fail || echo "An error occurred"

trap 'echo "An error occurred"; exit 1' ERR

echo "Starting script"
some_command || exit 1
echo "Script completed successfully"
```

### Regular Expressions (RegEx)

You can use regular expressions to perform pattern matching and text manipulation. 

Regular expressions are a powerful tool for searching and replacing text within a script.

You can check out [RegExr](https://regexr.com/) to learn more about how they work.

```bash
# Extracting email addresses from a file
cat file.txt | grep -oE '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}' 

# Extracting phone numbers from a string
text="My phone number is 123-456-7890"
echo $text | grep -oE '[0-9]{3}-[0-9]{3}-[0-9]{4}'

# Replacing all occurrences of a string in multiple files
find . -type f -name '*.txt' -exec sed -i 's/old_string/new_string/g' {} +

# Extracting all URLs from an HTML file
cat index.html | grep -oE 'https?://[^ ]+' 

# Replacing all occurrences of 'foo' with 'bar' in a string
text="The quick brown foo jumps over the lazy dog"
echo ${text/foo/bar}
```

### Functions

Define functions to encapsulate and reuse code. 

Functions can take arguments, return values, and be used to perform complex tasks.

```bash
# A function that returns the sum of two numbers
function add_numbers() {
  local result=$(( $1 + $2 ))
  echo $result
}

# A function that prints a message
function say_hello() {
  echo "Hello, world!"
}

# Using the functions
sum=$(add_numbers 5 7)
echo "The sum is: $sum"

say_hello
```

## Get Started

## For Basic Systems Administration

In this post, we'll explore some of use cases for bash scripting and provide some examples that could be of use for you and your environment.

### Performing Updates

We know updates are definitely important, so why not automate them in some way.

Create a `auto-updates.sh` script and add the following:

```bash
#!/bin/bash
sudo apt-get update
sudo apt-get upgrade -y
```

### Make Executable

```bash
chmod +x /path/to/auto-updates.sh
```

You can also add this script to the [crontab](/posts/2023-03/quick-bash-scripting/#adding-items-to-the-cron) to automate your updates for your system.

### Renaming Files

Renaming files can be a tedious and time-consuming task, especially when you have a large number of files to rename. 

We could make it easier for ourselves by creating a script to automate this for us.

The basic command to rename files in Bash is `mv`. 

To rename a file named `old_name.txt` to `new_name.txt`, you can use the `mv` command as below:

```
mv old_name.txt new_name.txt
```

#### Renaming Multiple Files

If you want to rename multiple files at once, you can use a Bash script to automate the process. 

Here is an example of how to rename all files in a directory with the `.txt` extension:

```bash
#!/bin/bash
for file in *.txt
do
  mv "$file" "new_${file}"
done
```

This script will add the prefix `new_` to the beginning of each file name with the `.txt` extension.

### Moving Files

Moving files is another task that can be automated with Bash scripting. 

The `mv` command can also be used to move files from one directory to another. 

Here is an example of how to move a file named `file.txt` from the current directory to the directory `/home/user/documents/`:

```
mv file.txt /home/user/documents/
```

This command will move the file `file.txt` to the directory `/home/user/documents/`.

#### Moving Multiple Files

To move multiple files at once, you can use a Bash script. 

Here is an example of how to move all files in a directory with the `.txt` extension to a new directory:

```bash
#!/bin/bash
mkdir /home/user/documents/txt_files
for file in *.txt
do
  mv "$file" /home/user/documents/txt_files/
done
```

### Performing Backups

```bash
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

This should perform a backup with `tar` of the `/etc`, `/home`, and `boot` directories to the `specified directory` (in this case`/backup`). Which could then be transferred to another machine once the backup is finished.

## Other Use Cases

### Web Development

Bash scripts are also useful for web developers who need to automate repetitive tasks such as deploying code, running tests, and building websites. 

For example, a web developer can use a bash script to automate the process of deploying code to a production server.

```bash
#!/bin/bash
git pull
npm install
npm run build
rsync -avz --exclude=node_modules /path/to/local/code/ user@server:/path/to/production/code/
```

### Data Analysis

Bash scripting is also useful for parsing fairly large amounts of data, and automating tasks such as data cleaning, data transformation, and data visualization. 

For example, you can use a bash script to clean a large CSV file and generate a summary report. 

The script can contain commands that remove duplicates, filter rows, and aggregate data.

You'll need the `csvkit` package which can be installed with `apt install`.

```bash
#!/bin/bash
csvclean input.csv | csvstat > report.txt
```

### Docker

#### Quickly Install Docker

```bash
#!/bin/bash

# Install Docker
sudo apt-get update
sudo apt-get install -y docker.io

# Start Docker daemon
sudo systemctl start docker

# Download and run "hello-world" container
sudo docker run hello-world
```

## Cron

`cron` is a utility program that allows users to schedule commands or scripts to run automatically at specified intervals in Linux-based operating systems. 

The name "cron" comes from the Greek word "chronos", which means "time". The cron daemon is a background process that runs continuously and checks the crontab files for any scheduled jobs to run.

### Adding Items to the Cron

```bash
crontab -e
```

If this is the first time you're editing your crontab file, the system may ask you to choose an editor.

In the editor, add a new line for each command or script you want to schedule. The format of the line is as follows:

```bash
* * * * * command-to-be-executed
```

The asterisks represent the timing specification for the command, which defines when it should be executed. 

For example, if you want a command to run every day at midnight, you would use the following line:

```bash
0 0 * * * command-to-be-executed
```

The cron daemon will automatically read the updated crontab file and start executing the scheduled commands at the specified intervals. 

You can verify that your new items have been added to your crontab file by typing the following command:

```bash
crontab -l
```

Check out this [helpful tool](https://crontab.guru/) for editing your cron schedule expressions.


### Add Scripts to Cron

```bash
* * * * * /path/to/script.sh
```

If you want to redirect `stdout` and errors to a file, you can modify the cron command like this:

```
0 0 * * * /path/to/script.sh >> /path/to/output.log 2>&1
```

### Automating Backups

You can utilize scripts and `cron` to perform backups, send them off to a remote server, and send a notification when they are done.

Example:

```bash
#!/bin/bash

# Backup directory path
local_backup_dir="$HOME/backups"

# Remote server IP address
remote_user="example"
remote_server="192.168.2.200"
remote_backup_dir="/backups"

# Email address for notifications
notification_email="alerts@example.com"

# Create a backup with tar in local dir, send it to a remote server, and send a notification when done
mkdir -p "$local_backup_dir"
backup_path="$local_backup_dir/$(date +%Y-%m-%d)"
tar -czvf "$backup_path.tar.gz" -C "$HOME" "$(basename $local_backup_dir)"
if [ $? -eq 0 ]; then
    echo "Backup succeeded."
else
    echo "Backup failed."
    exit 1
fi

rsync -avz --delete "$backup_path.tar.gz" "$remote_user@$remote_server:$remote_backup_dir"
if [ $? -eq 0 ]; then
    echo "Transfer succeeded."
else
    echo "Transfer failed."
    exit 1
fi

echo "Backup completed on $(date)." | mail -s "Backup completed" "$notification_email"

# Define a cronjob that runs this backup every 3 days at 10pm
(crontab -l ; echo "0 22 */3 * * /bin/bash /path/to/script.sh") | crontab -
```

### Snapshots with Timeshift

[Timeshift](https://github.com/linuxmint/timeshift) is a free and open-source backup/restore utility for Linux systems. 

It creates snapshots of the file system, allowing users to restore their system to a previous state if needed. Timeshift can be run manually or scheduled to run automatically using cron. 

Snapshots can be stored locally or remotely, and users can choose the number of snapshots to keep and the frequency of snapshots.

You can create a bash script for defining how you would like timeshift to run, make sure to include `sudo` when running:

```bash
#!/bin/bash

# Set the snapshot directory
snapshot_dir="/run/timeshift/<drive>/backup"

# Set the maximum number of snapshots to keep
max_snapshots=10

# Set the backup level (can be "system" or "home")
backup_level="system"

# Create a new snapshot with Timeshift
timeshift --snapshot --create --comments "Automated snapshot on $(date +%Y-%m-%d)" --backup-device "$backup_level"
```

You can then add this entry to your crontab to have cron run it every 3 days at 1am, or after your backups are done.

```bash
0 1 */3 * * /home/user/scripts/timeshift-auto.sh
```

If you would like to simply add it to `cron` manually, you can simply add the following:

Make sure to specify the `<drive>` under `--backup-device`.

```bash
0 1 */3 * * /usr/bin/timeshift --snapshot --create --comments "Automated snapshot on $(date +\%Y-\%m-\%d)" --backup-device "/run/timeshift/<drive>/backup" --scripted
```

## Learn More

Make sure to check out the [official Bash manual](https://www.gnu.org/software/bash/manual/) and other awesome guides like The Linux Documentation Project's [Beginner](http://www.tldp.org/LDP/Bash-Beginners-Guide/html/) and [Advanced Bash Scripting Guide](http://www.tldp.org/LDP/abs/html/), GreyCat's [BashGuide](https://mywiki.wooledge.org/BashGuide), and [commandlinefu](https://www.commandlinefu.com/commands/browse).

## Conclusion

Although Bash is useful for automating tasks on a single host, if you wish to replicate this and multiply it across a multitude of hosts, you should take a look at my other [Ansible post](/posts/2023-02/automate-your-infrastructure-with-ansible), where we take this to another level.

In conclusion, bash scripting is a powerful tool that enables users to automate tasks and streamline workflows in Unix-based operating systems. 

By writing scripts, you can save time, reduce errors, and improve productivity.

### Learn More
- [Official GNU Bash Manual](https://www.gnu.org/software/bash/manual/bash.pdf)
- [learnshell.org](https://www.learnshell.org/)
- [BashGuide](https://mywiki.wooledge.org/BashGuide)
- [TLDP](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
- [MrTutorize YouTube Series](https://www.youtube.com/playlist?list=PL18DF64CBBAEAAE77)
- [Code Academy](https://www.codecademy.com/learn/learn-the-command-line)
- [Devhints.io Cheat Sheet](https://devhints.io/bash)
- [BashHackers](https://wiki.bash-hackers.org/)

### Tools
- [Shellcheck](https://www.shellcheck.net/)