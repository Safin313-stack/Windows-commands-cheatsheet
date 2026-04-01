<div align="center">

# 🖥️ Windows CMD & PowerShell — Complete Cybersecurity & Admin Cheatsheet

[![GitHub stars](https://img.shields.io/github/stars/Safin313-stack?style=flat-square&color=yellow)](https://github.com/Safin313-stack)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-green.svg?style=flat-square)](https://github.com/Safin313-stack)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen.svg?style=flat-square)](CONTRIBUTING.md)

> **The most complete Windows CMD & PowerShell reference for cybersecurity learners, SOC analysts, sysadmins, and pentesters.**  
> From basic recon to forensics, registry to boot repair — all in one place.

**Author:** [Saharia Hassan Safin](https://github.com/Safin313-stack) · Dhaka, Bangladesh 🇧🇩

</div>

---

## 📋 Table of Contents

| # | Section | # | Section |
|---|---------|---|---------|
| 01 | [🔍 System Information](#-system-information) | 10 | [🔄 Windows Update & Activation](#-windows-update--activation) |
| 02 | [👤 User Account Management](#-user-account-management) | 11 | [🚀 Boot & Startup Repair](#-boot--startup-repair) |
| 03 | [🌐 Network Commands](#-network-commands) | 12 | [📋 Scheduled Tasks](#-scheduled-tasks) |
| 04 | [📁 Files & Directories](#-files--directories) | 13 | [🗝️ Registry Commands](#-registry-commands) |
| 05 | [🔎 Search & Forensics](#-search--forensics) | 14 | [📜 Event Log Management](#-event-log-management) |
| 06 | [⚙️ Process & Service Control](#-process--service-control) | 15 | [🛡️ Malware & Defender Tools](#-malware--defender-tools) |
| 07 | [🔐 Security & Permissions](#-security--permissions) | 16 | [💙 PowerShell Admin Tools](#-powershell-admin-tools) |
| 08 | [💽 Disk & System Utilities](#-disk--system-utilities) | 17 | [🔴 CMD Tips & Tricks](#-cmd-tips--tricks) |
| 09 | [🌍 Remote Access & Management](#-remote-access--management) | 18 | [🧰 Misc & Utilities](#-misc--utilities) |

---

> ⚠️ **Disclaimer:** All commands are for **educational purposes** and **authorized use only**. Always get proper written permission before running these commands on systems you don't own. The author holds no responsibility for misuse.

---

## 🔍 System Information

> Initial reconnaissance — profile a machine, its OS, hardware, and environment.

```cmd
whoami                              # Shows the currently logged-in user
hostname                            # Shows the computer's name
systeminfo                          # Full device and OS details — like the "About" section
ver                                 # Shows the Windows version
set                                 # Lists all environment variables (system-wide saved values)
echo %username%                     # Prints the current username
echo %COMPUTERNAME%                 # Prints the computer name as a variable
echo %OS%                           # Shows the OS name stored as an environment variable
echo %PROCESSOR_ARCHITECTURE%       # Shows the CPU architecture (x86, AMD64, ARM64)
echo %APPDATA%                      # Shows the path to the current user's AppData folder
echo %TEMP%                         # Shows the path to the temp directory
date /t                             # Shows today's date without prompting to change it
time /t                             # Shows the current time without prompting to change it
driverquery                         # Lists all installed device drivers
driverquery /v                      # Shows verbose info about all drivers (version, state)
tasklist                            # Shows all currently running processes with PID
tasklist /svc                       # Same as tasklist but also shows services inside each process
tasklist /v                         # Verbose view of processes with memory and CPU info
wmic os get name                    # Shows the operating system name and edition
wmic os get version                 # Shows the OS version number
wmic os get osarchitecture          # Shows 32-bit or 64-bit OS architecture
wmic os get lastbootuptime          # Shows when the computer was last rebooted
wmic cpu get name                   # Shows the CPU model name
wmic cpu get numberofcores          # Shows how many CPU cores the system has
wmic bios get serialnumber          # Shows the BIOS serial number (useful for asset tracking)
wmic bios get version               # Shows the BIOS version
wmic memorychip get capacity        # Shows the RAM size of each memory stick
wmic diskdrive get model,size       # Shows all physical disk drives and their sizes
wmic logicaldisk get name,size,freespace  # Shows all drives with total and free space
wmic product get name,version       # Lists all installed software with version numbers
wmic qfc                            # Lists installed Windows updates (hotfixes)
wmic /node:<IP> os get caption      # Gets OS info from a remote computer
msinfo32                            # Opens the System Information GUI tool
winver                              # Opens a popup showing the exact Windows version and build
```

---

## 👤 User Account Management

> Manage local users, groups, and access control — essential for privilege awareness and defense.

```cmd
net user                                         # Lists all local user accounts
net user <username>                              # Shows detailed info about a specific user
net user <username> /add                         # Creates a new local user account
net user <username> <password> /add              # Creates a new user with a set password
net user <username> /delete                      # Deletes a user account
net user administrator /active:yes               # Enables the built-in Administrator account
net user administrator /active:no                # Disables the built-in Administrator account
net user <username> /active:no                   # Disables a specific user account
net user <username> /active:yes                  # Re-enables a disabled user account
net user <username> *                            # Prompts to change a user's password
net user <username> /expires:MM/DD/YYYY          # Sets an expiry date for a user account
net localgroup                                   # Lists all local groups
net localgroup administrators                    # Shows all members of the Administrators group
net localgroup administrators <username> /add    # Adds a user to the Administrators group
net localgroup administrators <username> /delete # Removes a user from the Administrators group
net localgroup <groupname>                       # Shows members and details of a group
net localgroup <groupname> /add                  # Creates a new local group
net localgroup <groupname> /delete               # Deletes a local group
whoami                                           # Shows current user
whoami /groups                                   # Shows all groups the current user belongs to
whoami /priv                                     # Shows special privileges the current user has
whoami /all                                      # Shows user, groups AND privileges in one output
query user                                       # Shows all currently logged-in users and session info
net accounts                                     # Shows the current password policy
net accounts /minpwlen:12                        # Sets minimum password length to 12 characters
net accounts /maxpwage:30                        # Forces password change every 30 days
net accounts /minpwage:1                         # Sets minimum days before a password can be changed
net accounts /lockoutthreshold:5                 # Locks account after 5 failed login attempts
runas /user:<username> cmd                       # Opens CMD as a different user
runas /user:administrator cmd                    # Opens CMD as Administrator
control userpasswords2                           # Opens the advanced user accounts settings window
lusrmgr.msc                                      # Opens the Local Users and Groups Manager (GUI)
rundll32.exe user32.dll,LockWorkStation          # Instantly locks the workstation
taskmgr                                          # Opens Task Manager
eventvwr                                         # Opens Event Viewer — view system and security logs
```

---

## 🌐 Network Commands

> Understand, inspect, and control the network — critical for both attack and defense.

```cmd
# ── IP Configuration ──────────────────────────────────────────────
ipconfig                                        # Shows basic IP address info
ipconfig /all                                   # Full network config (MAC, DNS, DHCP, gateway...)
ipconfig /release                               # Releases the current DHCP-assigned IP address
ipconfig /renew                                 # Requests a new IP address from the DHCP server
ipconfig /displaydns                            # Shows the local DNS cache
ipconfig /flushdns                              # Clears the DNS cache
ipconfig /registerdns                           # Refreshes all DHCP leases and re-registers DNS names

# ── Netsh ──────────────────────────────────────────────────────────
netsh winsock reset                             # Resets Winsock (list of network protocol handlers)
netsh int ip reset                              # Resets the TCP/IP stack to default settings
netsh wlan show profile                         # Lists all saved Wi-Fi profiles
netsh wlan show profile <name> key=clear        # Shows Wi-Fi password for a saved profile
netsh wlan delete profile name=<name>           # Deletes a saved Wi-Fi profile
netsh wlan connect name=<name>                  # Connects to a saved Wi-Fi profile
netsh wlan disconnect                           # Disconnects from the current Wi-Fi network
netsh interface show interface                  # Shows all network interfaces and their status
netsh interface ip show config                  # Shows detailed IP config of all interfaces
netsh advfirewall reset                         # Resets all firewall rules to default
netsh advfirewall show allprofiles              # Shows firewall status for all profiles
netsh advfirewall firewall show rule name=all   # Lists all firewall rules
netsh advfirewall set allprofiles state on      # Turns on the firewall for all profiles
netsh advfirewall set allprofiles state off     # Turns off the firewall for all profiles (use carefully)
netsh advfirewall firewall add rule name="Block Telnet" protocol=TCP dir=in localport=23 action=block  # Block a port

# ── Physical & ARP ──────────────────────────────────────────────
getmac                                          # Shows MAC (physical hardware) addresses
getmac /v                                       # Verbose — shows MAC with adapter name
arp -a                                          # Shows all LAN devices your PC has recently talked to
arp -d                                          # Clears the ARP cache
arp -s <IP> <MAC>                               # Adds a static ARP entry

# ── Routing ───────────────────────────────────────────────────────
route print                                     # Shows the full routing table
route add <network> mask <mask> <gateway>       # Adds a static route
route delete <network>                          # Removes a route from the routing table

# ── Connections & Ports ──────────────────────────────────────────
netstat -an                                     # Shows all active connections and open ports
netstat -ano                                    # Same + shows PID for each connection
netstat -b                                      # Same + shows executable (.exe) responsible
netstat -s                                      # Shows per-protocol statistics (TCP, UDP, ICMP)
netstat -r                                      # Shows the routing table (same as route print)
netstat -e                                      # Shows Ethernet statistics (bytes sent/received)

# ── DNS & Connectivity ────────────────────────────────────────────
ping <host>                                     # Tests basic connectivity to a host
ping -t <host>                                  # Pings continuously until stopped (Ctrl+C)
ping -n 10 <host>                               # Sends exactly 10 ping packets
ping -l 1000 <host>                             # Sends a ping with a custom packet size (1000 bytes)
tracert <host>                                  # Traces the full path packets take to reach a host
pathping <host>                                 # Like tracert but also measures packet loss/latency
nslookup <domain>                               # Resolves a domain to its IP address
nslookup <domain> 8.8.8.8                       # DNS lookup using a specific DNS server (Google)
nslookup -type=MX <domain>                      # Looks up mail exchange (MX) records for a domain
nslookup -type=TXT <domain>                     # Looks up TXT records (used for SPF, DMARC, etc.)

# ── Network Shares & Remote ───────────────────────────────────────
net view                                        # Lists computers and shared resources on the LAN
net view \\<target>                             # Shows shared folders on a specific computer
nbtstat -n                                      # Lists all local NetBIOS names registered
nbtstat -A <ip>                                 # Shows NetBIOS info for a remote computer by IP
nbtstat -c                                      # Shows the local NetBIOS name cache
net use                                         # Shows all active mapped drives and connections
net use \\<ip>\<share>                          # Connects to a shared folder
net use Z: \\<ip>\<share>                       # Maps a shared folder to drive letter Z
net use Z: /delete                              # Disconnects a mapped drive
net share                                       # Lists all shared folders on the local machine
net share <name>=C:\path /grant:<user>,full     # Creates a new shared folder with permissions

# ── DHCP ──────────────────────────────────────────────────────────
net stop dhcp                                   # Stops the DHCP client service
net start dhcp                                  # Starts the DHCP client service
```

---

## 📁 Files & Directories

> Navigate, create, copy, move, hide, and manipulate the Windows file system.

```cmd
dir                                 # Lists all files and folders in the current directory
dir /a                              # Lists everything including hidden and system files
dir /a:h                            # Lists only hidden files
dir /s                              # Lists files in all subdirectories recursively
dir /o:s                            # Lists files sorted by size (smallest first)
dir /o:-s                           # Lists files sorted by size (largest first)
dir /o:d                            # Lists files sorted by date (oldest first)
dir /b                              # Bare format — shows only file names, no extra info
dir *.exe                           # Lists only .exe files in the current directory
tree                                # Displays directory structure as a visual tree
tree /f                             # Shows tree including file names inside each folder
cd <directory>                      # Changes the current directory
cd ..                               # Goes one level up in the directory tree
cd \                                # Goes directly to the root of the current drive
cd /d D:\folder                     # Changes both drive and directory at once
mkdir <foldername>                  # Creates a new folder
mkdir C:\A\B\C                      # Creates nested folders all at once
rmdir <foldername>                  # Removes an empty folder
rmdir /s /q <foldername>            # Removes a folder and all contents silently (no prompt)
del <filename>                      # Deletes a file
del /f /q <filename>                # Force-deletes a file silently (even read-only)
del /f /s /q <foldername>\*.*       # Deletes all files in a folder and subfolders silently
copy <file> <destination>           # Copies a file to a destination
copy /y <file> <destination>        # Copies a file and overwrites without asking
move <file> <destination>           # Moves a file to a new location
rename <filename> <newname>         # Renames a file
type file.txt                       # Prints the full content of a text file to the screen
more file.txt                       # Reads a text file page by page (great for large files)
echo Hello > file.txt               # Creates a file and writes "Hello" into it
echo More text >> file.txt          # Appends text to an existing file
attrib                              # Shows all file attributes (hidden, system, read-only...)
attrib +h <file>                    # Hides a file (sets hidden attribute)
attrib -h <file>                    # Unhides a file
attrib +r <file>                    # Sets a file as read-only
attrib -r <file>                    # Removes the read-only attribute
attrib +s <file>                    # Sets the system attribute on a file
attrib -h -r -s /s /d *.*           # Removes hidden, read-only, system attributes recursively
where <filename>                    # Finds the full path of a file or executable
assoc                               # Shows file extension associations
assoc .txt                          # Shows what program opens .txt files
ftype                               # Shows all registered file types and their open commands
mklink <link> <target>              # Creates a symbolic link (shortcut) to a file or folder
mklink /d <link> <target>           # Creates a symbolic link to a directory
expand <source.cab> <destination>   # Extracts files from a CAB archive
```

---

## 🔎 Search & Forensics

> Find files, compare them, hash them, investigate the file system — key digital forensics skills.

```cmd
find "text" file.txt                    # Searches for a specific string inside a file
find /i "text" file.txt                 # Same but case-insensitive
find /c "text" file.txt                 # Counts the number of lines containing the text
findstr "search phrase" file.txt        # Searches for a phrase (supports regex, more powerful)
findstr /i "text" file.txt              # Case-insensitive search
findstr /s "text" *.txt                 # Recursively searches all .txt files in subdirectories
findstr /r "reg.*ex" file.txt           # Searches using a regular expression pattern
fc file1 file2                          # Compares two files and shows the differences
fc /b file1 file2                       # Compares two files in binary mode
dir /s <filename>                       # Searches for a file recursively in all subdirectories
dir /s /b *.log                         # Finds all .log files on the system (bare output)
dir /R                                  # Lists files and any Alternate Data Streams (ADS) — forensic use

certutil -hashfile <file> md5           # Generates an MD5 hash (quick integrity check)
certutil -hashfile <file> sha1          # Generates a SHA-1 hash
certutil -hashfile <file> sha256        # Generates a SHA-256 hash (most trusted — verify downloads)
certutil -urlcache -split -f <URL> <output>  # Downloads a file from a URL (used for file transfer)
certutil -decode <encoded.b64> <output.bin>  # Decodes a Base64 encoded file

cipher /c <file>                        # Shows EFS encryption info for a file
cipher /e <file>                        # Encrypts a file using EFS (Windows Encrypting File System)
cipher /d <file>                        # Decrypts an EFS-encrypted file
cipher /w:C                             # Securely overwrites all free space on drive C
compact                                 # Checks or applies NTFS compression on files
compact /u <file>                       # Decompresses a file compressed with NTFS compact
```

---

## ⚙️ Process & Service Control

> Monitor, control, start, and stop processes and services — core for incident response and malware analysis.

```cmd
# ── Processes ──────────────────────────────────────────────────────
tasklist                            # Lists all running processes with their PID and memory
tasklist /v                         # Verbose — shows CPU, memory, user, window title per process
tasklist /svc                       # Shows which services are hosted inside each process
tasklist /fi "status eq running"    # Filters to show only running processes
tasklist /fi "memusage gt 50000"    # Shows processes using more than 50MB of memory
tasklist /fi "imagename eq notepad.exe"  # Shows if a specific process is running
taskkill /PID <PID>                 # Terminates a process by its PID
taskkill /PID <PID> /F              # Force-terminates a process by PID (no confirmation)
taskkill /IM <name>.exe             # Terminates a process by name
taskkill /IM <name>.exe /F          # Force-kills a process by name
taskkill /IM <name>.exe /F /T       # Kills a process and all its child processes
start <program>                     # Starts a program
start /wait <program>               # Starts a program and waits for it to finish
start /min <program>                # Starts a program minimized
timeout /t 10                       # Pauses CMD for 10 seconds

# ── Services ────────────────────────────────────────────────────────
sc query                            # Lists all currently running services
sc query state=all                  # Lists all services (running, stopped, paused, etc.)
sc query <servicename>              # Shows detailed status of a specific service
sc start <servicename>              # Starts a service
sc stop <servicename>               # Stops a service
sc config <servicename> start=auto  # Sets a service to start automatically at boot
sc config <servicename> start=disabled  # Disables a service from starting
sc config <servicename> start=demand    # Sets a service to manual start
sc delete <servicename>             # Deletes a service (permanent — use carefully)
sc create <name> binPath=<path>     # Creates a new service from an executable
net start <servicename>             # Starts a service (simpler syntax)
net stop <servicename>              # Stops a service
net start                           # Lists all currently running services (simple output)
```

---

## 🔐 Security & Permissions

> Control file access, take ownership, audit policy, and manage privilege — the foundation of Windows security.

```cmd
# ── File Permissions (ICACLS) ─────────────────────────────────────
icacls <file>                               # Shows file/folder permissions
icacls <file> /grant <user>:F               # Grants a user full control over a file
icacls <file> /grant <user>:R               # Grants a user read-only access
icacls <file> /grant <user>:W               # Grants a user write access
icacls <file> /deny <user>:F                # Explicitly denies a user all access
icacls <file> /remove <user>                # Removes a user's permissions from a file
icacls <folder> /grant <user>:F /t          # Applies full access recursively to all sub-items
icacls <folder> /reset /t                   # Resets permissions on all items to inherited
icacls <file> /save perms.txt               # Saves current permissions to a file (for backup)
icacls <file> /restore perms.txt            # Restores permissions from a saved file

# ── Ownership ─────────────────────────────────────────────────────
takeown /f <file>                           # Takes ownership of a file
takeown /f <folder> /r /d y                 # Takes ownership of a folder and all contents recursively

# ── Audit Policy ──────────────────────────────────────────────────
auditpol /get /category:*                   # Shows all audit categories and what is being logged
auditpol /set /category:"Logon/Logoff" /success:enable /failure:enable  # Enables logon auditing
auditpol /clear /y                          # Clears all audit policy settings

# ── Group Policy & Security Policy ───────────────────────────────
secedit /export /cfg output.cfg             # Exports the current security policy to a file
secedit /analyze /db secedit.sdb /cfg output.cfg  # Analyzes the current policy against a template
gpresult /r                                 # Shows which Group Policy is applied to user/computer
gpresult /h gpreport.html                   # Exports the full Group Policy report as HTML
gpupdate /force                             # Immediately reapplies all Group Policy settings
gpupdate /target:user                       # Updates only user Group Policy
gpupdate /target:computer                   # Updates only computer Group Policy

# ── Session & Shutdown ────────────────────────────────────────────
logoff                                      # Logs off the current user session
logoff <sessionID>                          # Logs off a specific user session by session ID
shutdown /s /t 0                            # Shuts down the computer immediately
shutdown /r /t 0                            # Restarts the computer immediately
shutdown /a                                 # Aborts a scheduled shutdown
shutdown /l                                 # Logs off the current user (same as logoff)
shutdown /s /t 60 /c "Maintenance restart"  # Shuts down after 60 seconds with a message
```

---

## 💽 Disk & System Utilities

> Manage, repair, optimize, and monitor storage and the Windows system.

```cmd
# ── Disk Check & Repair ───────────────────────────────────────────
chkdsk                                          # Checks the current drive for errors
chkdsk C: /f                                    # Fixes file system errors on drive C
chkdsk C: /r                                    # Locates bad sectors and recovers readable data
chkdsk C: /f /r /x                              # Fixes errors, recovers data, dismounts drive first
sfc /scannow                                    # Scans and repairs corrupted Windows system files
sfc /verifyonly                                 # Scans for corrupted files without repairing
dism /online /cleanup-image /checkhealth        # Quick check if the Windows image is corrupted
dism /online /cleanup-image /scanhealth         # Deeper scan of the Windows image
dism /online /cleanup-image /restorehealth      # Full repair of the Windows image (uses Windows Update)

# ── Disk Management ───────────────────────────────────────────────
diskpart                                        # Opens the disk partition manager (CLI)
diskmgmt.msc                                    # Opens Disk Management (GUI)
mountvol                                        # Shows all volume mount points
fsutil dirty query C:                           # Checks if drive C has the dirty bit (corruption flag)
fsutil volume diskfree C:                       # Shows free space info for drive C
fsutil file queryvaliddata <file>               # Shows the valid data length of a file
format D: /fs:ntfs                              # Formats drive D with NTFS (WARNING: destroys all data)
format D: /fs:fat32                             # Formats drive D with FAT32
label D: BackupDrive                            # Renames the label of drive D
vol C:                                          # Shows the label and serial number of drive C

# ── Copy & Backup ─────────────────────────────────────────────────
robocopy C:\Source D:\Backup /E                 # Copies all files + empty folders from Source to Backup
robocopy C:\Source D:\Backup /E /Z              # Same but restartable (good for large files over network)
robocopy C:\Source D:\Backup /E /MIR            # Mirror backup — deletes files in dest that aren't in source
robocopy C:\Source D:\Backup /E /LOG:backup.log # Logs all copy operations to a file
xcopy source destination /E /H /C /I           # Copies all files including hidden/system, continues on error

# ── Cleanup & Maintenance ─────────────────────────────────────────
cleanmgr                                        # Opens Disk Cleanup tool
defrag C:                                       # Defragments drive C (reorganizes fragmented files)
defrag C: /u /v                                 # Defrag with progress and verbose output
del /f /s /q C:\Windows\Temp\*.*               # Silently deletes all temp files
del /f /s /q %TEMP%\*.*                         # Deletes current user's temp files
compact                                         # Checks NTFS compression status of current folder
compact /c /s:<folder>                          # Compresses all files in a folder

# ── System Configuration ──────────────────────────────────────────
msconfig                                        # Opens System Configuration (startup, boot, services)
services.msc                                    # Opens the Services manager (GUI)
powercfg /batteryreport                         # Generates a detailed battery health report (HTML file)
powercfg /energy                                # Analyzes power efficiency and creates a report
powercfg /hibernate on                          # Enables hibernate mode
powercfg /hibernate off                         # Disables hibernate mode
powercfg /sleepstudy                            # Shows sleep activity and power usage report
perfmon                                         # Opens Performance Monitor
resmon                                          # Opens Resource Monitor (CPU, RAM, disk, network)
gpedit.msc                                      # Opens the Group Policy Editor (Local)
secpol.msc                                      # Opens Local Security Policy
compmgmt.msc                                    # Opens Computer Management (all-in-one admin console)
sysdm.cpl                                       # Opens System Properties (environment vars, name, etc.)
mmc                                             # Opens Microsoft Management Console (build custom tools)
```

---

## 🌍 Remote Access & Management

> Connect to, manage, and interact with remote systems — critical for sysadmins and red teamers.

```cmd
# ── Remote Desktop & Sessions ─────────────────────────────────────
mstsc                                           # Opens Remote Desktop Connection client
mstsc /v:<IP>                                   # Connects to a remote computer by IP
mstsc /v:<IP> /admin                            # Connects to admin session (console session)
qwinsta                                         # Lists all remote desktop sessions on this machine
rwinsta <sessionID>                             # Ends/resets a remote desktop session
query session                                   # Lists all sessions (same as qwinsta)
msg <username> "Your message here"              # Sends a message to a logged-in user's screen
msg * "Rebooting in 5 minutes"                  # Broadcasts a message to all logged-in users

# ── PsExec / WinRM / Remote CMD ───────────────────────────────────
winrs -r:<remote> cmd                           # Opens a CMD on a remote computer using WinRM
winrs -r:<remote> ipconfig                      # Runs a command on a remote machine
winrm quickconfig                               # Enables and configures WinRM on the local machine
winrm get winrm/config                          # Shows current WinRM configuration

# ── Remote WMIC ───────────────────────────────────────────────────
wmic /node:<IP> os get caption                  # Gets OS name from a remote computer
wmic /node:<IP> process list brief              # Lists processes on a remote computer
wmic /node:<IP> service list brief              # Lists services on a remote computer

# ── Remote Shares ─────────────────────────────────────────────────
net view \\<IP>                                 # Lists shared folders on a remote computer
net use \\<IP>\<share> /user:<username>         # Maps a remote share with credentials
net session                                     # Lists all current connections to this machine
net session \\<IP> /delete                      # Disconnects a remote session by IP

# ── SSH (Windows 10/11 Built-in) ─────────────────────────────────
ssh <user>@<IP>                                 # SSH into a remote machine
ssh -p 22 <user>@<IP>                           # SSH using a specific port
ssh-keygen                                      # Generates an SSH key pair
scp <file> <user>@<IP>:/path                    # Securely copies a file to a remote machine over SSH
```

---

## 🔄 Windows Update & Activation

> Manage Windows updates and licensing from the command line.

```cmd
wuauclt /detectnow                                      # Forces Windows to check for available updates
wuauclt /updatenow                                      # Forces update download and installation
usoclient startscan                                     # Scans for updates (modern Windows)
usoclient startinstall                                  # Installs available updates (modern Windows)
usoclient startdownload                                 # Downloads updates without installing
control update                                          # Opens Windows Update settings panel
sc query wuauserv                                       # Checks if the Windows Update service is running
net start wuauserv                                      # Starts the Windows Update service
net stop wuauserv                                       # Stops the Windows Update service
slmgr /ipk XXXXX-XXXXX-XXXXX-XXXXX-XXXXX               # Installs a Windows product key
slmgr /ato                                              # Activates Windows using the installed key
slmgr /xpr                                              # Checks Windows activation and expiry status
slmgr /dlv                                              # Shows detailed licensing information
slmgr /rearm                                            # Resets the Windows activation grace timer
slmgr /upk                                              # Uninstalls the current product key
```

---

## 🚀 Boot & Startup Repair

> Fix boot problems and manage boot configuration — essential for recovery and forensic scenarios.

```cmd
bcdedit /enum all                               # Displays all boot configuration entries
bcdedit /enum active                            # Shows only the active boot entries
bcdedit /set {default} description "My Windows"# Renames the default boot entry
bcdedit /set {default} safeboot minimal         # Configures Windows to boot into Safe Mode
bcdedit /deletevalue {default} safeboot         # Removes the Safe Mode boot flag (normal boot)
bcdedit /set {default} nointegritychecks on     # Disables driver signature enforcement (use carefully)
bcdedit /copy {current} /d "Backup Boot"        # Creates a copy of the current boot entry
bcdedit /delete {ID}                            # Deletes a specific boot entry by its ID
bootrec /fixmbr                                 # Repairs the Master Boot Record (MBR)
bootrec /fixboot                                # Repairs the boot sector of the active partition
bootrec /scanos                                 # Scans all disks for Windows installations
bootrec /rebuildbcd                             # Rebuilds the Boot Configuration Data (BCD)
bcdboot C:\Windows                              # Recreates boot files from the Windows installation
bcdboot C:\Windows /s Z: /f UEFI               # Creates UEFI boot files on a specific drive
reagentc /enable                                # Enables the Windows Recovery Environment (WinRE)
reagentc /disable                               # Disables WinRE
reagentc /info                                  # Shows the current recovery environment status
```

---

## 📋 Scheduled Tasks

> Create, manage, and audit scheduled tasks — also critical for detecting malware persistence.

```cmd
schtasks                                                # Lists all scheduled tasks (basic view)
schtasks /query                                         # Displays all scheduled tasks
schtasks /query /fo list /v                             # Shows detailed info about every task
schtasks /query /tn "TaskName"                          # Shows details of a specific task
schtasks /query /fo csv > tasks.csv                     # Exports all tasks to a CSV file

# ── Create Tasks ──────────────────────────────────────────────────
schtasks /create /sc daily /tn "MyTask" /tr "C:\script.bat" /st 09:00             # Runs daily at 9AM
schtasks /create /sc weekly /d MON /tn "WeeklyTask" /tr "C:\script.bat" /st 08:00 # Runs every Monday
schtasks /create /sc onlogon /tn "LoginTask" /tr "C:\script.bat"                  # Runs at every logon
schtasks /create /sc onstart /tn "StartTask" /tr "C:\script.bat" /ru SYSTEM       # Runs at system startup
schtasks /create /sc minute /mo 30 /tn "Every30Min" /tr "C:\script.bat"           # Runs every 30 minutes
schtasks /create /sc once /tn "OneTime" /tr "C:\script.bat" /sd 12/31/2025 /st 23:59  # Runs once at set time

# ── Modify & Control Tasks ────────────────────────────────────────
schtasks /run /tn "TaskName"                            # Runs a scheduled task immediately
schtasks /end /tn "TaskName"                            # Stops a currently running task
schtasks /change /tn "TaskName" /st 10:00               # Changes the run time of a task
schtasks /change /tn "TaskName" /enable                 # Re-enables a disabled task
schtasks /change /tn "TaskName" /disable                # Disables a task without deleting it
schtasks /delete /tn "TaskName" /f                      # Deletes a task permanently (no confirmation)
schtasks /delete /tn * /f                               # Deletes ALL scheduled tasks (use with extreme caution)
taskschd.msc                                            # Opens the Task Scheduler GUI
```

---

## 🗝️ Registry Commands

> Read, write, and manage the Windows registry — the backbone of OS configuration.

> ⚠️ **Warning:** Incorrect registry edits can break Windows. Always back up before making changes.

```cmd
regedit                                         # Opens the Registry Editor (GUI)

# ── Query (Read) ──────────────────────────────────────────────────
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion   # Lists subkeys of a registry path
reg query HKCU\Software /s                                 # Recursively lists all subkeys under HKCU\Software
reg query HKLM\System\CurrentControlSet\Services          # Lists all installed services in registry
reg query "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion" /v ProductName   # Gets Windows edition name
reg query "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"   # Shows programs that run at user login
reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"   # Shows programs that run at system startup
reg query HKLM /f "password" /t REG_SZ /s     # Searches the entire HKLM hive for "password" strings

# ── Add / Modify ──────────────────────────────────────────────────
reg add "HKCU\Software\MyApp" /v Setting1 /t REG_SZ /d "Value" /f     # Adds a string value to the registry
reg add "HKCU\Software\MyApp" /v Count /t REG_DWORD /d 1 /f           # Adds a DWORD (number) value
reg add "HKLM\Software\MyKey" /f                                        # Creates a new registry key

# ── Delete ────────────────────────────────────────────────────────
reg delete "HKCU\Software\MyApp" /v Setting1 /f    # Deletes a specific value from the registry
reg delete "HKCU\Software\MyApp" /f                # Deletes an entire registry key and all its values

# ── Export & Import (Backup/Restore) ─────────────────────────────
reg export HKLM\SOFTWARE\MyApp backup.reg           # Exports a registry key to a .reg file (backup)
reg import backup.reg                               # Imports/restores a registry key from a .reg file
reg save HKLM hklm_backup.hiv                       # Saves a hive to a binary file (full backup)
reg load HKLM\TEMP C:\hive.hiv                      # Loads a registry hive from a file (forensics)
reg unload HKLM\TEMP                                # Unloads a loaded registry hive

# ── Useful Forensic Registry Keys ────────────────────────────────
# Startup programs (persistence locations — check for malware):
# HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
# HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
# HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
# Recently typed URLs in the Run dialog:
# HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RunMRU
# Recent files opened by the user:
# HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
# USB devices ever connected:
# HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR
```

---

## 📜 Event Log Management

> Query, filter, and clear Windows event logs — essential for incident response and DFIR.

```cmd
eventvwr                                        # Opens Event Viewer GUI
eventvwr /l:<logname>                           # Opens Event Viewer to a specific log

# ── wevtutil — Command-line Event Log Tool ───────────────────────
wevtutil el                                     # Lists all available event logs on the system
wevtutil gl System                              # Shows info about the System log (size, path, etc.)
wevtutil qe System /c:20 /f:text               # Shows the last 20 events in the System log as text
wevtutil qe Security /c:50 /f:text             # Shows the last 50 Security log events
wevtutil qe System /q:"*[System[EventID=41]]" /f:text   # Filters events by Event ID (e.g. 41 = kernel crash)
wevtutil qe Security /q:"*[System[EventID=4625]]" /f:text  # Failed login attempts (Event ID 4625)
wevtutil qe Security /q:"*[System[EventID=4624]]" /f:text  # Successful logins (Event ID 4624)
wevtutil qe Security /q:"*[System[EventID=4720]]" /f:text  # New user account created (Event ID 4720)
wevtutil qe Security /q:"*[System[EventID=4732]]" /f:text  # User added to admin group (Event ID 4732)
wevtutil cl System                              # Clears the System event log (leaves a record that it was cleared)
wevtutil cl Security                            # Clears the Security event log
wevtutil cl Application                         # Clears the Application event log
wevtutil epl System C:\logs\system_export.evtx # Exports the System log to a file (for analysis)

# ── Common Important Event IDs ────────────────────────────────────
# 4624  - Successful user logon
# 4625  - Failed logon attempt (wrong password, brute force)
# 4634  - User logoff
# 4648  - Logon with explicit credentials (runas)
# 4672  - Special privileges assigned (admin logon)
# 4688  - New process created (process tracking)
# 4698  - Scheduled task created
# 4699  - Scheduled task deleted
# 4702  - Scheduled task modified
# 4720  - New user account created
# 4722  - User account enabled
# 4725  - User account disabled
# 4726  - User account deleted
# 4732  - User added to security-enabled local group
# 4740  - User account locked out
# 4776  - NTLM authentication attempted
# 7045  - New service installed (common malware indicator)
# 1102  - Audit log cleared (possible evidence of tampering)
```

---

## 🛡️ Malware & Defender Tools

> Windows Defender commands and key security enforcement settings.

```cmd
# ── Windows Defender (CMD) ────────────────────────────────────────
explorer ms-settings:windowsdefender            # Opens Windows Security settings
MpCmdRun -Scan -ScanType 1                      # Quick scan using Windows Defender
MpCmdRun -Scan -ScanType 2                      # Full scan using Windows Defender
MpCmdRun -Scan -ScanType 3 -File C:\path        # Custom scan of a specific file or folder
MpCmdRun -UpdateSignatures                      # Updates Defender virus definitions
MpCmdRun -GetFiles                              # Collects support logs for Defender
MpCmdRun -RemoveDefinitions -All                # Removes all virus definition files (emergency reset)

# ── Password Policy ───────────────────────────────────────────────
net accounts /minpwlen:12                       # Sets minimum password length to 12
net accounts /maxpwage:30                       # Forces password change every 30 days
net accounts /minpwage:1                        # Minimum days before a password can be changed
net accounts /lockoutthreshold:5                # Locks account after 5 failed attempts
net accounts /lockoutduration:30                # Locked account stays locked for 30 minutes

# ── Security Check Tips ───────────────────────────────────────────
# Combine these for a quick system security check:
#   tasklist /svc       → check running processes and services
#   netstat -b          → check what executables have open network connections
#   schtasks /query /fo list /v  → check for suspicious scheduled tasks
#   reg query "HKLM\...\Run"     → check startup registry keys
#   wevtutil qe Security /q:"...[EventID=4625]"  → check for failed logins
```

---

## 💙 PowerShell Admin Tools

> PowerShell provides powerful, scriptable versions of CMD commands — preferred for automation.

```powershell
# ── System Info ───────────────────────────────────────────────────
Get-ComputerInfo                                    # Full hardware and OS summary
Get-WmiObject Win32_OperatingSystem                 # Detailed OS information (build, version, etc.)
Get-WmiObject Win32_ComputerSystem                  # Hardware details (RAM, manufacturer, model)
Get-WmiObject Win32_Processor                       # CPU details (name, cores, speed)
Get-WmiObject Win32_PhysicalMemory                  # RAM details (size, speed, slot)
Get-WmiObject Win32_BIOS                            # BIOS information (version, serial number)
Get-Date                                            # Shows current date and time
[System.Environment]::OSVersion                     # Shows the OS version object
$env:COMPUTERNAME                                   # Shows computer name as a variable
$env:USERNAME                                       # Shows current username as a variable

# ── Users & Groups ────────────────────────────────────────────────
Get-LocalUser                                       # Lists all local user accounts
Get-LocalUser | Where {$_.Enabled -eq $true}        # Shows only enabled user accounts
Get-LocalGroup                                      # Lists all local groups
Get-LocalGroupMember Administrators                 # Shows all members of the Administrators group
New-LocalUser -Name "NewUser" -NoPassword           # Creates a new local user with no password
Enable-LocalUser -Name Administrator                # Enables the local Administrator account
Disable-LocalUser -Name Guest                       # Disables the Guest account
Remove-LocalUser -Name "OldUser"                    # Deletes a local user

# ── Processes ────────────────────────────────────────────────────
Get-Process                                         # Lists all running processes
Get-Process | Sort-Object CPU -Descending | Select -First 10  # Top 10 CPU-hungry processes
Get-Process | Sort-Object WS -Descending | Select -First 10   # Top 10 memory-hungry processes
Get-Process -Name notepad                           # Gets info on a specific process by name
Stop-Process -Name notepad                          # Stops a process by name
Stop-Process -Id 1234                               # Stops a process by PID
Stop-Process -Name malware -Force                   # Force-stops a process

# ── Services ──────────────────────────────────────────────────────
Get-Service                                         # Lists all services
Get-Service | Where {$_.Status -eq "Running"}       # Lists only running services
Get-Service | Where {$_.Status -eq "Stopped"}       # Lists only stopped services
Get-Service -Name Spooler                           # Gets the status of a specific service
Start-Service -Name Spooler                         # Starts a service
Stop-Service -Name Spooler                          # Stops a service
Restart-Service -Name Spooler                       # Restarts a service
Set-Service -Name Spooler -StartupType Disabled     # Disables a service from auto-starting

# ── Network ───────────────────────────────────────────────────────
Get-NetAdapter                                      # Shows all network adapters and their status
Get-NetIPAddress                                    # Shows all IP addresses on all adapters
Get-NetIPConfiguration                              # Shows full network config per adapter
Get-NetRoute                                        # Shows the routing table
Get-DnsClientCache                                  # Shows the local DNS cache
Clear-DnsClientCache                                # Clears the DNS cache
Test-Connection google.com                          # Tests network connectivity (like ping)
Test-Connection google.com -Count 10                # Sends 10 pings to google.com
Test-NetConnection google.com -Port 443             # Tests if a specific TCP port is reachable
Resolve-DnsName google.com                          # Performs a DNS lookup

# ── Files & Storage ───────────────────────────────────────────────
Get-ChildItem C:\                                   # Lists files and folders (like dir)
Get-ChildItem C:\ -Recurse                          # Lists all files recursively
Get-ChildItem C:\ -Recurse -Filter *.log            # Finds all .log files recursively
Get-ChildItem C:\ -Hidden                           # Lists hidden files and folders
Get-Item C:\Windows\System32\notepad.exe            # Gets detailed info about a specific file
Get-FileHash C:\file.exe -Algorithm SHA256          # Gets the SHA-256 hash of a file
Get-Disk                                            # Shows all physical disks
Get-Partition                                       # Shows all partitions on all disks
Get-Volume                                          # Shows all volumes (drives) and their sizes
Get-PSDrive                                         # Shows all drives including network and registry

# ── Security & Logs ───────────────────────────────────────────────
Get-EventLog -LogName System -Newest 20             # Shows the 20 most recent System log events
Get-EventLog -LogName Security -Newest 50           # Shows the 50 most recent Security events
Get-EventLog -LogName Security -InstanceId 4625 -Newest 20  # Shows recent failed login events
Get-EventLog -LogName Security -InstanceId 4624 -Newest 20  # Shows recent successful logins
Get-WinEvent -LogName Security -MaxEvents 100       # Gets Security events (newer PowerShell method)
Get-HotFix                                          # Lists all installed Windows updates/patches
Get-HotFix | Sort InstalledOn -Descending           # Shows the most recently installed updates first

# ── Scheduled Tasks ───────────────────────────────────────────────
Get-ScheduledTask                                   # Lists all scheduled tasks
Get-ScheduledTask | Where {$_.State -eq "Ready"}    # Shows only enabled tasks
Get-ScheduledTask -TaskName "MyTask"                # Gets a specific task
Start-ScheduledTask -TaskName "MyTask"              # Runs a scheduled task immediately
Stop-ScheduledTask -TaskName "MyTask"               # Stops a running scheduled task
Disable-ScheduledTask -TaskName "MyTask"            # Disables a scheduled task
Enable-ScheduledTask -TaskName "MyTask"             # Re-enables a disabled task
Unregister-ScheduledTask -TaskName "MyTask" -Confirm:$false  # Deletes a task permanently

# ── Registry ──────────────────────────────────────────────────────
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion"   # Gets Windows version info from registry
Get-ItemProperty "HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"  # Gets user startup programs
Set-ItemProperty -Path "HKCU:\Software\MyApp" -Name "Setting" -Value "1"  # Sets a registry value
New-Item -Path "HKCU:\Software\MyNewKey"                                 # Creates a new registry key
Remove-Item -Path "HKCU:\Software\MyNewKey" -Recurse                     # Deletes a registry key

# ── Misc ──────────────────────────────────────────────────────────
Get-ChildItem Env:                                  # Lists all environment variables
Get-Command *network*                               # Finds commands related to networking
Get-Help Get-Process -Full                          # Shows full help for a cmdlet
Get-Help Get-Process -Examples                      # Shows usage examples for a cmdlet
Set-ExecutionPolicy RemoteSigned                    # Allows locally-created scripts to run
Get-ExecutionPolicy                                 # Shows the current script execution policy
Get-WindowsFeature                                  # Lists available Windows features (Server only)
Restart-Computer -Force                             # Force restarts the computer immediately
```

---

## 🔴 CMD Tips & Tricks

> Productivity shortcuts and power-user tricks for the command line.

```cmd
# ── Output Redirection ────────────────────────────────────────────
command > output.txt                # Saves command output to a file (overwrites)
command >> output.txt               # Appends command output to a file
command 2> errors.txt               # Saves only error output to a file
command > output.txt 2>&1           # Saves both normal output and errors to a file
command | more                      # Pipes output through a pager (read page by page)
command | find "keyword"            # Filters output to only show lines containing a keyword
command | findstr "pattern"         # Filters output using a pattern (more powerful than find)
command | clip                      # Copies command output directly to the clipboard

# ── Chaining Commands ─────────────────────────────────────────────
command1 & command2                 # Runs both commands regardless of whether the first succeeded
command1 && command2                # Runs command2 ONLY if command1 succeeded
command1 || command2                # Runs command2 ONLY if command1 failed

# ── Variables & Scripting ─────────────────────────────────────────
set myvar=Hello                     # Creates a variable named myvar
echo %myvar%                        # Prints the value of myvar
set /p name=Enter your name:        # Prompts the user to input a value
set /a result=5+3                   # Performs arithmetic and stores the result
for %i in (*.txt) do echo %i        # Loops through all .txt files in the current directory

# ── History & Navigation ──────────────────────────────────────────
doskey /history                     # Shows all previously typed commands in this session
F7                                  # Opens an interactive history popup in CMD
cls                                 # Clears the screen
help                                # Lists all available CMD commands
<command> /?                        # Shows help for any command (e.g. netstat /?)
pushd <path>                        # Saves current dir and changes to a new one
popd                                # Returns to the directory saved by pushd
color 0A                            # Changes CMD color (0=black bg, A=green text)
title My Terminal                   # Sets a custom title for the CMD window
prompt $P$G                         # Sets the prompt to show path + > (default)
mode con cols=120 lines=50          # Resizes the CMD window

# ── Useful Shortcuts ──────────────────────────────────────────────
# Tab             → Auto-complete file/folder names
# Ctrl+C          → Cancels the running command
# Ctrl+Z          → Sends EOF signal
# Up/Down arrows  → Cycle through command history
# F3              → Repeats the last command
# Alt+F7          → Clears CMD command history
```

---

## 🧰 Misc & Utilities

> Quick shortcuts to open built-in Windows tools from Run (`Win+R`) or CMD.

```cmd
# ── System Tools ─────────────────────────────────────────────────
msinfo32                # System Information (full hardware & software details)
dxdiag                  # DirectX Diagnostic Tool (GPU, sound, display info)
msconfig                # System Configuration (startup programs, boot options)
taskschd.msc            # Task Scheduler
compmgmt.msc            # Computer Management
devmgmt.msc             # Device Manager
eventvwr.msc            # Event Viewer
regedit                 # Registry Editor
mmc                     # Microsoft Management Console
perfmon.msc             # Performance Monitor
resmon                  # Resource Monitor
gpedit.msc              # Local Group Policy Editor
secpol.msc              # Local Security Policy
lusrmgr.msc             # Local Users and Groups Manager

# ── Control Panel Shortcuts ───────────────────────────────────────
control                 # Opens Control Panel
control printers        # Printers and Scanners
control userpasswords2  # Advanced User Accounts
control update          # Windows Update
ncpa.cpl               # Network Connections
inetcpl.cpl            # Internet Options
appwiz.cpl             # Programs and Features (install/uninstall)
timedate.cpl           # Date and Time settings
desk.cpl               # Display Settings
main.cpl               # Mouse Settings
sysdm.cpl              # System Properties (computer name, environment variables)
firewall.cpl           # Windows Defender Firewall
powercfg.cpl           # Power Options
hdwwiz.cpl             # Add Hardware Wizard
joy.cpl                # Game Controllers

# ── Built-in Apps ─────────────────────────────────────────────────
calc                    # Calculator
notepad                 # Notepad
mspaint                 # Microsoft Paint
wordpad / write         # WordPad
snippingtool            # Snipping Tool (screenshots)
osk                     # On-Screen Keyboard
magnify                 # Magnifier
narrator                # Windows Narrator (screen reader)
charmap                 # Character Map (special symbols)
cleanmgr                # Disk Cleanup
mstsc                   # Remote Desktop Connection
wf.msc                  # Windows Firewall with Advanced Security
```

---

## 📌 Quick Reference — Key Shortcuts

| Goal | Command |
|------|---------|
| Who am I? | `whoami /all` |
| What OS? | `wmic os get name,version` |
| Who else is logged in? | `query user` |
| What's my IP? | `ipconfig /all` |
| Who's on my network? | `arp -a` |
| What ports are open? | `netstat -ano` |
| What programs are running? | `tasklist /v` |
| What services are running? | `sc query state=all` |
| What's scheduled to run? | `schtasks /query /fo list /v` |
| What programs run at startup? | `reg query HKLM\...\CurrentVersion\Run` |
| Any failed logins? | `wevtutil qe Security /q:"*[System[EventID=4625]]"` |
| Is the firewall on? | `netsh advfirewall show allprofiles` |
| Check disk health | `chkdsk C: /f /r` |
| Check system file integrity | `sfc /scannow` |
| Hash a file | `certutil -hashfile <file> sha256` |

---

## 📌 Notes

- Commands with `<angle brackets>` → replace the content, **do not include** the `<` or `>`
- Many commands require **Administrator privileges** → right-click CMD → *Run as Administrator*
- PowerShell commands are case-insensitive but conventionally written in `PascalCase`
- Use `/?` after any CMD command for full help: `netstat /?` , `schtasks /?`
- Use `Get-Help <cmdlet> -Examples` in PowerShell for usage examples
- To save output to a file: `command > output.txt`
- To run as another user: `runas /user:administrator cmd`

---

## 👤 Author

**Saharia Hassan Safin**  
Cybersecurity enthusiast from Dhaka, Bangladesh 🇧🇩  
Currently learning offensive and defensive security, building secure tools, and sharing knowledge.

🔗 [GitHub](https://github.com/Safin313-stack) · [Facebook](https://www.facebook.com/share/14EQjp8qPeE/)

---

<div align="center">

⭐ **If this helped you, star the repo — it helps others find it too!**

</div>
