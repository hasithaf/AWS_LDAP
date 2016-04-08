#  Coding Challenge

```
ansible-playbook ldapclientsetup.yml -i hosts
```


```
PLAY ***************************************************************************

TASK [setup] *******************************************************************
ok: [54.213.222.178]

TASK [clean repo] **************************************************************
changed: [54.213.222.178]

TASK [yum update] **************************************************************
ok: [54.213.222.178]

TASK [install openldap-clients, nss-pam-ldapd, autofs] *************************
changed: [54.213.222.178] => (item=[u'openldap-clients', u'nss-pam-ldapd', u'autofs'])

TASK [add entry to /etc/hosts] *************************************************
changed: [54.213.222.178] => (item=54.213.222.178  client1  client1.ldap-coding-challenge.com)
changed: [54.213.222.178] => (item=54.213.43.28  server1  server1.ldap-coding-challenge.com)

TASK [set hostname/domain] *****************************************************
changed: [54.213.222.178]

TASK [add entry to /etc/fstab] *************************************************
changed: [54.213.222.178]

TASK [start and enable autofs] *************************************************
changed: [54.213.222.178]

TASK [setup LDAP authentication] ***********************************************
changed: [54.213.222.178]

PLAY RECAP *********************************************************************
54.213.222.178             : ok=9    changed=7    unreachable=0    failed=0  
```

```
[root@new-host-10 ldap-code]# ssh ec2-user@54.213.222.178
Last login: Thu Apr  7 21:53:51 2016 from pool-100-11-29-175.phlapa.fios.verizon.net
[ec2-user@client1 ~]$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
avahi-autoipd:x:170:170:Avahi IPv4LL Stack:/var/lib/avahi-autoipd:/sbin/nologin
systemd-bus-proxy:x:999:997:systemd Bus Proxy:/:/sbin/nologin
systemd-network:x:998:996:systemd Network Management:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
polkitd:x:997:995:User for polkitd:/:/sbin/nologin
tss:x:59:59:Account used by the trousers package to sandbox the tcsd daemon:/dev/null:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
chrony:x:996:993::/var/lib/chrony:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
ec2-user:x:1000:1000:Cloud User:/home/ec2-user:/bin/bash
nscd:x:28:28:NSCD Daemon:/:/sbin/nologin
nslcd:x:65:55:LDAP Client User:/:/sbin/nologin
[ec2-user@client1 ~]$ 
[ec2-user@client1 ~]$ ls -la /home/
total 8
drwxr-xr-x.  3 root     root       21 Apr  7 16:14 .
dr-xr-xr-x. 20 root     root     4096 Apr  7 21:53 ..
drwx------.  4 ec2-user ec2-user 4096 Apr  7 21:53 ec2-user
[ec2-user@client1 ~]$ su ldapuser1
Password: 
[ldapuser1@client1 ec2-user]$ ls -la /home/
total 8
drwxr-xr-x.  4 root      root        37 Apr  7 21:57 .
dr-xr-xr-x. 20 root      root      4096 Apr  7 21:53 ..
drwx------.  4 ec2-user  ec2-user  4096 Apr  7 21:53 ec2-user
drwx------.  2 ldapuser1 ldapuser1   59 Apr  7 21:57 ldapuser1
[ldapuser1@client1 ec2-user]$ 
[ldapuser1@client1 ec2-user]$ exit 
exit
[ec2-user@client1 ~]$ 
[ec2-user@client1 ~]$ getent passwd ldapuser1
ldapuser1:x:1001:1001:ldapuser1:/home/ldapuser1:/bin/bash
[ec2-user@client1 ~]$ 
```

## Before jump-host policy
```
[root@new-host-10 ldap-code]# ssh ec2-user@54.213.43.28
Last login: Thu Apr  7 21:49:19 2016 from pool-100-11-29-175.phlapa.fios.verizon.net
[ec2-user@server1 ~]$ hostname
server1.ldap-coding-challenge.com
[ec2-user@server1 ~]$ exit
logout
Connection to 54.213.43.28 closed.
[root@new-host-10 ldap-code]# ssh ec2-user@54.213.222.178
Last login: Thu Apr  7 21:56:38 2016 from pool-100-11-29-175.phlapa.fios.verizon.net
[ec2-user@client1 ~]$ hostname
client1.ldap-coding-challenge.com
[ec2-user@client1 ~]$
```

## With jump-host policy
```
HQSML-146554:aws hferna001c$ ssh -i "awskey.pem" ec2-user@ec2-54-213-43-28.us-west-2.compute.amazonaws.com -v
OpenSSH_6.2p2, OSSLShim 0.9.8r 8 Dec 2011
debug1: Reading configuration data /Users/hferna001c/.ssh/config
debug1: /Users/hferna001c/.ssh/config line 1: Applying options for *
debug1: Reading configuration data /etc/ssh_config
debug1: /etc/ssh_config line 20: Applying options for *
debug1: Connecting to ec2-54-213-43-28.us-west-2.compute.amazonaws.com [54.213.43.28] port 22.

^C
HQSML-146554:aws hferna001c$ 
HQSML-146554:aws hferna001c$ ssh -i "awskey.pem" ec2-user@ec2-54-213-222-178.us-west-2.compute.amazonaws.com
Last login: Thu Apr  7 22:35:26 2016 from pool-100-11-29-175.phlapa.fios.verizon.net
[ec2-user@client1 ~]$ hostname
client1.ldap-coding-challenge.com
[ec2-user@client1 ~]$ 
[ec2-user@client1 ~]$ cd aws/
[ec2-user@client1 aws]$ ssh -i "awskey.pem" ec2-user@ec2-54-213-43-28.us-west-2.compute.amazonaws.com
Last login: Thu Apr  7 22:36:10 2016 from ip-172-31-29-44.us-west-2.compute.internal
[ec2-user@server1 ~]$ hostname
server1.ldap-coding-challenge.com
[ec2-user@server1 ~]$ 
[ec2-user@server1 ~]$ exit
logout
Connection to ec2-54-213-43-28.us-west-2.compute.amazonaws.com closed.
[ec2-user@client1 aws]$ exit
logout
Connection to ec2-54-213-222-178.us-west-2.compute.amazonaws.com closed.
HQSML-146554:aws hferna001c$ 
```







