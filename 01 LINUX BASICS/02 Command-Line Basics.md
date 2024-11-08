### Using the Command-Line in Kali Linux
In Kali Linux, one of the main ways to interact with the system is through the command-line, which is a text-based interface where you type commands to perform actions like running programs, navigating the system, or managing files. You open the command-line by launching a terminal.
### Opening a Terminal
To open a terminal in Kali Linux, click the black icon in the top-left corner of the screen. You’ll then see something like this:
```bash
┌──(kali@kali)-[~]
└─$
```
This is your command-line prompt.
### Shells
The "command-line" is also called a shell. A shell is a program that interprets your commands. There are different types of shells in Linux, such as:
- `sh`: The original shell.
- `bash`: An improved version of sh, which is the most common shell in Linux.
- `ksh`: A shell that adds extra features like better loops.
- `zsh`: Another shell with more features, often used by advanced users.
### Filesystem Structure
In Linux, there are no drive letters like on Windows (e.g., C:, D:). Instead, everything starts from the root directory (`/`). All files, folders, and devices are connected under this root directory.
- Example: `/home/kali/Documents` means the "Documents" folder inside the "kali" user folder, which is inside the "home" folder, starting from the root (`/`).
### Navigating Directories
- Use the `pwd` command to print the current directory you are in.
```bash
kali@kali:~$ pwd
/home/kali
```
- Use `cd <directory_name>` to change to a different directory. If you try to `cd` into a directory that doesn't exist, you will get an error.
```bash
kali@kali:~$ cd Documents
kali@kali:~/Documents$ pwd
/home/kali/Documents
kali@kali:~/Documents$ cd doesnotexist
cd: no such file or directory: /doesnotexist
```
- Use `cd ..` to go up one level in the directory structure.
```bash
kali@kali:~/Documents$ cd ..
kali@kali:~$ pwd
/home/kali
```
### Absolute vs. Relative Paths
- Absolute path: A full path starting from the root directory (`/`). For example, `/etc/passwd` is the absolute path to the passwd file.
```bash
kali@kali:~/Documents/drafts$ file /etc/passwd
/etc/passwd: ASCII text
```
- Relative path: A path relative to your current location. For example, `../../etc/passwd` means go up two directories from your current location, and then into the `/etc` folder.
```bash
kali@kali:~$ file ../../etc/passwd
/etc/passwd: ASCII text
```
If you change directories, the relative path will change, so be careful.
### Home Directory
- Tilde (`~`) represents your home directory. You can quickly jump back to your home directory with the command cd `~`.
```bash
kali@kali:/etc$ cd ~
kali@kali:~$ pwd
/home/kali
```
### Listing Files
- Use the `ls` command to list files in a directory.
```bash
kali@kali:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
```
- Add options to `ls` to change its behavior:
	- `ls -1` lists each file on a single line.
	- `ls -la` lists all files, including hidden ones, in a detailed format.
```bash
kali@kali:~$ ls -la
total 120
drwxr-xr-x 14 kali kali 4096 Jun 23 15:47 .
drwxr-xr-x  3 root root 4096 Jun 23 15:07 ..
-rw-r--r--  1 kali kali 220 Jun 23 15:07 .bash_logout
...
```
### Viewing Files
There are different commands to display the contents of files:
- `cat`: Displays the entire contents of a file. Use `cat -n` to show line numbers.
```bash
kali@kali:~$ cat file
this
is
a
file
that
has
many 
lines

kali@kali:~$ cat -n file
     1  this
     2  is
     3  a
     4  file
     5  that
     6  has
     7  many 
     8  lines
```
- `more`: Displays file contents one screen at a time (useful for large files).
- `less`: Like more, but with more features (you can scroll forward and backward).
- `head`: Shows the first few lines of a file (e.g., `head -n 3 file.txt` shows the first 3 lines).
- `tail`: Shows the last few lines of a file (e.g., `tail -n 3 file.txt` shows the last 3 lines).
