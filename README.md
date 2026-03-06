Linux

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