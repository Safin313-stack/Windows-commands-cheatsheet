# 🖥️ Windows Command Line — Complete Cybersecurity & Admin Cheatsheet

> A practical, well-organized reference of Windows CMD and PowerShell commands for cybersecurity learners, system administrators, and IT enthusiasts. From basic recon to forensics — all in one place.

---

## 📋 Table of Contents

- [🔍 System Information](#-system-information)
- [👤 User Account Management](#-user-account-management)
- [🌐 Network Commands](#-network-commands)
- [📁 Files & Directories](#-files--directories)
- [🔎 Search & Forensics](#-search--forensics)
- [⚙️ Process & Service Control](#-process--service-control)
- [🔐 Security & Permissions](#-security--permissions)
- [💽 Disk & System Utilities](#-disk--system-utilities)
- [🔄 Windows Update & Activation](#-windows-update--activation)
- [🚀 Boot & Startup Repair](#-boot--startup-repair)
- [🛡️ Malware & Defender Tools](#-malware--defender-tools)
- [💙 PowerShell Admin Tools](#-powershell-admin-tools)
- [🧰 Misc & Utilities](#-misc--utilities)

---

## 🔍 System Information

Basic commands to quickly profile a machine — useful for initial recon or troubleshooting.

```cmd
whoami                          # Shows the currently logged-in user
hostname                        # Shows the computer's name
systeminfo                      # Full device and OS details (like the "About" section)
ver                             # Shows the Windows version
set                             # Lists all environment variables (system-wide saved values)
echo %username%                 # Prints the current username
date /t                         # Shows today's date without prompting to change it
time /t                         # Shows the current time without prompting to change it
driverquery                     # Lists all installed device drivers
tasklist                        # Shows all currently running processes
tasklist /svc                   # Same as tasklist but also shows services inside each process
wmic os get name                # Shows operating system name and info
wmic cpu get name               # Shows the CPU model name
wmic bios get serialnumber      # Shows the BIOS serial number (useful for asset tracking)
wmic qfc                        # Lists installed Windows updates (may not work on newer Windows)
```

---

## 👤 User Account Management

Manage local users and groups — essential for access control and privilege escalation awareness.

```cmd
net user                                        # Lists all local user accounts
net user <username>                             # Shows detailed info about a specific user
net user <username> /delete                     # Deletes a user account
net user administrator /active:yes              # Enables the built-in Administrator account
net user administrator /active:no               # Disables the built-in Administrator account
net user <username> /active:no                  # Disables a specific user account
net user <username> *                           # Prompts to change a user's password
net localgroup                                  # Lists all local groups
net localgroup administrators <username> /add   # Adds a user to the Administrators group
net localgroup <groupname>                      # Shows members and details of a specific group
whoami /groups                                  # Shows which groups the current user belongs to
whoami /priv                                    # Shows special privileges assigned to the current user
query user                                      # Shows all currently logged-in users
net accounts                                    # Shows and helps manage the password policy
net accounts /minpwlen:8                        # Sets minimum password length to 8 characters
net accounts /maxpwage:30                       # Sets password expiry to 30 days
control userpasswords2                          # Opens the advanced user accounts settings window
lusrmgr.msc                                     # Opens the Local Users and Groups Manager (GUI)
rundll32.exe user32.dll,LockWorkStation         # Instantly locks the workstation
taskmgr                                         # Opens Task Manager
eventvwr                                        # Opens Event Viewer — used to view system and security logs
```

---

## 🌐 Network Commands

Understand, inspect, and manipulate network configuration — critical for both defense and offense.

```cmd
ipconfig                                        # Shows basic IP address information
ipconfig /all                                   # Shows full network configuration (MAC, DNS, DHCP, etc.)
ipconfig /release                               # Releases the current IP address
ipconfig /renew                                 # Requests a new IP address from DHCP
ipconfig /displaydns                            # Shows the local DNS cache (run ping first if cache is empty)
ipconfig /flushdns                              # Clears the DNS cache

netsh winsock reset                             # Resets Winsock (the list of network protocol handlers)
netsh int ip reset                              # Resets TCP/IP stack to default
netsh wlan show profile                         # Lists all saved Wi-Fi profiles
netsh wlan delete profile name=<profilename>    # Deletes a saved Wi-Fi profile
netsh interface show interface                  # Shows all network interfaces and their status
netsh advfirewall reset                         # Resets all firewall rules to default
netsh firewall show state                       # Shows current firewall state

getmac                                          # Shows the MAC (physical hardware) address of network adapters
arp -a                                          # Shows all devices your computer has recently communicated with on the local network
route print                                     # Shows the routing table — how packets are directed to destinations
netstat -an                                     # Shows all active connections and ports being listened to
netstat -ano                                    # Same as above but includes the Process ID (PID) for each connection
netstat -b                                      # Same as -ano but also shows the executable (.exe) responsible

ping <host>                                     # Tests connectivity to a host or website
tracert <host>                                  # Traces the path (hop by hop) packets take to reach a host
pathping <host>                                 # Like tracert but also measures packet loss and latency at each hop
nslookup <domain>                               # Resolves a domain name to its IP address (DNS lookup)

net view                                        # Lists computers and shared resources on the local network
net view \\<target>                             # Shows shared folders on a specific network computer
nbtstat -n                                      # Lists all NetBIOS names registered on the local computer
nbtstat -A <ip>                                 # Shows NetBIOS info for a remote computer by IP
net use                                         # Shows all active network connections and mapped drives
net use \\<ip>\<share>                          # Connects to a shared folder on a remote computer

net stop dhcp                                   # Stops the DHCP service
net start dhcp                                  # Starts the DHCP service
```

---

## 📁 Files & Directories

Navigate, manage, and manipulate the file system.

```cmd
dir                             # Lists all files and folders in the current directory
dir /a                          # Lists everything including hidden files
tree                            # Displays directory structure as a visual tree
cd <directory>                  # Changes the current directory
mkdir <foldername>              # Creates a new folder
rmdir <foldername>              # Removes an empty folder
rmdir /s /q <foldername>        # Removes a folder and all its contents silently
del <filename>                  # Deletes a file
copy <filename> <destination>   # Copies a file to a destination
move <filename> <destination>   # Moves a file to a destination
rename <filename> <newname>     # Renames a file
type file.txt                   # Prints the full content of a text file
more file.txt                   # Reads a text file page by page (useful for large files)
attrib                          # Shows file attributes (hidden, system, read-only, etc.)
attrib +h <file>                # Hides a file by setting its hidden attribute
where <filename>                # Finds and shows the full path of a file or executable
```

---

## 🔎 Search & Forensics

Find files, compare them, hash them, and investigate storage — key skills in digital forensics.

```cmd
find "text" file.txt                    # Searches for a specific word inside a file
findstr "search phrase" file.txt        # Searches for a phrase or multiple words in a file (more powerful than find)
fc file1 file2                          # Compares two files and shows differences

certutil -hashfile <file> sha256        # Generates a SHA-256 hash (digital fingerprint) of a file
                                        # Use this to verify file integrity

cipher /c <file>                        # Shows encryption info for a file (EFS encrypted files)
cipher /w:C                             # Securely wipes all free space on drive C (prevents file recovery)
compact                                 # Checks or applies NTFS compression on files without zipping them
dir /s <filename>                       # Searches for a file recursively in all subdirectories
```

---

## ⚙️ Process & Service Control

Monitor, start, stop, and kill processes and services — essential for malware analysis and incident response.

```cmd
tasklist                        # Lists all running processes with their PID
taskkill /PID 1234              # Terminates the process with PID 1234
taskkill /IM file.exe /F        # Force-kills a process by its executable name

sc query                        # Lists all currently running services
sc query state=all              # Lists all services regardless of state (running, stopped, paused, etc.)
```

---

## 🔐 Security & Permissions

Control who can access what — core to understanding Windows security and privilege management.

```cmd
icacls <file>                           # Shows file permissions (who can read, write, execute)
icacls <file> /grant <user>:F           # Grants full access to a user for a specific file
takeown /f <file>                       # Takes ownership of a file (needed before changing its permissions)
auditpol /get /category:*               # Shows all auditing categories and whether success/failure is being logged
secedit /export /cfg output.cfg         # Exports the current local security policy to a file
gpresult /r                             # Shows which Group Policy settings are applied to the current user/machine
gpupdate /force                         # Immediately reapplies all Group Policy settings
logoff                                  # Logs off the current user session
shutdown /s /t 0                        # Shuts down the computer immediately
shutdown /r /t 0                        # Restarts the computer immediately
```

---

## 💽 Disk & System Utilities

Repair, manage, and optimize storage and the Windows system itself.

```cmd
chkdsk                                          # Checks the disk for errors
chkdsk C: /f /r                                 # Checks drive C, fixes errors, and recovers readable data
diskpart                                        # Opens the disk partition manager (CLI)
diskmgmt.msc                                    # Opens Disk Management (GUI)
msconfig                                        # Opens System Configuration (startup, boot options)
services.msc                                    # Opens the Services manager (GUI)
sfc /scannow                                    # Scans and repairs corrupted Windows system files
dism /online /cleanup-image /restorehealth      # Repairs the Windows image (deeper repair than sfc)
mountvol                                        # Shows or manages volume mount points
cleanmgr                                        # Opens Disk Cleanup to free up space
powercfg /batteryreport                         # Generates a detailed battery health report (saved as HTML)
defrag C:                                       # Defragments drive C (reorganizes fragmented files for speed)
format D: /fs:ntfs                              # Formats drive D with the NTFS file system (WARNING: erases all data)

robocopy C:\Source D:\Backup /E                 # Copies all files and folders (including empty folders) from Source to Backup
xcopy source destination /E /H /C /I           # Copies all files including hidden/system files, continues on errors

del /f /s /q C:\Windows\Temp\*.*               # Silently deletes all temp files including read-only ones
attrib -h -r -s /s /d *.*                       # Removes hidden, read-only, and system attributes recursively
fsutil dirty query C:                           # Checks if drive C has the dirty bit set (indicates possible corruption)
sdelete -p 3 <filename>                         # Securely deletes a file with 3 overwrite passes (requires Sysinternals)
perfmon                                         # Opens Performance Monitor
resmon                                          # Opens Resource Monitor (real-time CPU, memory, disk, network usage)
gpedit.msc                                      # Opens the Group Policy Editor
secpol.msc                                      # Opens Local Security Policy
compmgmt.msc                                    # Opens Computer Management (all-in-one admin console)
sysdm.cpl                                       # Opens System Properties
```

---

## 🔄 Windows Update & Activation

Manage Windows updates and licensing from the command line.

```cmd
wuauclt /detectnow                                      # Forces Windows to check for updates
wuauclt /updatenow                                      # Forces Windows to start downloading and installing updates
usoclient startscan                                     # Scans for available updates (newer Windows)
usoclient startinstall                                  # Installs available updates (newer Windows)
control update                                          # Opens the Windows Update settings panel
slmgr /ipk XXXXX-XXXXX-XXXXX-XXXXX-XXXXX               # Installs a Windows product key
slmgr /ato                                              # Activates Windows using the installed key
slmgr /xpr                                              # Checks the Windows activation/expiry status
slmgr /rearm                                            # Resets the Windows activation grace timer
sc query wuauserv                                       # Checks whether the Windows Update service is running
```

---

## 🚀 Boot & Startup Repair

Fix boot issues and manage boot configuration — critical for recovery scenarios.

```cmd
bcdedit /enum all                               # Displays all boot configuration entries
bootrec /fixmbr                                 # Repairs the Master Boot Record (MBR)
bootrec /fixboot                                # Repairs the boot sector of the active partition
bootrec /scanos                                 # Scans all disks for Windows installations
bootrec /rebuildbcd                             # Rebuilds the Boot Configuration Data (BCD) from scratch
bcdboot C:\Windows                              # Recreates the boot files from the Windows installation
reagentc /enable                                # Enables the Windows Recovery Environment (WinRE)
bcdedit /set {default} safeboot minimal         # Configures Windows to boot into Safe Mode on next restart
bcdedit /deletevalue {default} safeboot         # Removes the Safe Mode boot flag (returns to normal boot)
srttrail.txt                                    # Location of the Startup Repair log file (found in WinRE)
```

---

## 🛡️ Malware & Defender Tools

Commands related to Windows Defender and basic security policy enforcement.

```cmd
explorer ms-settings:windowsdefender            # Opens Windows Security / Defender settings
net accounts /minpwlen:8                        # Enforces a minimum password length of 8 characters
net accounts /maxpwage:30                       # Forces users to change passwords every 30 days
```

> 💡 **Tip:** For deeper malware analysis, combine `tasklist`, `netstat -b`, and `Autoruns` from Sysinternals Suite.

---

## 💙 PowerShell Admin Tools

PowerShell provides more powerful and scriptable versions of many CMD commands.

```powershell
Get-EventLog -LogName System -Newest 20                     # Shows the 20 most recent system log events
Get-Service | Where-Object {$_.Status -eq 'Running'}        # Lists only currently running services
Restart-Service Spooler                                     # Restarts the print spooler service
Stop-Process -Name notepad                                  # Stops any running Notepad process
Get-Process | Sort-Object CPU -Descending | Select -First 10  # Shows the top 10 processes consuming the most CPU
Get-Disk                                                    # Lists all physical disks
Get-NetAdapter                                              # Shows all network adapters and their status
Test-Connection google.com                                  # Tests network connectivity (like ping)
Get-WindowsFeature                                          # Lists all available and installed Windows features
Restart-Computer -Force                                     # Force restarts the computer immediately
Get-ChildItem Env:                                          # Lists all environment variables
Get-Command *network*                                       # Searches for all commands with "network" in the name
Get-Help Get-Process                                        # Displays help documentation for Get-Process
Set-ExecutionPolicy RemoteSigned                            # Allows locally written scripts to run
Get-WmiObject Win32_OperatingSystem                         # Shows detailed operating system information
Get-HotFix                                                  # Lists all installed Windows updates and patches
Get-LocalUser                                               # Lists all local user accounts
Enable-LocalUser -Name Administrator                        # Enables the local Administrator account
Disable-LocalUser -Name Guest                               # Disables the Guest account
Get-ComputerInfo                                            # Shows a full summary of the computer's hardware and OS info
```

---

## 🧰 Misc & Utilities

Handy shortcuts to open built-in Windows tools quickly from Run or CMD.

```cmd
calc                # Opens Calculator
notepad             # Opens Notepad
mspaint             # Opens Microsoft Paint
osk                 # Opens the On-Screen Keyboard
magnify             # Opens the Magnifier tool
snippingtool        # Opens the Snipping Tool for screenshots
write               # Opens WordPad
control printers    # Opens the Printers & Scanners folder
hdwwiz.cpl          # Opens the Add Hardware Wizard
timedate.cpl        # Opens Date and Time settings
ncpa.cpl            # Opens Network Connections
inetcpl.cpl         # Opens Internet Options
main.cpl            # Opens Mouse Settings
desk.cpl            # Opens Display Settings
appwiz.cpl          # Opens Programs and Features (uninstall programs)
joy.cpl             # Opens Game Controllers settings
```

---

## 📌 Notes

- Commands marked with `<angle brackets>` require you to replace that part with your actual value — **do not include the `<` or `>`**.
- Some commands require **Administrator privileges** — right-click CMD and choose *Run as Administrator*.
- PowerShell commands are case-insensitive but conventionally written in PascalCase.
- Use `/?` after any CMD command (e.g., `netstat /?`) to see its full help and options.

---

## 👤 Author

**Saharia Hassan Safin**
Cybersecurity enthusiast from Dhaka, Bangladesh.
🔗 [GitHub Profile](https://github.com/Safin313-stack)

---

> ⭐ If this helped you, consider starring the repository!
