# Invoke-ATTACKAPI
A PowerShell script to interact with the MITRE ATT&amp;CK Framework via its own API in order to gather information about techniques, 
tactics, groups, software and references provided by the MITRE ATT&CK Team @MITREattack.

# Goals
* Provide an easy way to interact with the MITRE ATT&CK Framework via its own API and PowerShell to the community.
* Expedite the acquisition of data from ATT&CK when preparing for a Hunting Campaign.
* Learn PowerShell Dynamic Parameters :) 

# Resources
* [MITRE ATT&CK API](https://attack.mitre.org/wiki/Using_the_API)
* [Semantic MediaWiki API](https://www.semantic-mediawiki.org/wiki/Help:API)
* [Get-ATTack](https://github.com/SadProcessor/SomeStuff/blob/master/Get-ATTaCK.ps1)
  * Walter Legowski [@SadProcessor](https://twitter.com/SadProcessor) 

# Getting Started

## Requirements
* PowerShell version 3+

## Installing /Importing
```
git clone https://github.com/Cyb3rWard0g/Invoke-ATTACKAPI.git
cd Invoke-ATTACKAPI
import-module .\Invoke-ATTACKAPI.ps1

  /$$$$$$  /$$$$$$$$ /$$$$$$$$ /$$$      /$$$$$$  /$$   /$$        /$$$$$$  /$$$$$$$  /$$$$$$
 /$$__  $$|__  $$__/|__  $$__//$$ $$    /$$__  $$| $$  /$$/       /$$__  $$| $$__  $$|_  $$_/
| $$  \ $$   | $$      | $$  |  $$$    | $$  \__/| $$ /$$/       | $$  \ $$| $$  \ $$  | $$
| $$$$$$$$   | $$      | $$   /$$ $$/$$| $$      | $$$$$/        | $$$$$$$$| $$$$$$$/  | $$
| $$__  $$   | $$      | $$  | $$  $$_/| $$      | $$  $$        | $$__  $$| $$____/   | $$
| $$  | $$   | $$      | $$  | $$\  $$ | $$    $$| $$\  $$       | $$  | $$| $$        | $$
| $$  | $$   | $$      | $$  |  $$$$/$$|  $$$$$$/| $$ \  $$      | $$  | $$| $$       /$$$$$$
|__/  |__/   |__/      |__/   \____/\_/ \______/ |__/  \__/      |__/  |__/|__/      |______/

Author: Roberto Rodriguez @Cyb3rWard0g
Version: 0.9 [BETA]

[++] Pulling MITRE ATT&CK Data

```

## Examples
### This query matches all techniques
```
Invoke-ATTACKAPI -Category -Technique

URL             : https://attack.mitre.org/wiki/Technique/T1001
ID              : {T1001}
Tactic          : Command and Control
AnalyticDetails : {Analyze network data for uncommon data flows (e.g., a client sending significantly more data than it receives from a
                  server). Processes utilizing the network that do not normally have network communication or have never been seen befor
                  are suspicious. Analyze packet contents to detect communications that do not follow the expected protocol behavior for
                  the port that is being used.University of Birmingham C2}
RequiresSystem  : {}
FullText        : Technique/T1001
Bypass          : {}
Name            : {Data Obfuscation}
Description     : {Command and control (C2) communications are hidden (but not necessarily encrypted) in an attempt to make the content
                  more difficult to discover or decipher and to make the communication less conspicuous and hide commands from being see
                  This encompasses many methods, such as adding junk data to protocol traffic, using steganography, commingling legitima
                  traffic with C2 communications traffic, or using a non-standard data encoding system, such as a modified Base64 encodi
                  for the message body of an HTTP request.}
Mitigation      : {Network intrusion detection and prevention systems that use network signatures to identify traffic for specific
                  adversary malware can be used to mitigate activity at the network level. Signatures are often for unique indicators
                  within protocols and may be based on the specific obfuscation technique used by a particular adversary or tool, and wi
                  likely be different across various malware families and versions. Adversaries will likely change tool C2 signatures ov
                  time or construct protocols in such a way as to avoid detection by common defensive tools.University of Birmingham C2}
Platform        : {Windows Server 2003, Windows Server 2008, Windows Server 2012, Windows XP...}
Reference       : {University of Birmingham C2, FireEye APT28, Axiom, FireEye APT30...}
URL             : https://attack.mitre.org/wiki/Technique/T1002
ID              : {T1002}
Tactic          : Exfiltration
AnalyticDetails : {Compression software and compressed files can be detected in many ways. Common utilities that may be present on the
                  system or brought in by an adversary may be detectable through process monitoring and monitoring for command-line
                  arguments for known compression utilities. This may yield a significant amount of benign events, depending on how
                  systems in the environment are typically used.
```
### This query matches the page Technique with ID T1014
```
Invoke-ATTACKAPI -Category -Technique -ID T1014

URL             : https://attack.mitre.org/wiki/Technique/T1014
ID              : {T1014}
Tactic          : Defense Evasion
AnalyticDetails : {Some rootkit protections may be built into anti-virus or operating system software. There are dedicated rootkit
                  detection tools that look for specific types of rootkit behavior. Monitor for the existence of unrecognized DLLs,
                  devices, services, and changes to the MBR.Wikipedia Rootkit}
RequiresSystem  : {}
FullText        : Technique/T1014
Bypass          : {Anti-virus, File monitoring, Host intrusion prevention systems, Process whitelisting...}
Name            : {Rootkit}
Description     : {Rootkits are programs that hide the existence of malware by intercepting and modifying operating system API calls t
                  supply system information. Rootkits or rootkit enabling functionality may reside at the user or kernel level in the
                  operating system or lower, to include a [[Technique/T1062|Hypervisor]], Master Boot Record, or the
                  [[Technique/T1019|System Firmware]].Wikipedia Rootkit
                  Adversaries may use rootkits to hide the presence of programs, files, network connections, services, drivers, and ot
                  system components.}
Mitigation      : {Identify potentially malicious software that may contain rootkit functionality, and audit and/or block it by using
                  whitelistingBeechey 2010 tools, like AppLocker,Windows Commands JPCERTNSA MS AppLocker or Software Restriction
                  PoliciesCorio 2008 where appropriate.TechNet Applocker vs SRP}
Platform        : {Windows Server 2003, Windows Server 2008, Windows Server 2012, Windows XP...}
Reference       : {Wikipedia Rootkit, Beechey 2010, Windows Commands JPCERT, NSA MS AppLocker...}
```

### This query matches against all the group that use a specific software (in this case Cobalt Strike). SYNTAX: "Software: \<tool name>"
```
Invoke-ATTACKAPI -Category -Group -Tool "Software: Cobalt Strike"

URL           : https://attack.mitre.org/wiki/Group/G0050
Alias         : {APT32, OceanLotus Group}
ID            : {G0050}
Tool          : {Software: Cobalt Strike, Software: KOMPROGO, Software: WINDSHIELD, Software: SOUNDBITE...}
TechniqueID   : {Technique/T1053, Technique/T1117, Technique/T1086, Technique/T1094...}
FullText      : Group/G0050
Name          : {APT32}
Description   : {[[Group/G0050|APT32]] is a threat group that has been active since at least 2014. The group has targeted multiple private
                sector industries as well as with foreign governments, dissidents, and journalists. The group's operations are aligned
                with Vietnamese state interests.FireEye APT32 May 2017}
TechniqueName : {Scheduled Task, Regsvr32, PowerShell, Custom Command and Control Protocol...}
Reference     : {FireEye APT32 May 2017, GitHub Malleable C2, GitHub Invoke-Obfuscation}
```

### [BETA] Exporting custom results to a CSV
```
PS C:\HIVE\github\Invoke-ATTACKAPI> Invoke-ATTACKAPI -Category -Technique | where-object -Property ID -GE "T1134" | select @{Name="Name"; Ex
pression={$_.Name -join ","}}, @{Name="Tactic"; Expression={$_.Tactic -join ","}}, @{Name ="ID"; Expression={$_.ID -join ","}}, @{Name="Desc
ription"; Expression={$_.Description -join ","}}, @{Name="Analyticdetails"; Expression={$_.AnalyticDetails -join ","}}, @{Name="DataSource";
 Expression={$_.DataSource -join ","}}  | export-csv F:\wardog\scripts\demo6.csv -NoTypeInformation
```
### Showing an up to date ATT&CK Matrix for Enterprise
```
Invoke-ATTACKAPI -Matrix | select Persistence, 'Privilege Escalation', 'Defense Evasion','Credential Access', Discovery, 'Lateral Movement', Execution, Collection, Exfiltration, 'Command and Control' | ft

Persistence                                           Privilege Escalation                  Defense Evasion                         Credential Access                      Discovery                              Lateral Movement                    Execution
-----------                                           --------------------                  ---------------                         -----------------                      ---------                              ----------------                    ---------
.bash_profile and .bashrc                             Access Token Manipulation             Access Token Manipulation               Account Manipulation                   Account Discovery                      AppleScript                         AppleScript
Accessibility Features                                Accessibility Features                Binary Padding                          Bash History                           Application Window Discovery           Application Deployment Software     Application Shimming
AppInit DLLs                                          AppInit DLLs                          Bypass User Account Control             Brute Force                            File and Directory Discovery           Exploitation of Vulnerability       Command-Line Interface
Application Shimming                                  Application Shimming                  Clear Command History                   Create Account                         Network Service Scanning               Logon Scripts                       Execution through API
Authentication Package                                Bypass User Account Control           Code Signing                            Credential Dumping                     Network Share Discovery                Pass the Hash                       Execution through Mod...
Bootkit                                               DLL Injection                         Component Firmware                      Credentials in Files                   Peripheral Device Discovery            Pass the Ticket                     Graphical User Interface
Change Default File Association                       DLL Search Order Hijacking            Component Object Model Hijacking        Exploitation of Vulnerability          Permission Groups Discovery            Remote Desktop Protocol             InstallUtil
Component Firmware                                    Dylib Hijacking                       Deobfuscate/Decode Files or Information Input Capture                          Process Discovery                      Remote File Copy                    Launchctl
Component Object Model Hijacking                      Exploitation of Vulnerability         Disabling Security Tools                Input Prompt                           Query Registry                         Remote Services                     PowerShell
Cron Job                                              File System Permissions Weakness      DLL Injection                           Keychain                               Remote System Discovery                Replication Through Removable Media Process Hollowing
DLL Search Order Hijacking                            Launch Daemon                         DLL Search Order Hijacking              Network Sniffing                       Security Software Discovery            Shared Webroot                      Regsvcs/Regasm
Dylib Hijacking                                       Local Port Monitor                    DLL Side-Loading                        Private Keys                           System Information Discovery           Taint Shared Content                Regsvr32
External Remote Services                              New Service                           Exploitation of Vulnerability           Securityd Memory                       System Network Configuration Discovery Third-party Software                Rundll32
File System Permissions Weakness                      Path Interception                     File Deletion                           Two-Factor Authentication Interception System Network Connections Discovery   Windows Admin Shares                Scheduled Task
Hidden Files and Directories                          Plist Modification                    File System Logical Offsets                                                    System Owner/User Discovery            Windows Remote Management           Scripting
Hypervisor                                            Scheduled Task                        Gatekeeper Bypass                                                              System Service Discovery                                                   Service Execution
Launch Agent                                          Service Registry Permissions Weakness Hidden Files and Directories                                                   System Time Discovery                                                      Source
Launch Daemon                                         Setuid and Setgid                     Hidden Users                                                                                                                                              Space after Filename
Launchctl                                             Startup Items                         Hidden Window                                                                                                                                             Third-party Software
LC_LOAD_DYLIB Addition                                Sudo                                  HISTCONTROL                                                                                                                                               Trap
Local Port Monitor                                    Valid Accounts                        Indicator Blocking                                                                                                                                        Trusted Developer Uti...
Login Item                                            Web Shell                             Indicator Removal from Tools                                                                                                                              Windows Management In...
Logon Scripts                                                                               Indicator Removal on Host                                                                                                                                 Windows Remote Manage...
Modify Existing Service                                                                     Install Root Certificate
Netsh Helper DLL                                                                            InstallUtil
New Service                                                                                 Launchctl
Office Application Startup                                                                  LC_MAIN Hijacking
Path Interception                                                                           Masquerading
Plist Modification                                                                          Modify Registry
Rc.common                                                                                   Network Share Connection Removal
Redundant Access                                                                            NTFS Extended Attributes
Registry Run Keys / Start Folder                                                            Obfuscated Files or Information
Re-opened Applications                                                                      Plist Modification
Scheduled Task                                                                              Process Hollowing
Security Support Provider                                                                   Redundant Access
Service Registry Permissions Weakness                                                       Regsvcs/Regasm
Shortcut Modification                                                                       Regsvr32
Startup Items                                                                               Rootkit
System Firmware                                                                             Rundll32
Trap                                                                                        Scripting
Valid Accounts                                                                              Software Packing
Web Shell                                                                                   Space after Filename
Windows Management Instrumentation Event Subscription                                       Timestomp
Winlogon Helper DLL                                                                         Trusted Developer Utilities
                                                                                            Valid Accounts
```

### Getting an up to date ATT&CK Matrix for Enterprise and exporting it to a csv
```
Invoke-ATTACKAPI -Matrix | select Persistence, 'Privilege Escalation', 'Defense Evasion','Credential Access', Discovery, 'Lateral Movement', Execution, Collection, Exfiltration, 'Command and Control' | Export-Csv C:\wardog\scripts\matrix.csv -NoTypeInformation
```

# Author
* Roberto Rodriguez [@Cyb3rWard0g](https://twitter.com/Cyb3rWard0g)
# Contributors
# Contributing
Feel free to submit a PR and make this script a better one for the community.
# TO-DO
