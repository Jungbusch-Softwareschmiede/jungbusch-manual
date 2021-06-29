# Module

## Inhaltsverzeichnis

**Für alle Architekturen:**

- [ExecuteCommand](#executecommand)

- [FileContent](#filecontent)

- [Grep](#grep)

- [IsFile](#isfile)

- [Permissions](#permissions)

- [Script](#das-script-modul)

**Linux:**

- [Auditctl](#auditctl)

- [Authselect](#authselect)

- [AwkScript](#awkscript)

- [BashScript](#bashscript)

- [CheckPartition](#checkpartition)

- [IsInstalled](#isinstalled)

- [IsNotInstalled](#isnotinstalled)

- [Modprobe](#modprobe)

- [NftListRuleset](#nftlistruleset)

- [Sshd](#sshd)

- [Stat](#stat)

- [Sysctl](#sysctl)

- [Systemctl](#systemctl)

**Windows:**

- [AuditPolicyQuery](#auditpolicyquery)

- [DumpSecuritySettings](#dumpsecuritysettings)

- [ExportInstalledSoftware](#exportinstalledsoftware)

- [GetAccountName](#getaccountname)

- [GetUserSID](#getusersid)

- [GetWinEnv](#getwinenv)

- [IsGPTemplatePresent](#isgptemplatepresent)

- [RegistryQuery](#registryquery)

- [SecuritySettingsQuery](#securitysettingsquery)

## Module für alle Architekturen

### ExecuteCommand

- Kompatibilität: all
- Alias: execute_command, executeCommand
- Beschreibung des Moduls: ExecuteCommand führt den übergebenen Befehl aus und überprüft optional, ob der angegebene Suchbegriff im Ergebnis vorhanden ist.
- Parameter:
	- command (cmd): Der auszuführende Befehl
	- grep: \[Optional\] Suchbegriff, entspricht dem Pipen des Outputs in grep
- Benötigt Admin-Rechte: Nein

### FileContent
- Kompatibilität: all
- Alias: file_content, fileContent
- Beschreibung des Moduls: FileContent gibt den Inhalt einer Datei als String zurück. Ist der grep-Parameter angegeben, werden die Zeilen zurückgegeben, in denen ein Match vorliegt.
- Parameter:
	- file (datei): Pfad zur Datei, die ausgelesen werden soll
	- grep: \[Optional\] Optionaler Suchbegriff, entspricht dem Pipen des Outputs in grep
- Benötigt Admin-Rechte: Nein

### Grep
- Kompatibilität: all
- Alias: grep
- Beschreibung des Moduls: Grep dient als Suchfunktion und kann in verschiedenen Modulen aufgerufen werde.
- Parameter:
  - input: Übergebener String, in dem gesucht werden soll
  - grep: Suchbegriff/Regex-Ausdruck
- Benötigt Admin-Rechte: Nein

### IsFile
- Kompatibilität: all
- Alias: isfile
- Beschreibung: IsFile prüft ob eine Datei existiert.
- Parameter:
	- path: Pfad zur Datei
- Benötigt Admin-Rechte: Nein

### Permissions
- Kompatibilität: all
- Alias: perms, permissions
- Beschreibung des Moduls: Permissions gibt die Berechtigungen der/des angegebenen Datei/Ordners zurück.
- Parameter:
	- path (pfad): Pfad der/des zu überprüfenden Datei/Ordners
- Benötigt Admin-Rechte: Nein

## Linux-Module

### Auditctl
- Kompatibilität: linux
- Alias: auditctl
- Beschreibung des Moduls: Mit Auditctl können die Kernel-Audit-Regeln ausgelesen werden.
- Parameter:
	- grep (name, modul): Suchbegriff, entspricht Pipen des Outputs in grep
- Benötigt Admin-Rechte: Ja

### Authselect
- Kompatibilität: rhel
- Alias: authselect
- Beschreibung des Moduls: Mit Authselect lässt sich die Konfiguration des authselect-Profils überprüfen.
- Parameter:
	- grep: \[Optional\] Suchbegriff, entspricht dem Pipen des Outputs in grep
- Benötigt Admin-Rechte: Nein

### AwkScript
- Kompatibilität: linux
- Alias: awk, awkScript, awk_script
- Beschreibung des Moduls: Awk ist eine Skriptsprache zum Editieren und Analysieren von Texten. AwkScript führt ein Skript auf die Input-Datei aus.
- Parameter:
	- input: String, auf den das Skript angewendet wird
	- awkscript (script): Awk-Script, welches ausgeführt werden soll
	- seperator: \[Optional\] Legt den Field-Separator fest
- Benötigt Admin-Rechte: Nein

### Bashscript
- Kompatibilität: linux
- Alias: bash_script, bashscript
- Beschreibung des Moduls: BashScript führt das verlinkte Bash-Script aus. Als Ergebnis wird der Output des Skripts erhalten.
- Parameter:
	- script: Der Pfad zum auszuführenden Bash-Script
- Benötigt Admin-Rechte: Nein

### CheckPartition
- Kompatibilität: linux
- Alias: checkPartition, mount
- Beschreibung des Moduls: CheckPartition gibt alle eingehängten Datenträger aus. Ist der grep-Parameter gesetzt, werden die Zeilen zurückgegeben, in denen das Pattern gefunden wurde.
- Parameter:
	- grep: \[Optional\] Optionaler Suchbegriff, entspricht dem Pipen des Outputs in grep
	- vgrep: \[Optional\] Optionaler Suchbegriff, entspricht dem Pipen des Outputs in grep -v
- Benötigt Admin-Rechte: Nein


### IsInstalled
- Kompatibilität: linux, darwin
- Alias: isInstalled, is_installed, installed
- Beschreibung des Moduls: IsInstalled überprüft, ob das angegebene Package installiert ist.
- Parameter:
	- package (name, packagename, pkg): Name des Packages
- Benötigt Admin-Rechte: Nein

### IsNotInstalled
- Kompatibilität: linux, darwin
- Alias: isNotInstalled, is_not_installed, notInstalled, not_installed
- Beschreibung des Moduls: IsNotInstalled überprüft, ob das angegebene Package nicht installiert ist.
- Parameter:
	- package (name, packagename, pkg): Name des Packages
- Benötigt Admin-Rechte: Nein

### Modprobe
- Kompatibilität: linux
- Alias: modprobe
- Beschreibung des Moduls: Modprobe simuliert das Laden des angegebenen Moduls zur Laufzeit des Systems und speichert das Ergebnis ausführlich ab. Daraufhin wird überprüft, ob das angegebene Modul aktuell geladen ist.
- Parameter:
	- modul (name): Name des Moduls
- Benötigt Admin-Rechte: Ja

### NftListRuleset
- Kompatibilität: linux
- Alias: nftListRuleset, nft_list_ruleset
- Beschreibung des Moduls: Mit NftListRuleset lässt sich das Ruleset von nftables analysieren.
- Parameter:
	- awk: \[Optional\] Optionales Skript
	- grep: Suchbegriff, entspricht dem Pipen des Outputs in grep
- Benötigt Admin-Rechte: Ja

### Sshd
- Kompatibilität: linux
- Alias: sshd
- Beschreibung des Moduls: Sshd liest die Informationen aus der sshd Config-Datei aus.
- Parameter:
	- grep: \[Optional\] Optionaler Suchbegriff, entspricht dem Pipen des Outputs in grep
- Benötigt Admin-Rechte: Nein

### Stat
- Kompatibilität: linux
- Alias: stat
- Beschreibung: Mit dem Befehl stat lassen sich Zugriffs- und Änderungszeitstempel von Dateien und Ordnern anzeigen. Weiterhin werden Informationen zu Rechten, Besitzer und Gruppe, sowie zu dem Dateityp ausgegeben.
- Parameter:
	- file (datei): Pfad zur Datei
- Benötigt Admin-Rechte: Ja

### Sysctl
- Kompatibilität: linux
- Alias: sysctl
- Beschreibung: Sysctl wird dazu verwendet, Kernelparameter zur Laufzeit zu ändern. Die verfügbaren Parameter sind unter `/proc/sys/` aufgelistet. Für die sysctl-Unterstützung in Linux ist Procfs notwendig. Sysctl kann sowohl zum Lesen als auch zum Schreiben von Sysctl-Daten verwendet werden.
- Parameter:
	- kernelparameter (kernelparam): Der Name des Schlüssels, aus dem gelesen werden soll.
- Benötigt Admin-Rechte: Nein

### Systemctl
- Kompatibilität: linux
- Alias: systemctl
- Beschreibung: Systemctl überprüft, ob die angegebene Unitdatei aktiviert ist.
- Parameter:
	- unitdatei (unitname): Name der Unitdatei
- Benötigt Admin-Rechte: Nein

## Windows Module

### AuditPolicyQuery
- Kompatibilität: windows
- Alias: auditpolicyquery, auditpol
- Beschreibung des Moduls: AuditPolicyQuery ermöglicht den Bereich 'Advanced Audit Policy Configuration' der Security Settings auszulesen.
- Parameter:
	- guid: GUID der jeweiligen Value. Bitte im Benutzerhandbuch oder Internet nachschlagen.
- Benötigt Admin-Rechte: Ja
- Weitere Informationen: **Achtung**: Die Ausgabe des Moduls ist von der jeweiligen  Systemsprache abhängig. Dies muss in der Auditconfig berücksichtigt werden.

Da die Richtlinien des Konfigurationsknoten `Computer Configuration\Policies\Windows Settings\Security Settings\Advanced Audit Policy Configuration` nur schwer per Registry auszulesen sind (`SYSTEM`-Rechte werden benötigt, die Values sind vom Typ `REG_BINARY`) kann stattdessen dieses Modul verwendet werden. Es wird nur die GUID der auszulesenden Richtlinie benötigt. 

Über die GUID `{0CCE923F-69AE-11D9-BED3-505054503030}` kann man so beispielsweise auf die Richtlinie `...\Account Logon\Audit Credential Validation` zugreifen. Anbei einige der benötigten GUIDs:  

GUID| GP-Pfad
--- | ---
{0CCE923F-69AE-11D9-BED3-505054503030} | ...\\Account Logon\\Audit Credential Validation
{0CCE9241-69AE-11D9-BED3-505054503030} | ...\\Account Logon\\Audit Other Account Logon Events
{0CCE9240-69AE-11D9-BED3-505054503030} | ...\\Account Logon\\Audit Kerberos Service Ticket Operations
{0CCE9242-69AE-11D9-BED3-505054503030} | ...\\Account Logon\\Audit Kerberos Authentication Service
{0CCE9239-69AE-11D9-BED3-505054503030} | ...\\Account Management\\Audit Application Group Management
{0CCE9237-69AE-11D9-BED3-505054503030} | ...\\Account Management\\Audit Security Group Management
{0CCE9235-69AE-11D9-BED3-505054503030} | ...\\Account Management\\Audit User Account Management
{0CCE9236-69AE-11D9-BED3-505054503030} | ...\\Account Management\\Audit Computer Account Management
{0CCE923A-69AE-11D9-BED3-505054503030} | ...\\Account Management\\Audit Other Account Management Events
{0CCE9238-69AE-11D9-BED3-505054503030} | ...\\Account Management\\Audit Distribution Group Management
{0CCE922B-69AE-11D9-BED3-505054503030} | ...\\Detailed Tracking\\Audit Process Creation
{0CCE924A-69AE-11D9-BED3-505054503030} | ...\\Detailed Tracking\\Token Right Adjusted Events
{0CCE9248-69AE-11D9-BED3-505054503030} | ...\\Detailed Tracking\\Audit PNP Activity
{0CCE922E-69AE-11D9-BED3-505054503030} | ...\\Detailed Tracking\\Audit RPC Events
{0CCE922D-69AE-11D9-BED3-505054503030} | ...\\Detailed Tracking\\Audit DPAPI Activity
{0CCE922C-69AE-11D9-BED3-505054503030} | ...\\Detailed Tracking\\Audit Process Termination
{0CCE9217-69AE-11D9-BED3-505054503030} | ...\\Logon/Logoff\\Audit Account Lockout
{0CCE9249-69AE-11D9-BED3-505054503030} | ...\\Logon/Logoff\\Audit Group Membership
{0CCE9216-69AE-11D9-BED3-505054503030} | ...\\Logon/Logoff\\Audit Logoff
{0CCE9215-69AE-11D9-BED3-505054503030} | ...\\Logon/Logoff\\Audit Logon
{0CCE921C-69AE-11D9-BED3-505054503030} | ...\\Logon/Logoff\\Audit Other Logon/Logoff Events
{0CCE921B-69AE-11D9-BED3-505054503030} | ...\\Logon/Logoff\\Audit Special Logon
{0CCE921A-69AE-11D9-BED3-505054503030} | ...\\Logon/Logoff\\IPsec Extended Mode
{0CCE9219-69AE-11D9-BED3-505054503030} | ...\\Logon/Logoff\\Audit IPsec Quick Mode
{0CCE9243-69AE-11D9-BED3-505054503030} | ...\\Logon/Logoff\\Network Policy Server
{0CCE9247-69AE-11D9-BED3-505054503030} | ...\\Logon/Logoff\\Audit User/Device Claims
{0CCE9218-69AE-11D9-BED3-505054503030} | ...\\Logon/Logoff\\Audit IPsec Main Mode
{0CCE9244-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit Detailed File Share
{0CCE9224-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit File Share
{0CCE9227-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit Other Object Access Events
{0CCE9245-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit Removable Storage
{0CCE921E-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit Registry
{0CCE921D-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit File System
{0CCE9220-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit SAM
{0CCE9222-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit Application Generated
{0CCE9223-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit Handle Manipulation
{0CCE9225-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit Filtering Platform Packet Drop
{0CCE9246-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit Central Access Policy Staging
{0CCE9226-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit Filtering Platform Connection
{0CCE9221-69AE-11D9-BED3-505054503030} | ...\\Object Access\\Audit Certification Services
{0CCE922F-69AE-11D9-BED3-505054503030} | ...\\Policy Change\\Audit Audit Policy Change
{0CCE9230-69AE-11D9-BED3-505054503030} | ...\\Policy Change\\Audit Authentication Policy Change
{0CCE9231-69AE-11D9-BED3-505054503030} | ...\\Policy Change\\Audit Authorization Policy Change
{0CCE9232-69AE-11D9-BED3-505054503030} | ...\\Policy Change\\Audit MPSSVC RuleLevel Policy Change
{0CCE9234-69AE-11D9-BED3-505054503030} | ...\\Policy Change\\Audit Other Policy Change Events
{0CCE9233-69AE-11D9-BED3-505054503030} | ...\\Policy Change\\Audit Filtering Platform Policy Change
{0CCE9228-69AE-11D9-BED3-505054503030} | ...\\Privilege Use\\Audit Sensitive Privilege Use
{0CCE9213-69AE-11D9-BED3-505054503030} | ...\\System\\Audit IPsec Driver
{0CCE9214-69AE-11D9-BED3-505054503030} | ...\\System\\Audit Other System Events
{0CCE9210-69AE-11D9-BED3-505054503030} | ...\\System\\Audit Security State Change
{0CCE9211-69AE-11D9-BED3-505054503030} | ...\\System\\Audit Security System Extension
{0CCE9212-69AE-11D9-BED3-505054503030} | ...\\System\\Audit System Integrity
{0CCE922A-69AE-11D9-BED3-505054503030} | ...\\Privilege Use\\Audit Other Privilege Use Events
{0CCE9229-69AE-11D9-BED3-505054503030} | ...\\Privilege Use\\Audit Non-Sensitive Privilege Use
{0CCE923C-69AE-11D9-BED3-505054503030} | ...\\DS Access\\Audit Directory Service Changes
{0CCE923D-69AE-11D9-BED3-505054503030} | ...\\DS Access\\Audit Directory Service Replication
{0CCE923E-69AE-11D9-BED3-505054503030} | ...\\DS Access\\Audit Detailed Directory Service Replication
{0CCE923B-69AE-11D9-BED3-505054503030} | ...\\DS Access\\Audit directory service access
{0CCE921F-69AE-11D9-BED3-505054503030} | ...\\Global Object Access Auditing\\Audit Kernel Object

Weiterführende Links: 

[docs.microsoft.com](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-gpac/77878370-0712-47cd-997d-b07053429f6d)

[gerhaeuser.info](https://www.gerhaeuser.info/index.php/erweiterte-ueberwachungsrichtlinienkonfiguration)

### DumpSecuritySettings
- Kompatibilität: windows
- Alias: dumpsecuritysettings
- Beschreibung des Moduls: DumpSecuritySettings ermöglicht das Dumpen der aktuellen Security-Settings in eine Datei, welche mit dem Modul [SecuritySettingsQuery](#securitysettingsquery) ausgelesen werden kann.
- Parameter:
	- path: \[Optional\] Hier kann ein Pfad angegeben werden, an welchem die zu dumpende Datei abgelegt werden soll. Wird kein Pfad angegeben, wird sie in einem temporären Ordner abgelegt. Unabhängig davon, wird sie in die Modul-Artefakte und somit den Output aufgenommen. Wird hier ein Pfad angegeben, muss dieser auch im Query-Modul explizit angegeben werden.
- Benötigt Admin-Rechte: Ja

### ExportInstalledSoftware
- Kompatibilität: windows
- Alias: exportinstalledsoftware
- Beschreibung des Moduls: ExportInstalledSoftware speichert alle Namen und Versionsnummern der auf der Maschine installierten Software in einer CSV Datei ab.
- Parameter:
	- path: \[Optional\] Hier kann ein Pfad angegeben werden, an welchem die CSV Datei abgelegt werden soll. Wird kein Pfad angegeben, wird sie in einem Temporären Ordner abgelegt. Unabhängig davon, wird sie in die Modul-Artefakte und somit den Output aufgenommen.
- Benötigt Admin-Rechte: Nein
- Weitere Informationen: Als Quelle der Informationen über die installierte Software wird die Registry verwendet. 

### GetAccountName
- Kompatibilität: windows
- Alias: getaccountname
- Beschreibung des Moduls: GetAccountName gibt den Name des Gast oder Lokalen Accounts aus.
- Parameter:
	- type (typ): Accounttyp dessen Name abgefragt werden möchte. (`Guest`/`User`)
- Benötigt Admin-Rechte: Nein

### GetUserSID
- Kompatibilität: windows
- Alias: getusersid
- Beschreibung des Moduls: GetUserSID gibt die SID des angegebenen Nutzer aus.
- Parameter:
	- userName: Windows Nutzername dessen SID bestimmt werden soll.
- Benötigt Admin-Rechte: Nein

### GetWinEnv
- Kompatibilität: windows
- Alias: getwinenv
- Beschreibung des Moduls: GetWinEnv gibt den Wert der angegebenen Windows Umgebungsvariable aus.
- Parameter:
	- envVar: Name der Windows-Umgebungsvariable.
- Benötigt Admin-Rechte: Nein

### IsGPTemplatePresent
- Kompatibilität: windows
- Alias: isgptemplatetresent
- Beschreibung des Moduls: IsGPTemplatePresent prüft, ob das angegebene Group Policy Administrative Template vorhanden ist.
- Parameter:
	- templateName: Vollständiger Dateinamen des Templates (z.B.: AdmPwd.admx/adml).
- Benötigt Admin-Rechte: Nein
- Weitere Informationen: **Achtung:** Da die '.adml' Dateien in dem Ordner der jeweiligen Sparche liegen, müssen diese manuell im Modul hinzugefügt werden. Aktuell werden 21 Sprachen unterstützt.

### RegistryQuery
- Kompatibilität: windows
- Alias: registryquery, regquery, registry
- Beschreibung des Moduls: RegQuery gibt den Wert eines Registry Keys aus.
- Parameter:
	- key: Vollständiger Key. Z.B.: HKEY_LOCAL_MACHINE\\SOFTWARE\\Policies...
	- value: Value des Registry Keys. Z.B.: AllowCortana
- Weitere Informationen: Bereiche der Registry für die man `SYSTEM`-Rechte benötigt, können nicht abgefragt werden (z.B.: 'HKEY_LOCAL_MACHINE\\SECURITY\\SAM'). Die Typem REG_BINARY und REG_LINK werden zurzeit nicht unterstützt, können aber im Modul ergänzt werden.
- Benötigt Admin-Rechte: Nein


### SecuritySettingsQuery
- Kompatibilität: windows
- Alias: securitysettingsquery
- Beschreibung des Moduls: SecuritySettingsQuery ermöglicht das Auslesen von verschiedenen Bereichen der Security Settings. Es muss vorher ein Dump dieser Settings mit [DumpSecuritySettings](#dumpsecuritysettings) erstellt werden.
- Parameter:
	- valueName: Name der Security Setting. Bitte im Benutzerhandbuch nachschlagen.
	- path: \[Optional\] Pfad zur Dump-Datei. Muss nur angegeben werden, wenn im Dump-Modul ein Pfad spezifiziert wurde. 
- Benötigt Admin-Rechte: Nein
- Weitere Informationen: Das DumpSecuritySettings Modul muss zwingend vor diesem Modul ausgeführt werden! Da die Richtlinien des Konfigurationsknoten `Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies` und `Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies` nur schwer per Registry auszulesen sind (`SYSTEM`-Rechte werden benötigt, die Values sind vom Typ `REG_BINARY`) kann stattdessen dieses Modul verwendet werden.
Die Value-Namen ergeben sich aus der DumpSecuritySettings-Datei. Die zugehörigen Gruppenrichtlinien-Pfade werden in der unten stehenden Tabelle aufgeführt.

Value | GP-Pfad
--- | ---
PasswordHistorySize | ...\\Account Policies\\Password Policy\\Enforce password history
MaximumPasswordAge | ...\\Account Policies\\Password Policy\\Maximum password age
MinimumPasswordAge | ...\\Account Policies\\Password Policy\\Minimum password age
MinimumPasswordLength | ...\\Account Policies\\Password Policy\\Minimum password length
PasswordComplexity | ...\\Account Policies\\Password Policy\\Password must meet complexity requirements
ClearTextPassword | ...\\Account Policies\\Password Policy\\Store passwords using reversible encryption
LockoutDuration | ...\\Account Policies\\Account Lockout Policy\\Account lockout duration
LockoutBadCount | ...\\Account Policies\\Account Lockout Policy\\Account lockout threshold
ResetLockoutCount | ...\\Account Policies\\Account Lockout Policy\\Reset account lockout counter after
SeTrustedCredManAccessPrivilege | ...\\Local Policies\\User Rights Assignment\\Access Credential Manager as a trusted caller
SeNetworkLogonRight | ...\\Local Policies\\User Rights Assignment\\Access this computer from the network
SeTcbPrivilege | ...\\Local Policies\\User Rights Assignment\\Act as part of the operating system
SeIncreaseQuotaPrivilege | ...\\Local Policies\\User Rights Assignment\\Adjust memory quotas for a process
SeInteractiveLogonRight | ...\\Local Policies\\User Rights Assignment\\Allow log on locally
SeRemoteInteractiveLogonRight | ...\\Local Policies\\User Rights Assignment\\Allow log on through Remote Desktop Services
SeBackupPrivilege | ...\\Local Policies\\User Rights Assignment\\Back up files and directories
SeSystemtimePrivilege | ...\\Local Policies\\User Rights Assignment\\Changethe system time
SeTimeZonePrivilege | ...\\Local Policies\\User Rights Assignment\\Change the time zone
SeCreatePagefilePrivilege | ...\\Local Policies\\User Rights Assignment\\Create a pagefile
SeCreateTokenPrivilege | ...\\Local Policies\\User Rights Assignment\\Create a token object
SeCreateGlobalPrivilege | ...\\Local Policies\\User Rights Assignment\\Create global objects
SeCreatePermanentPrivilege | ...\\Local Policies\\User Rights Assignment\\Create permanent shared objects
SeCreateSymbolicLinkPrivilege | ...\\Local Policies\\User Rights Assignment\\Create symbolic links
SeDebugPrivilege | ...\\Local Policies\\User Rights Assignment\\Debug programs
SeDenyNetworkLogonRight | ...\\Local Policies\\User Rights Assignment\\Deny access to this computer from the network
SeDenyBatchLogonRight | ...\\Local Policies\\User Rights Assignment\\Deny log on as a batch job
SeDenyServiceLogonRight | ...\\Local Policies\\User Rights Assignment\\Deny log on as a service
SeDenyInteractiveLogonRight | ...\\Local Policies\\User Rights Assignment\\Deny log on locally
SeDenyRemoteInteractiveLogonRight | ...\\Local Policies\\User Rights Assignment\\Deny log on through Remote Desktop Services
SeEnableDelegationPrivilege | ...\\Local Policies\\User Rights Assignment\\Enable computer and user accounts to be trusted for delegation
SeRemoteShutdownPrivilege | ...\\Local Policies\\User Rights Assignment\\Force shutdown from a remote system
SeAuditPrivilege | ...\\Local Policies\\User Rights Assignment\\Generate security audits
SeImpersonatePrivilege | ...\\Local Policies\\User Rights Assignment\\Impersonate a client after authentication
SeIncreaseBasePriorityPrivilege | ...\\Local Policies\\User Rights Assignment\\Increase scheduling priority
SeLoadDriverPrivilege | ...\\Local Policies\\User Rights Assignment\\Load and unload device drivers
SeLockMemoryPrivilege | ...\\Local Policies\\User Rights Assignment\\Lock pages in memory
SeBatchLogonRight | Computer Configuration\\Windows Settings\\Security Settings\\Local Policies\\User Rights Assignment\\Log on as a batch job
SeServiceLogonRight | Computer Configuration\\Windows Settings\\Security Settings\\Local Policies\\User Rights Assignment\\Log on as a service
SeSecurityPrivilege | ...\\Local Policies\\User Rights Assignment\\Manage auditing and security log
SeRelabelPrivilege | ...\\Local Policies\\User Rights Assignment\\Modify an object label
SeSystemEnvironmentPrivilege | ...\\Local Policies\\User Rights Assignment\\Modify firmware environment values
SeManageVolumePrivilege | ...\\Local Policies\\User Rights Assignment\\Perform volume maintenance tasks
SeProfileSingleProcessPrivilege | ...\\Local Policies\\User Rights Assignment\\Profile single process
SeSystemProfilePrivilege | ...\\Local Policies\\User Rights Assignment\\Profile system performance
SeShutdownPrivilege | ...\\Local Policies\\User Rights Assignment\\Replace a process level token
SeRestorePrivilege | ...\\Local Policies\\User Rights Assignment\\Restore files and directories
SeShutdownPrivilege | ...\\Local Policies\\User Rights Assignment\\Shut down the system
SeTakeOwnershipPrivilege | ...\\Local Policies\\User Rights Assignment\\Take ownership of files or other objects
EnableAdminAccount | ...\\Local Policies\\Security Options\\Accounts: Administrator account status
EnableGuestAccount | ...\\Local Policies\\Security Options\\Accounts: Guest account status
NewAdministratorName | ...\\Local Policies\\Security Options\\Accounts: Rename administrator account
NewGuestName | ...\\Local Policies\\Security Options\\Accounts: Rename guest account
LSAAnonymousNameLookup | ...\\Local Policies\\Security Options\\Network access: Allow anonymous SID/Name translation
ForceLogoffWhenHourExpire | ...\\Local Policies\\Security Options\\Network security: Force logoff when logon hours expire

## Das Script-Modul

- Name: Script
- Alias: script, javascript, js
- Parameter:
	- script (js): Auszuführendes Script über mehrere Zeilen
- Benötigt Admin-Rechte: Nein

Das `Script`-Modul ist ein besonderes Modul im Jungbusch-Auditorium. Grundlegend bietet es folgende Funktionen an:
- Scripting mittels ECMAScript 5.1 Syntax
- Zugriff auf alle anderen Auditorium-Module
- Zugriff auf alle in der Audit-Config definierten Variablen

### Grundlegender Aufbau

Der Script-Parameter ist normaler ECMAScript-Code. Als letztes Statement im Code muss immer ein ModuleResult-Objekt zurückgegeben werden. Deshalb wird empfohlen, das Script immer nach dem folgenden Muster aufzubauen:

```js
function runModule() {
    // Hier steht Code...
	return result;
}
runModule();
```

Der Funktionsname kann hier frei gewählt werden.

Ein `result`-Objekt kommt entweder von einem ausgeführten Modul ([Zugriff auf Moduke](#zugriff-auf-module) oder kann im Code selbst mit eigenen Werten gefüllt werden ([Das Erstellen eines Result-Objekts](#das-erstellen-eines-benutzerdefinierten-result-objekts)).

### Zugriff auf Module

Im Script kann auf alle verfügbaren Module des Auditoriums über ihren Funktionsnamen und mit den benötigten Parametern aufgerufen werden. Eine `map` namens `params` steht für die Übergabe von Parametern zur Verfügung. Jedes Modul liefert ein `ModuleResult`-Objekt, welches zurückgegeben werden kann:

```js
function runModule() {
    params.file = "/etc/shadow";
    params.grep = "\$[1256]\$";
    return FileContent(params);
}
runModule();
```

Zugriff auf die Module erfolgt über einen großgeschriebenen Methodennamen, um zu verdeutlichen, dass es sich hier um ein Modul handelt.

Das Ergebnis des ausgeführten Moduls kann dann weiterverwendet werden:

```js
function runModule() {
	params.file = "/etc/shadow";
	params.grep = "\$[1256]\$";
	res = FileContent(params);
	
	if(res.result != "") {
	    params.command = "stat /etc/shadow";
	    params.grep = ""; // Grep-Parameter muss wieder überschrieben werden
	    res = ExecuteCommand(params);
	}
	return res;
}
runModule();
```

### Zugriff auf Logging-Funktionen

Im Script kann auf die Logging-Funktionen `info`, `warn`, `err` und `debug` zugegriffen werden. Diese sind äquivalent zu den Logging-Funktionen im Rest des Auditoriums und werden auf der Konsole, sowie in der Log-Datei basierend auf den für das Jungbusch-Auditorium gesetzten Log-Leveln ausgegeben.

```js
function runModule() {
	info("Dies ist eine INFO-Nachricht");
	warn("Dies ist eine WARN-Nachricht");
	err("Dies ist eine ERR-Nachricht");
	debug("Dies ist eine DEBUG-Nachricht");
	// Code...
	return result;
}
runModule();
```

### Zugriff auf Variablen

Im Script kann auf alle in der Auditkonfiguration festgelegten und im Modul verfügbaren Variablen zugegriffen werden. Im Code werden hierfür die %-Zeichen weggelassen. Den Variablen kann im Code auch ein neuer Wert zugewiesen werden. Der neue Wert ist dann in den verschachtelten Modulen verfügbar. Siehe auch: [Variablen](#variablen)

```js
id: "1"
module: "Script"
%shadow% = "/etc/shadow"
script: `
function runModule() {
    params.file = shadow;
    params.grep = "\$[1256]\$";
    return FileContent(params);
}
runModule();
`
```

### Das Erstellen eines benutzerdefinierten Result-Objekts

Falls vom Script ein Ergebnis zurückgegeben werden soll, welches nicht von einem Modul produziert werden kann, steht die Funktion `newResult(result, resultRaw, err)` zur Verfügung.

```js
function runModule() {
    return newResult("Ergebnis", "Dies ist ein benutzerdefiniertes Ergebnis", null);
}
runModule();
```

## Das Erstellen von benutzerdefinierten Modulen

Das Jungbusch-Auditorium erlaubt das einfache Erstellen von eigenen Modulen. Das vorgegebene Format muss nur ausgefüllt und angepasst werden. Ein Template befindet sich im Modul-Ordner unter dem Dateinamen "0_template.go".

### Genereller Aufbau

Jedes Modul besteht aus drei Funktionen:

1. **Initialize**

Diese Methode ist zwingend benötigt und teilt dem Framework unter anderem mit, was das Modul tut, welche Eingaben erwartet werden und mit welchen Betriebssystemen das Modul kompatibel ist. 

2. **Validate**

Diese Methode wird **nicht** zwingend benötigt. Ihr wird eine ParameterMap übergeben werden, also ein Array aus den Übergabe-Parametern an das Modul. Diese bestehen jeweils aus einem Parameter-Namen und einem Wert.
In der Validate-Methode kann überprüft werden, ob die in der Audit-Konfiguration angegebenen Werte valide sind. Wenn dies der Fall ist, gibt sie nil zurück, ansonsten einen Error.
Der Vorteil dieser Methode ist, dass die Validate-Methoden aller Module ausgeführt und überprüft werden, bevor ein einziges Modul ausgeführt wird. Fehler in der Konfiguration können so frühzeitig festgestellt werden.

3. **Execute**

Diese Methode wird zwingend benötigt. Sie führt das eigentliche Modul aus. Sie bekommt dieselbe ParameterMap wie die Validate-Methode übergeben. Sie führt die Aufgabe, die das Modul übernehmen soll, aus und gibt ein Objekt vom Typ ModuleResult zurück. In diesem sind verwendete Dateien zum späteren Sammeln dieser, das Ergebnis des Modules selbst und ggf. ein Error enthalten.


### Die Initialize-Methode

Der Name der Methode setzt sich aus dem Namen des Moduls, sowie dem Suffix "Init" zusammen.
Folgend am Beispiel des Moduls [ExecuteCommand](#executecommand) erläutert:

```go
func (mh *MethodHandler) ExecuteCommandInit() ModuleSyntax {
	return ModuleSyntax{
		ModuleName:          "ExecuteCommand",
		ModuleDescription:   "ExecuteCommand führt den übergebenen Befehl aus und überprüft optional, ob der angegebene Suchbegriff im Ergebnis vorhanden ist.",
		ModuleAlias:         []string{"execute_command", "executeCommand"},
		ModuleCompatibility: []string{"all"},
		InputParams: ParameterSyntaxMap{
			"command": ParameterSyntax{
				ParamName:        "command",
				ParamAlias:       []string{"cmd"},
				ParamDescription: "Der auszuführende Befehl",
			},
			"grep": ParameterSyntax{
				ParamName:        "grep",
				IsOptional:       true,
				ParamDescription: "Optionaler Suchbegriff, entspricht dem Pipen des Outputs in grep",
			},
		},
	}
}
```

#### Modul-Name

Der Parameter "ModulName" legt den Namen des Moduls fest. Anhand von diesem Namen werden die Module aus der Audit-Konfiguration angesprochen. An ihm orientieren sich außerdem die **Namen aller Funktionen des Moduls**. Modulnamen müssen **einzigartig** sein. Dieser Parameter ist zwingend anzugeben.

> **Wichtig:** Der Name eines Moduls muss zwingend mit einem Großbuchstaben beginnen.

#### Modul-Alias

Der ModuleAlias-Parameter ist eine Liste aus möglichen Aliasen, mit denen das Modul aus der Audit-Konfiguration angesprochen werden kann. Sie können mit Klein-Buchstaben beginnen. Es muss darauf geachtet werden, dass sie sich nicht mit den Namen/Aliasen anderer Module überschneiden. Sollen keine Aliase gesetzt werden, kann dieser Parameter weggelassen werden.

#### Module-Description

Dieser Parameter ist optional. Die Beschreibung wird für die Ausgabe des Comamndline-Parameters [ShowModuleInfo](#showmoduleinfo) verwendet.

#### Modul-Compatibility

Der ModuleCompatibility-Parameter ist eine Liste aus allen Betriebssystemen, mit welcher das Modul getestet wurde und kompatibel ist. Siehe [Betriebssysteme](#betriebssysteme). Dieser Parameter ist zwingend anzugeben.

#### Input-Parameter

Die `InParams` legen fest, welche Eingabe-Parameter das Modul bekommt. Diese haben jeweils einen Name (hier: "command"), und optional eine Beschreibung und Aliase. Des Weiteren kann `IsOptional` auf `true` gesetzt werden. Per Default ist dies auf `false` gesetzt, was bedeutet dass der Parser einen Fehler erzeugt, wenn der Parameter nicht in der Audit-Konfigurationsdatei angegeben wurde.
 
```go		
InputParams: ParameterSyntaxMap{
	"command": ParameterSyntax{
		ParamName:        "command",
		ParamAlias:       []string{"cmd"},
		ParamDescription: "Der auszuführende Befehl",
	},
	"grep": ParameterSyntax{
		ParamName:        "grep",
		IsOptional:       true,
		ParamDescription: "Optionaler Suchbegriff, entspricht dem Pipen des Outputs in grep",
	},
},
```

### Die Validate-Methode 

Der Name der Methode setzt sich aus dem Name des Moduls, sowie dem Suffix "Validate" zusammen.
Der Code, den diese Methode beinhaltet ist stark abhängig vom Modul selbst und seinen Übergabe-Parametern. Die Methode könnte so aussehen:

```go
func (mh *MethodHandler) ExecuteCommandValidate(params ParameterMap) error {
	if params["command"] == "" {
		return errors.New("der Command-Parameter darf nicht leer sein")
	 }

	return nil
}

```

Gibt es nichts zu validieren, kann diese Methode vollständig weggelassen werden. Es muss kein leerer Methodenstumpf stehen gelassen werden.

### Die Execute-Methode 

Der Name der Methode ist der Name des Moduls selbst.
Sie bekommt die aus der Validate-Methode bekannte Parameter-Map übergeben, führt danach die Aufgabe des Moduls aus und erzeugt ein Objekt vom Typ ModuleResult.

Dieses setzt sich wie folgt zusammen:

#### ParameterMap

Auf die Werte der ParameterMap greift man über die Namen zu, die in der Init-Methode gesetzt wurde. Ist der `ParamName` auf `"command"` gesetzt, dann wird auf den Wert mit `params["command"]` zugegriffen. Wird in der Auditkonfiguration ein Alias statt des Parameternamens (hier bspw.: `cmd`) verwendet, wurde dieser vorher automatisch konvertiert.

Wurden in der Init-Methode optionale Parameter angegeben, muss vor deren Verwendung überprüft werden, dass diese nicht leer sind.

##### Artifacts 

Diese Variable ist ein Slice (Go-Array), welche alle ausgeführten Befehle, sowie die Pfade zu allen verwendeten Dateien oder Ähnlichem beinhalten sollte.

Sie wird wie folgt verwendet: 

```go
r.Artifacts = append(r.Artifacts, Artifact{
	Name: "Name des Artifakts", 
	Value: "Wert des Artifakts",
},
```

Diese Art von Artefakt ist für solche gedacht, die sich in **Textform befinden**. Beispielsweise ein Commandline-Befehl und dessen Ergebnis, wie im Fall von ExecuteCommand:

```go
r.Artifacts = append(r.Artifacts, Artifact{
	Name: params["command"],
	Value: r.ResultRaw,
},
```

Der Befehl selbst befindet sich in der ParameterMap an der Stelle "command". Er wurde im Code bereits ausgeführt und sein Ergebnis wurde in r.ResultRaw gesetzt. Das Artefakt ist somit: 

```
Name: <ausgeführter Befehl>,
Value: <Ergebnis des Befehls>,
```

Ist das Artefakte eine **Datei** wird der Pfad zu der Datei als `Value` angegeben und zusätzlich der Parameter **IsFile** angegeben:

```go
r.Artifacts = append(r.Artifacts, Artifact{
	Name:   "file",
	Value:  filePath,
	IsFile: true,
},
)
```

So kann die Datei später im [Programmoutput](#programmoutput)-Ordner gespeichert werden.

#### Result

Hier soll das Ergebnis des Moduls gespeichert werden. Dieses Ergebnis wird vom Modul selbst aus dem ausgeführten Befehl generiert und sollte nur Informationen enthalten, die relevant für den Zweck des Moduls sind. Man sollte beachten, dass der hier angegebene Wert möglichst gut von Bedingungen aus der Audit-Konfigurationsdatei überprüfbar sein sollte. Bei Modulen mit "binären" Rückgabewerten, bietet es sich an, das Result auf `true` oder `false` zu setzen. 

Bietet das Modul dies an, sollte auf den Result-Wert der Grep-Befehl angewendet werden (Siehe [Grep in Modulen](#grep-1).  

```go
r.Result = "Mein Wert"
```

#### ResultRaw

Das Ergebnis des Moduls, aber vollständig. Dies ist die vollständige Ausgabe des ausgeführten Befehls. Dies kann zusätzliche Informationen enthalten und sollte nicht vom Grep-Parameter verändert werden. 

#### Err

Hier sollte ein herkömmlicher Go-Error erzeugt werden, falls bei der Ausführung des Moduls ein Fehler auftritt.

Beispielsweise:

```go
	out, err := util.ExecCommand(params["command"])
	if err != nil {
		r.Err = err
		return
	}
```

#### Grep

Bei vielen Modulen bietet es sich an, einen optionalen Parameter `Grep` anzugeben, mit dem das Ergebnis auf den relevanten Teil zugeschnitten werden kann, bevor es zurückgegeben wird.

In der Initialize-Methode könnte das so aussehen:

```go
...

InputParams: ParameterSyntaxMap{
	"file": ParameterSyntax{
		ParamName:        "file",
		ParamAlias:       []string{"datei"},
		ParamDescription: "Pfad zur Datei",
	},
	"grep": ParameterSyntax{
		ParamName:        "grep",
		IsOptional:       true,
		ParamDescription: "Optionaler Suchbegriff, entspricht Pipen des Outputs in grep",
	},
},
```

In der Execute-Methode kann dies dann wie folgt verwendet werden:

```go
...

if params["grep"] != "" {
	r.Result = mh.Grep(ParameterMap{
		"input": r.ResultRaw,
		"grep":  params["grep"],
	}).Result
}
```

Ist der Wert des Grep-Parameters nicht leer, wird aus dem Code des Moduls das Grep-Modul mit dem korrekten Input und dem übergebenem Grep-String. Das `Result` unseres Moduls wird daraufhin auf das `Result` des Grep-Moduls gesetzt.

