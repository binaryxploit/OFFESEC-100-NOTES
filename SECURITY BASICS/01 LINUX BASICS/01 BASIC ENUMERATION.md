## TOGGLE BETWEEN TERMINAL VIEW 
```bash
Ctrl + p
```
## ENVIRONMENTAL VARIABLES
```bash
# View Default environmental variables
set

# View value of the variable - example SHELL PATH
echo $SHELL
echo $PATH
```
## FIND
```bash
# Example
sudo find / -name offsec.txt -type f 2>/dev/null

# Options
-name - Search by filename or directory name (case sensitive).
-iname - Search by filename or directory name (case insensitive).
-type f/d/l/s - Search by type which can be (files,directories, links or sockets)
-size - Search by file or directory size.
-mtime - Search using the last modified date criteria.
-o - Allows us to combine multiple values of the same argument.
-user - Find files and directories based on their owner.
```
## TEXT MANIPULATION
```bash
# sed - replace words on output stream - Example
echo "I need to try hard" | sed 's/hard/harder/'

# cut - extract a field from output
cut -d ":" -f 1 /etc/passwd

# awk -  Extracting fields from a stream using a multi-character separator
echo "hello::there::friend" | awk -F "::" '{print $1, $3}'

# Compare files 
comm 
diff
```
## USERS AND GROUPS
```bash
# verify account lock and password expiration dates
passwd --status kali
chage -l kali

# Information about user accounts are stored
/etc/passwd

# fingerprints of the passwords are stored
/etc/shadow

# group memberships are defined in
/etc/group

# sudo configurations
/etc/sudoers

# list sudo permissions of user
sudo -l

# allows the current user to run a login shell as the root user
sudo -i
```
## FILE PERMISSIONS
```bash
# User catergories
u - as in user
g - as in group
o - as in other

# Types of rights
r - as in read
w - as in write
x - as in execute

# Numerical file permissions
7 = 4 + 2 + 1 = read, write, and execute
6 = 4 + 2 = read and write
5 = 4 + 1 = read and execute
3 = 2 + 1 = write and execute

# The most frequent right combinations are 
- 755 for executable filesdirectories
- 644 for data files

# Add or remove permission using
'+' - a+x
'-' - a-x 

# changing ownership on a file - examples
sudo chown root file.txt
sudo chown root:kali /usr/bin/idcopy

# changing permissions on a file - examples
chmod u+x,g+w,o-r file.txt

# Additional special rights pertain to executable files
- setuid 
- setgid 
- The lowercase "s", which appears here, means both execute and setuid flags are set. 
- A capital "S" would mean the setuid bit is set, but that the execute flag is missing.
- The sticky bit (symbolized by the letter "t") is a permission that is only useful in directories. It is commonly used for temporary
directories where everybody has write access (such as /tmp/).
```
## PROCESS
```bash
# Backgrounding a job right after it starts
ping -c 400 localhost > ping_results.txt &

# Using bg to background a job
bg

# Note
- the "&" symbol, the command would have run in the foreground
- cancel thecommand with Ctrl+c
- Wait until the command finishes to regain control of the terminal, or suspend the job using Ctrl+z after it has already started

# Using jobs to look at jobs
jobs

# fg to bring one into the foreground
fg
fg %1

# Note
- %Number : Refers to a job number such as %1 or %2.
- %String : Refers to the beginning of the suspended command's name such as %commandNameHere or %ping.
- %+ OR %% : Refers to the current job.
- %- : Refers to the previous job.

# List all the processes currently running
ps -ef

# Terminal process using PID
kill 1307
```
## FILE AND COMMAND MONITORING
```bash
# Continously monitor log file using tail
sudo tail -f /var/log/apache2/access.log 

# Monitoring logged in users
watch -n 5 w
```
## PACKAGE MANGAGEMENT
```bash
# Search for packages
sudo apt-cache search pure-ftpd

# View package Infortmation using - apt show
sudo apt show pure-ftpd Package: pure-ftpd
sudo apt show resource-agents Package: resource-agents

# Install applications
sudo dpkg -i man-db_2.7.0.2-5_amd64.deb
```
## SCHEDULED TASKS
```bash
# Linux-based job scheduler is known as Cron

# Listing all cron jobs on Linux
ls -lah /etc/cron*

# Read /etc/crontab
cat /etc/crontab
```
## LOGS
```bash
# Most Unix-like systems, as well as services running on them, produce logs within the /var/log directory.
ls -la /var/log

# Authentication log
less /var/log/auth.log

# Checking who has logged in to this machine
who /var/log/wtmp | tail -5 

# Kernel logs
dmesg

# Dump all logs Chronologically
journalctl 
journalctl -r          # Reverse the log order
journalctl -f          # continously update the logs
journalctl -u ssh.service         # limit the messages to those emitted by a specific systemd unit
```
## DISC MANAGEMENT
```bash
# Tools used
- free
- dd
- du
- df
- mount
- fdisk

# check information on memory
free -m

# check disk space
df -h

# Note
- dd is mostly used to raw copy a device file on a block level.
- du can be used to determine the size of files and directories. The -hs option is typically used to make the output more human readable.
- df and its -T option can be used to show the type of the filesystem.

# Details about our USB drive
sudo fdisk -l

# create a folder and mount
sudo mkdir /mnt/usb
sudo mount /dev/sdb1 /mnt/usb

# Unmount
sudo umount /mnt/usb
```