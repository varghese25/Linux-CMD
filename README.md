Linux
Logs & Monitoring
System Monitoring Commands
varghese@DESKTOP-OODIU93:~/Data$ top
top - 13:42:11 up 12 min,  0 users,  load average: 0.13, 0.63, 0.61
Tasks:  40 total,   1 running,  39 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.4 us,  0.5 sy,  0.0 ni, 98.9 id,  0.0 wa,  0.0 hi,  0.2 si,  0.0 st
MiB Mem :   3881.2 total,   2825.8 free,    418.2 used,    637.3 buff/cache
MiB Swap:   1024.0 total,   1024.0 free,      0.0 used.   3314.1 avail Mem
varghese@DESKTOP-OODIU93:~/Data$ free -m
               total        used        free      shared  buff/cache   available
Mem:            3881         418        2825          14         637        3314
Swap:           1024           0        1024
varghese@DESKTOP-OODIU93:~/Data$ vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 0  2      0 2825464 108436 595640    0    0   147    10  106  125  1  1 74 24  0
varghese@DESKTOP-OODIU93:~/Data$ iostat
Linux 6.6.87.2-microsoft-standard-WSL2 (DESKTOP-OODIU93)  03/14/26  _x86_64_  (4 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           0.91    0.00    1.14   20.60    0.00   77.34

Device             tps    kB_read/s    kB_wrtn/s    kB_dscd/s
sda               1.18        77.30         0.00         0.00
sdb               0.16        11.53         0.00         0.00
sdc               0.11         2.97         0.00         0.00
sdd              25.52       381.53        32.45        21.93
Log Files in Linux

Most system and application logs are stored in the /var/log directory.

varghese@DESKTOP-OODIU93:~/Data$ cd /var
varghese@DESKTOP-OODIU93:/var$ ls -lrt

Important directories inside /var:

/var/log
/var/cache
/var/tmp
/var/backups
/var/www
Log Directory
varghese@DESKTOP-OODIU93:/var$ cd log
varghese@DESKTOP-OODIU93:/var/log$ ls

Example log files:

alternatives.log
auth.log
dmesg
dpkg.log
kern.log
syslog
apache2/
journal/
Important Log Files
1. dmesg (Kernel Messages)

Shows kernel boot messages and hardware events.

varghese@DESKTOP-OODIU93:/var/log$ cat dmesg

Example:

[    0.000000] kernel: Linux version 6.6.87.2-microsoft-standard-WSL2
[    0.000000] kernel: Command line: initrd=\initrd.img WSL_ROOT_INIT=1

Used for:

Hardware detection

Kernel boot messages

Driver issues

System startup troubleshooting

2. syslog (System Logs)

Shows system activities and background services like cron jobs.

varghese@DESKTOP-OODIU93:/var/log$ cat syslog

Example:

Mar 8 17:49:59 DESKTOP-OODIU93 systemd[1]: rsyslog.service: Sent signal SIGHUP

Used for:

System events

Service logs

Scheduled jobs

Error tracking

Apache Logs

Apache web server logs are stored in:

/var/log/apache2/
varghese@DESKTOP-OODIU93:/var/log$ cd apache2/
varghese@DESKTOP-OODIU93:/var/log/apache2$ ls

Example:

access.log
error.log
error.log.1
other_vhosts_access.log
access.log

Records all client requests to the web server.

error.log

Stores Apache server errors and warnings.

Summary

Important monitoring commands:

Command	Purpose
top	Real-time CPU and process monitoring
free -m	Memory usage
vmstat	System performance statistics
iostat	Disk I/O statistics

Important log files:

Log File	Purpose
dmesg	Kernel and hardware events
syslog	System and service logs
auth.log	Authentication logs
kern.log	Kernel logs
apache2/*	Apache web server logs

Note:
dmesg and syslog are both very important for Logs & Monitoring, especially for troubleshooting system issues and tracking events.

# Corn Job Scheduler (Sample)

- Corn Format in Linux Cmd_IMG & Below both are same

* * * * * command-to-execute
- - - - -

| | | | |
| | | | +---- Day of the Week (0 - 7, where both 0 and 7 are Sunday)
| | | +------ Month (1 - 12)
| | +-------- Day of the Month (1 - 31)
| +---------- Hour (0 - 23)
+------------ Minute (0 - 59)

Guide: Automating a Script with CronStep 1: Create the Shell ScriptCreate a file named script.sh in your home directory. This script contains the actual task you want to perform.File: /home/varghese/script.shBash#!/bin/bash

# This line appends the current date and time to a log file
echo "Test $(date)" >> /home/varghese/test_log.txt
Note: Ensure the script is executable by running: chmod +x /home/varghese/script.shStep 2: Configure the Cron TableOpen your user's crontab configuration to schedule the task.Command:Bashcrontab -e
Inside the editor (GNU nano):Scroll to the very bottom and add the following line. This tells the system to run your script every minute (* * * * *).Plaintext# m h  dom mon dow   command
* * * * * /bin/bash /home/varghese/script.sh
Press Ctrl + O, Enter to save, and Ctrl + X to exit.Step 3: Verify the OutputWait at least 60 seconds for the first cycle to trigger. Then, check the log file to see if the script is running automatically.Command:Bashcat /home/varghese/test_log.txt
Expected Output:PlaintextTest Tue Mar 10 13:00:01 EDT 2026
Test Tue Mar 10 13:01:01 EDT 2026
Test Tue Mar 10 13:02:01 EDT 2026
Summary of Key CommandsActionCommandEdit Cron Jobscrontab -eList Active Jobscrontab -lMake Script Executablechmod +x script.shCheck Script Manually./script.sh



1️⃣ Apache Service Management

You successfully installed and managed Apache HTTP Server. Below is a clean summary of the commands you used.

Check Apache Status
sudo systemctl status apache2

Output shows:

Active: running

Apache processes running (/usr/sbin/apache2 -k start)

This confirms the web server is working.

Start Apache
sudo systemctl start apache2

Starts the Apache service.

Stop Apache
sudo systemctl stop apache2

Stops the Apache web server.

Restart Apache
sudo systemctl restart apache2

Restarts Apache after configuration changes.

Enable Apache at Boot
sudo systemctl enable apache2

Automatically starts Apache when the system boots.

Disable Apache at Boot
sudo systemctl disable apache2

Prevents Apache from starting automatically.

Access Apache in Browser

Open:

http://localhost

or

http://127.0.0.1

Default web directory in Ubuntu:

/var/www/html
2️⃣ Storage Management & Disk Information
Check Disk Usage
df -h

Example output:

Filesystem	Size	Used	Available	Use%	Mounted
/dev/sdd	1TB	4GB	952GB	1%	/

-h = human readable format.

Show Block Devices
lsblk

Output explanation:

Device	Type	Size	Mount
sda	disk	388.6M	system
sdb	disk	186M	system
sdc	swap	1G	swap
sdd	disk	1TB	main filesystem
Install Disk Partition Tool
sudo apt install fdisk

Installs the fdisk utility.

View Disk Partitions
sudo fdisk -l

Shows:

Disk size

Sector size

Partition layout

Example:

Disk	Size	Sectors
/dev/sdd	1TB	2147483648
3️⃣ Important Notes

You are running Ubuntu inside Windows Subsystem for Linux.

Because of this:

Apache runs inside Linux

Browser runs in Windows

So access Apache using:

http://localhost

from the Windows browser.






Linux Commands Notes
1. File Permissions
Change File Permission
chmod u=rwx,g=rwx,o=r script1.sh

Check permissions:

ls -l script1.sh

Output:

-rwxrwxr-- 1 varghese varghese 17 Mar 3 12:36 script1.sh
Permission Meaning
-rwxrwxr--
Symbol	Meaning
-	File
d	Directory
r	Read
w	Write
x	Execute
2. Directory Permissions

Check directory permissions:

ls -lrtd testing/

Output:

drwxr-xr-x 2 varghese varghese 4096 Mar 7 12:16 testing/

Explanation:

d -> directory
r -> read
w -> write
x -> execute (enter directory)

If x permission exists, users can enter the directory.

Restrict Other Users
chmod 774 testing/

Check permission:

ls -lrtd testing/

Output:

drwxrwxr-- 2 varghese varghese 4096 Mar 7 12:16 testing/
Folder Permission Read & Execute
chmod 775 testing/

Output:

drwxrwxr-x 2 varghese varghese 4096 Mar 7 12:16 testing/

Meaning:

Owner → Read, Write, Execute

Group → Read, Write, Execute

Others → Read, Execute

Full Permission
chmod 777 testing/

Output:

drwxrwxrwx 2 varghese varghese 4096 Mar 7 12:16 testing/

Meaning: Everyone has Full Access

3. Change Ownership

Change owner from varghese → tiju

sudo chown tiju:tiju testing

Check:

ls -lrtd testing/

Output:

drwxrwxrwx 2 tiju tiju 4096 Mar 7 12:16 testing/
Package Management
Package Formats
Format	Description
.deb	Debian package
.rpm	RedHat Package Manager
Install Package Using dpkg
sudo dpkg -i package.deb
apt Package Manager

Similar to Play Store for Linux.

Install multiple packages:

sudo apt install docker.io ansible curl wget
List Installed Packages
sudo dpkg -l

Example Output:

ii  adduser              3.118ubuntu5
ii  adwaita-icon-theme   41.0-1ubuntu1

ii means package is installed

Search Package

Example: Search Docker

sudo apt-cache search docker
Find Installed Package Using grep

Example:

sudo dpkg -l | grep python

Output:

ii libpython3-stdlib
ii libpython3.10
Apache Installation Example

Install Apache:

sudo apt install apache2

Check installed packages:

sudo dpkg -l | grep apache2

Output:

ii apache2
ii apache2-bin

ii → Installed package

Remove Package
Remove Package Only
sudo apt remove apache2
Purge Package

Remove package + config + documentation

sudo apt purge apache2

Check remaining packages:

sudo dpkg -l | grep apache2

Example remaining packages:

apache2-bin
apache2-data
apache2-utils

Remove all related packages:

sudo apt purge apache2*

Now check again:

sudo dpkg -l | grep apache2

Output:

(no output)

Apache completely removed.

Process Management
Check Running Processes
ps -ef

Example:

UID   PID  PPID  C STIME TTY  TIME CMD

More info:

man ps
Process Management Example

Create script:

script.sh

Example content:

sleep 120

Run script:

sh script.sh
Check Running Script
ps -ef | grep -i script.sh

Output:

varghese 36384 115 0 13:42 pts/0 00:00:00 sh script.sh

PID of script: 36384

Kill Process
sudo kill -9 36384

This will forcefully terminate the process.





# Linux File Permision

```bash
varghese@DESKTOP-OODIU93:~/temp$ ls -lrt
total 8
-rw-r--r-- 1 varghese varghese  6 Mar  3 12:15 tiju
-rw-r--r-- 1 varghese varghese 17 Mar  3 12:36 script1.sh

varghese@DESKTOP-OODIU93:~/temp$ ./script1.sh
-bash: ./script1.sh: Permission denied

varghese@DESKTOP-OODIU93:~/temp$ ls -lrt script1.sh
-rw-r--r-- 1 varghese varghese 17 Mar  3 12:36 script1.sh

varghese@DESKTOP-OODIU93:~/temp$ chmod u=rwx script1.sh

varghese@DESKTOP-OODIU93:~/temp$ ls -lrt script1.sh
-rwxr--r-- 1 varghese varghese 17 Mar  3 12:36 script1.sh

varghese@DESKTOP-OODIU93:~/temp$ ./script1.sh
Tue Mar  3 13:02:41 EST 2026

varghese@DESKTOP-OODIU93:~/temp$
```


## Granting Permission to Other Users

The `chmod` command can be used to modify file permissions.  
Here we grant **read, write, and execute permissions** to **other users**.

### Command

```bash
chmod o=rwx script1.sh

| Section | Meaning                 |
| ------- | ----------------------- |
| `rwx`   | Owner permissions       |
| `r--`   | Group permissions       |
| `rwx`   | Other users permissions |



# Absolute Path vs Relative Path

## Absolute Path
- Example: `ls /var/log/`
- Starts with `/` (root directory).
- It specifies the complete path from the root (`/`) to the target directory or file.
- It works from anywhere in the system.

## Relative Path
- Example: `ls var/log`
- Does NOT start with `/`.
- It specifies the path relative to your current working directory.
- It works only if the path exists from your current location.




Basic Linux Navigation Commands

This document explains some basic Linux terminal navigation commands.

1️⃣ Check Current Directory
pwd

Description:
Displays the current working directory.

Example Output:

/ home/varghese
2️⃣ List Files Inside a Directory Without Entering It
ls busapp

Description:
Lists all files and folders inside the busapp directory without navigating into it.

3️⃣ Change Directory
cd busapp

Description:
Moves into the busapp directory.

4️⃣ Move Up Two Directories
cd ../../

Description:
Moves up two levels in the directory structure.

Example:

/ home/varghese/busapp → / home
5️⃣ Go Back to Previous Directory
cd -

Description:
Returns to the previous directory you were in.

Example:

/ home → / home/varghese/busapp

cd - allows you to quickly switch back to your last working directory.


Go to Home Directory
cd ~

Description:
The ~ symbol represents the home directory of the current user.

Example:

varghese@DESKTOP-OODIU93:~/busapp$ cd ~
varghese@DESKTOP-OODIU93:~$ pwd
/home/varghese

This shows that you are now inside the home directory:
/home/varghese

2️⃣ List Files and Directories in Long Format
ls -l

Description:
Lists files and directories in the current location in long format.

Example Output:

total 36
drwxr-xr-x 6 varghese varghese 4096 Jan 13 11:40 Bash-Commands
drwxr-xr-x 2 varghese varghese 4096 Aug 22  2025 bash_varghese
drwxr-xr-x 3 varghese varghese 4096 Feb 21 18:30 busapp
drwxr-xr-x 3 varghese varghese 4096 Feb 19 11:52 busapp_Git_Demo_old
-rw-r--r-- 1 varghese varghese   14 Aug 26  2025 copy_tiju.txt
drwxr-xr-x 2 varghese varghese 4096 Dec 21  2024 from-windows
-rw-r--r-- 1 varghese varghese   79 Oct 22  2024 pg_hba.conf
drwx------ 3 varghese varghese 4096 Aug  2  2024 snap
drwxr-xr-x 4 varghese varghese 4096 Jan 10  2025 varghese
What ls -l Shows:

File type and permissions

Number of links

Owner name

Group name

File size

Last modified date

File or directory name

3️⃣ Listing a Specific Folder
ls -l varghese
Command Breakdown:

ls → Command (list directory contents)

-l → Option (long listing format)

varghese → Argument (the folder name to list)