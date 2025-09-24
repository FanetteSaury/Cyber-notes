#THM #Cybersecurity101 #Cybersecurity101-CommandLine
## Basic System Information
- `set # see env variables`
- `ver # OS version`
- `systeminfo`
-  `help` - Provides help information for a specific command
- `cls` - Clears the Command Prompt screen.
- **`/?` can be used with most commands to display a help page.**
## Network Troubleshooting
- `ipconfig`
- `ping`
- `nslookup` ❤️ 👉 to get the IP address of a domain name
	- - `-a` displays all established connections and listening ports
	- `-p` shows the program associated with each listening port and established connection
	- `-o` reveals the process ID (PID) associated with the connection
	- `-n` uses a numerical form for addresses and port numbers
	- => We combine these four options and execute the `netstat -abon` command. The result is quite long, but we display the first few lines in the terminal below. It is clear now that the executable `sshd.exe` is responsible for listening for incoming connections on port 22, as shown in the first line. We can also see the process ID (PID) associated with each connection. ```shell-session
```
C:\>netstat -apon
Active Connections
[...]
  TCP    0.0.0.0:49669          0.0.0.0:0              LISTENING       2036
 [spoolsv.exe]
  TCP    0.0.0.0:49670          0.0.0.0:0              LISTENING       584 
 Can not obtain ownership information
  TCP    0.0.0.0:49686          0.0.0.0:0              LISTENING       592
 [lsass.exe]
  TCP    10.10.230.237:22       10.11.81.126:53486     ESTABLISHED     2116 
 [sshd.exe]
 [...]
```
## File and Disk Management
- `dir` = "ls"
	- `dir /a`
	- `dir /s` display files in current and subdirectories
- `del` / `erase`
- `move`
- `copy
- `type`
## Task and Process Management
Tool 👉`tasklist`

### example 
```  C:\>tasklist Image Name PID Session Name Session# Mem Usage ========================= ======== ================ =========== ============ System Idle Process 0 Services 0 8 K System 4 Services 0 88 K Registry 84 Services 0 50,700 K smss.exe 276 Services 0 1,132 K csrss.exe 372 Services 0 5,264 K wininit.exe 448 Services 0 6,892 K csrss.exe 456 Console 1 5,028 K winlogon.exe 516 Console 1 11,144 K services.exe 584 Services 0 7,492 K lsass.exe 592 Services 0 16,108 K svchost.exe 704 Services 0 23,432 K fontdrvhost.exe 736 Console 1 4,256 K [...]
	  ```
## Lexicon
- netstat -apon
### `[...] | more`
You can pipe it through `more` if the output is too long. Then, you can view it page after page by pressing the space bar button. To demonstrate this, try running `driverquery` and compare it with running `driverquery | more`. In the latter, you can display the output page by page and you can exit it using `CTRL + C`.

- `chkdsk`: checks the file system and disk volumes for errors and bad sectors.
- `driverquery`: displays a list of installed device drivers.
- `sfc /scannow`: scans system files for corruption and repairs them if possible.