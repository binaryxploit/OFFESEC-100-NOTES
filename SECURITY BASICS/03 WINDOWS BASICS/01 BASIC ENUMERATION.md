## WINDOWS COMMAND-LINE INTERFACES
```bash
- cmd.exe
- PowerShell
- WMIC
- Windows Subsystem for Linux (WSL)
```
## WINDOWS PERMISSIONS
```bash
- ACL (access control lists)
- ACE (access control entries )

- local users and permissions
- network-based users and permissions
```
## WINDOWS PROCESSES
```bash
- Kernel Mode
- User Mode
```
## NAVIGATION
```bash
# Navigate to root directory of current drive
cd \ 
cd / 

# View  Hidden files
dir /A
```
## SYSTEM INFORMATION
```bash
# System Information
systeminfo

# Environmental Variables
set

# Echo Environmental Variable - username
echo %username%
```
## FIND FILES 
```bash
# Search for any file in the given folder and any of its subfolders. /p to pause the print after the terminal page is full.
dir /s filename.txt
dir /s *.exe /p

# tree - View Directory Structure. /F flag will display any files that exist within each of the directories in the output.
tree
tree /F

# forfiles - Using forfiles to find the path of notepad.exe. /P specifies where to begin our search. /S indicates that we want to search recursively. /M points at what we want to search for. /C executes a specified command.
forfiles /P C:\Windows /S /M notepad.exe /c "cmd /c echo @PATH"

# find - Searches for a text string in a file or files. Using find for finding the string 'password' in a file.  
find "password" C:\Users\Offsec\importantfile.txt
type importantfile.txt |find "password"

# findstr - Searches for strings in files. 
findstr "Johnny password" importantfile.txt
```
## VIEW USER SID
```bash
# View user SID
whoami /user

# Administrator | S-1-5-domain-500 
# Guest | S-1-5-32-546
# SYSTEM
# Everyone Group | S-1-1-0

# Note - SID example 
S-1-5-21-2753864161-1776656122-2845895175-1001
- The 3rd component of a SID indicates the principal's identifier authority.
- 5 indicates that the SID belongs to an individual account or a group.
```
## ADD NEW USER, VIEW INFO, VIEW LOCAL GROUP, ADD USER TO GROUP
```bash
# View User accounts
net user

# Add User
net user /add offsec Mypassword1

# Delete user
net user /del offsec

# View user information
net user offsec

# View localgroup information
net localgroup

# Add user to Administrator Group
net localgroup Administrators offsec /add

# Remove user from Administrators group
net localgroup Administrators offsec /del

# View current account policies
net accounts
```
## RUNAS 
```bash
# Use runas to execute command as offsec user 
runas /user:offsec "cmd.exe"
runas /user:offsec "cmd.exe /c echo hello"
runas /user:DOMAIN\username "notepad.exe"
```
## ICACLS, CACLS - VIEW PERMISSIONS
```bash
# Interact with permissions on a Windows system cacls/icacls - icacls is deprecated
icacls Music

# Grant permission
icacls Music /grant offsec:(OI)(CI)(F)

# Remove permission
icacls Music /deny offsec:(OI)(CI)(F)

# /t option to check that the assigned permissions have been propagated to children of the directory.
icacls Music /t /c
```
## VIEW, KILL PROCESS
```bash
# Check windows process
tasklist

# tasklist to view SYSTEM's running processes. /FI flag, which allows us to parse results based on additional input.
tasklist /fi "USERNAME eq NT AUTHORITY\SYSTEM" /fi "STATUS eq running"

# Kill process via PID
taskkill /PID 84
```
## INTERACT WITH REGISTRY
```bash
# Registry command
reg

# Query Registry - example Run and RunOnce key
reg query hkcu\software\microsoft\windows\currentversion\runonce
reg query hkcu\software\microsoft\windows\currentversion\runonce

# Remove value from registry
reg delete hkcu\software\microsoft\windows\currentversion\run /va

# Add vaules to the key - example add onedrive key value. /t to specify its data type, and /d to supply the data
reg add hkcu\software\microsoft\windows\currentversion\run /v OneDrive /t REG_SZ /d "C:\Users\Offsec\AppData\Local\Microsoft\OneDrive\OneDrive.exe"
reg query hkcu\software\microsoft\windows\currentversion\run

# Export Registry keys
reg export hkcu\environment environment
```
## SCHEDULE TASKS 
```bash
# Command - schtasks command replaces the now deprecated at command
schtasks

# list of all currently scheduled tasks
schtasks
schtasks /query

# /create - to create tasks. /create help - for more help
schtasks /create
schtasks /create help

# Example, let's imagine we wish to run a binary called runme.exe every Monday at 9:00AM
schtasks /create /sc weekly /d mon /tn runme /tr C:\runme.exe /st 09:00

# Delete scheduled tasks
schtasks /delete /tn runme

# Use the query parameter and the /fo LIST parameter to output the results in a list.
schtasks /query /TN runme /fo LIST 
```
## DISK UTILITIES
```bash
#  fsutil fsinfo commands
fsutil fsinfo

# Listing out drives
fsutil fsinfo drives

# Examine the individual drives with the drivetype subcommand
fsutil fsinfo drivetype C:
fsutil fsinfo drivetype D:
fsutil fsinfo drivetype E:

# Listing out information about the C: drive
fsutil fsinfo volumeinfo C:
```