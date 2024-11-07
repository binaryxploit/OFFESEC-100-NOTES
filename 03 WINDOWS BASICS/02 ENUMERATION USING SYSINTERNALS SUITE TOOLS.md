## SOURCE
```bash
https://learn.microsoft.com/en-us/sysinternals/downloads/
```
## NOTE
```bash
- Upon executing any of the Sysinternals tools for the first time, we will need to accept the End-User License Agreement (eula).
- The eula can also be accepted via the command-line for each utility with the /accepteula option.

# Example
C:\Users\USER\Downloads\SysinternalsSuite> psinfo /accepteula
```
## SYSTEM INFORMATION - PSINFO
```bash
psinfo /accepteula
psinfo
```
## CHECK PERMISSIONS - ACCESSCHK
```bash
# Accept eula
accesschk /accepteula

# Check what permission the user group has on c drive C:
accesschk.exe "users" c:\
```
## VIEW, KILL PROCESS
```bash
# View process
pslist /accepteula

# -d switch to show information about threads running within processes
pslist -d

# The -t switch provides us with tree-like output that exposes child-parent relationships
pslist -t

# Kill process
pskill /accepteula
pskill 6135

# Suspend and Resume process
pssuspend /accepteula
pssuspend chrome.exe
# Resume
pssuspend /accepteula
pssuspend -r chrome.exe
```
## LIST DLL
```bash
# list dll
listdlls /accepteula

# -u switch to list any unsigned DLLs
listdlls -u
```
## DISK UTILITIES
```bash
du /accepteula

# To view the usage of a particular drive
du c:

# Check disk Usage C:\users
du c:\users

# View Files with alternate data stream ADS
dir /r

# View ADS Content
more < offsecStream.txt:offsec
```
