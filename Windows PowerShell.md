#THM #Cybersecurity101 #Cybersecurity101-CommandLine 
## Introduction
PowerShell is a cross-platform **task automation** solution made up of a command-line shell, a scripting language, and a configuration management framework.
- object oriented
- Initially exclusive to Windows, PowerShell has lately expanded to support macOS and Linux
## System and network information
```
PS C:\Users\captain> Get-ComputerInfo WindowsBuildLabEx : 20348.859.amd64fre.fe_release_svc_prod2.220707-1832 WindowsCurrentVersion : 6.3 WindowsEditionId : ServerDatacenter WindowsInstallationType : Server Core WindowsInstallDateFromRegistry : 4/23/2024 6:36:29 PM WindowsProductId : 00454-60000-00001-AA763 WindowsProductName : Windows Server 2022 Datacenter [...]
```
Essential for managing user accounts and understanding the machine’s security configuration, `Get-LocalUser` lists all the local user accounts on the system. The default output displays, for each user, username, account status, and description.```

```
PS C:\Users\captain> Get-LocalUser Name Enabled Description ---- ------- ----------- Administrator True Built-in account for administering the computer/domain captain True The beloved captain of this pirate ship. DefaultAccount False A user account managed by the system. Guest False Built-in account for guest access to the computer/domain WDAGUtilityAccount False A user account managed and used by the system for Windows Defender Application Guard scenarios.
```
Similar to the traditional `ipconfig` command, the following two cmdlets can be used to retrieve detailed information about the system’s network configuration.

`Get-NetIPConfiguration` provides detailed information about the network interfaces on the system, including IP addresses, DNS servers, and gateway configurations.
```
PS C:\Users\captain> Get-NetIPConfiguration InterfaceAlias : Ethernet InterfaceIndex : 5 InterfaceDescription : Amazon Elastic Network Adapter NetProfile.Name : Network 3 IPv4Address : 10.10.178.209 IPv6DefaultGateway : IPv4DefaultGateway : 10.10.0.1 DNSServer : 10.0.0.2
```
In case we need specific details about the IP addresses assigned to the network interfaces, the `Get-NetIPAddress` cmdlet will show details for all IP addresses configured on the system, including those that are not currently active.
```
PS C:\Users\captain> Get-NetIPAddress IPAddress : fe80::3fef:360c:304:64e%5 InterfaceIndex : 5 InterfaceAlias : Ethernet AddressFamily : IPv6 Type : Unicast PrefixLength : 64 PrefixOrigin : WellKnown SuffixOrigin : Link AddressState : Preferred ValidLifetime : Infinite ([TimeSpan]::MaxValue) PreferredLifetime : Infinite ([TimeSpan]::MaxValue) SkipAsSource : False PolicyStore : ActiveStore IPAddress : ::1 InterfaceIndex : 1 InterfaceAlias : Loopback Pseudo-Interface 1 AddressFamily : IPv6 [...] IPAddress : 10.10.178.209 InterfaceIndex : 5 InterfaceAlias : Ethernet AddressFamily : IPv4 [...] IPAddress : 127.0.0.1 InterfaceIndex : 1 InterfaceAlias : Loopback Pseudo-Interface 1 AddressFamily : IPv4 [...]
```
## Scripting
### Invoke command ⚠🌉
`Invoke-Command` is essential for executing commands on remote systems, making it fundamental for system administrators, security engineers and penetration testers. `Invoke-Command` enables efficient remote management and—combining it with scripting—automation of tasks across multiple machines. It can also be used to execute payloads or commands on target systems during an engagement by penetration testers—or attackers alike.

Let us discover some example usage for this powerful cmdlet by consulting the `Get-Help` "examples" page:

Terminal

```powershell
PS C:\Users\captain> Get-Help Invoke-Command -examples

NAME
    Invoke-Command
    
SYNOPSIS
    Runs commands on local and remote computers.
    
    ------------- Example 1: Run a script on a server -------------
    
    Invoke-Command -FilePath c:\scripts\test.ps1 -ComputerName Server01
    
    The FilePath parameter specifies a script that is located on the local computer. The script runs on the remote computer and the results are returned to the local computer.

    --------- Example 2: Run a command on a remote server ---------

    Invoke-Command -ComputerName Server01 -Credential Domain01\User01 -ScriptBlock { Get-Culture }

    The ComputerName parameter specifies the name of the remote computer. The Credential parameter is used to run the command in the security context of Domain01\User01, a user who has permission to run commands. The ScriptBlock parameter specifies the command to be run on the remote computer.

    In response, PowerShell requests the password and an authentication method for the User01 account. It then runs the command on the Server01 computer and returns the result.
[...]
```

The first two examples provided by the `Get-Help` "examples" page and reported above are enough to grasp the simplicity and power of the `Invoke-Command` cmdlet.

The first example shows how the cmdlet can be very easily combined with any custom script to automate tasks on remote computers.

The second example demonstrates that we don't need to know how to script to benefit from the power of `Invoke-Command`. In fact, by appending the `-ScriptBlock { ... }` parameter to the cmdlet's syntax, we can execute any command (or sequence of commands) on the remote computer. The result would be the same as if we were typing the commands in a local PowerShell session on the remote computer itself.

## Lexicon
```powershell
hostname # find hostname
whoami # find username and domain
```