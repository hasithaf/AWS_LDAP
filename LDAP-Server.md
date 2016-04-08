#  Coding Challenge

```
ansible-playbook ldapserversetup.yml -i hosts
```


```
PLAY ***************************************************************************

TASK [setup] *******************************************************************
ok: [54.213.43.28]

TASK [clean repo] **************************************************************
changed: [54.213.43.28]

TASK [yum update] **************************************************************
ok: [54.213.43.28]

TASK [install openldap*, migrationtools, nfs-utils, rpcbind] *******************
changed: [54.213.43.28] => (item=[u'*openldap*', u'openldap-clients', u'migrationtools', u'nfs-utils', u'rpcbind'])

TASK [add entry to /etc/hosts] *************************************************
changed: [54.213.43.28]

TASK [set hostname/domain] *****************************************************
changed: [54.213.43.28]

TASK [create ldap admin secret-passwd] *****************************************
changed: [54.213.43.28]

TASK [create a symlink for olcDatabase={2}bdb.ldif] ****************************
changed: [54.213.43.28]

TASK [edit olcDatabase={2}bdb.ldif] ********************************************
changed: [54.213.43.28] => (item={u'line': u'olcAccess: {2}to * by dn="cn=Manager,dc=ldap-coding-challenge,dc=com" write  by * read', u'reg': u'olcAccess: \\{2\\}.*'})
changed: [54.213.43.28] => (item={u'line': u'olcSuffix: dc=ldap-coding-challenge,dc=com', u'reg': u'olcSuffix:.*'})
changed: [54.213.43.28] => (item={u'line': u'olcRootDN: cn=Manager,dc=ldap-coding-challenge,dc=com', u'reg': u'olcRootDN:.*'})
changed: [54.213.43.28] => (item={u'line': u'olcRootPW: {SSHA}xykOyMpUddWhDTw3sJ0vLXmebrgsY/r/', u'reg': u'olcRootPW:.*'})
changed: [54.213.43.28] => (item={u'line': u'olcTLSCertificateFile: /etc/pki/CA/cacert.pem', u'reg': u'olcTLSCertificateFile:.*'})
changed: [54.213.43.28] => (item={u'line': u'olcTLSCertificateKeyFile: /etc/pki/CA/private/cakey.pem', u'reg': u'olcTLSCertificateKeyFile:.*'})

TASK [create a symlink for olcDatabase={1}monitor.ldif] ************************
changed: [54.213.43.28]

TASK [edit olcDatabase={2}bdb.ldif] ********************************************
changed: [54.213.43.28] => (item={u'state': u'present', u'line': u'olcAccess: {0}to * by dn.base="gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth" read by dn.base="cn=Manager,dc=ldap-coding-challenge,dc=com" read by * none', u'reg': u'olcAccess:.*$'})
changed: [54.213.43.28] => (item={u'state': u'absent', u'line': u'', u'reg': u'^ al,cn=auth".*$'})

TASK [generate a X509 self sign certificate] ***********************************
changed: [54.213.43.28]

TASK [debug] *******************************************************************
ok: [54.213.43.28] => {
    "msg": {
        "changed": true, 
        "cmd": "openssl req -new -x509 -nodes -out /etc/pki/CA/cacert.pem -keyout /etc/pki/CA/private/cakey.pem -subj \"/CN=server1.ldap-coding-challenge.com\" -days 365", 
        "delta": "0:00:00.097360", 
        "end": "2016-04-07 21:28:47.082264", 
        "rc": 0, 
        "start": "2016-04-07 21:28:46.984904", 
        "stderr": "Generating a 2048 bit RSA private key\n..........+++\n............................................+++\nwriting new private key to '/etc/pki/CA/private/cakey.pem'\n-----", 
        "stdout": "", 
        "stdout_lines": [], 
        "warnings": []
    }
}

TASK [set permission to /etc/pki/CA/cacert.pem] ********************************
changed: [54.213.43.28]

TASK [set permission to /etc/pki/CA/private/cakey.pem] *************************
changed: [54.213.43.28]

TASK [prepare LDAP database] ***************************************************
changed: [54.213.43.28]

TASK [set permission to /var/lib/ldap/] ****************************************
changed: [54.213.43.28]

TASK [edit /etc/sysconfig/slapd] ***********************************************
changed: [54.213.43.28]

TASK [test ldap configuration] *************************************************
changed: [54.213.43.28]

TASK [debug] *******************************************************************
ok: [54.213.43.28] => {
    "msg": {
        "changed": true, 
        "cmd": "slaptest -u", 
        "delta": "0:00:00.008739", 
        "end": "2016-04-07 21:28:56.124817", 
        "rc": 0, 
        "start": "2016-04-07 21:28:56.116078", 
        "stderr": "57070958 ldif_read_file: checksum error on \"/etc/openldap/slapd.d/cn=config/olcDatabase={1}monitor.ldif\"\n57070958 ldif_read_file: checksum error on \"/etc/openldap/slapd.d/cn=config/olcDatabase={2}hdb.ldif\"\nconfig file testing succeeded", 
        "stdout": "", 
        "stdout_lines": [], 
        "warnings": []
    }
}

TASK [start and enable slapd at boot] ******************************************
changed: [54.213.43.28]

TASK [check LDAP] **************************************************************
changed: [54.213.43.28]

TASK [debug] *******************************************************************
ok: [54.213.43.28] => {
    "msg": {
        "changed": true, 
        "cmd": "netstat -lt |grep ldap; netstat -tunlp |egrep '389|636'", 
        "delta": "0:00:00.034378", 
        "end": "2016-04-07 21:28:59.562110", 
        "rc": 0, 
        "start": "2016-04-07 21:28:59.527732", 
        "stderr": "", 
        "stdout": "tcp        0      0 0.0.0.0:ldaps           0.0.0.0:*               LISTEN     \ntcp        0      0 0.0.0.0:ldap            0.0.0.0:*               LISTEN     \ntcp6       0      0 [::]:ldaps              [::]:*                  LISTEN     \ntcp6       0      0 [::]:ldap               [::]:*                  LISTEN     \ntcp        0      0 0.0.0.0:636             0.0.0.0:*               LISTEN      27807/slapd         \ntcp        0      0 0.0.0.0:389             0.0.0.0:*               LISTEN      27807/slapd         \ntcp6       0      0 :::636                  :::*                    LISTEN      27807/slapd         \ntcp6       0      0 :::389                  :::*                    LISTEN      27807/slapd         ", 
        "stdout_lines": [
            "tcp        0      0 0.0.0.0:ldaps           0.0.0.0:*               LISTEN     ", 
            "tcp        0      0 0.0.0.0:ldap            0.0.0.0:*               LISTEN     ", 
            "tcp6       0      0 [::]:ldaps              [::]:*                  LISTEN     ", 
            "tcp6       0      0 [::]:ldap               [::]:*                  LISTEN     ", 
            "tcp        0      0 0.0.0.0:636             0.0.0.0:*               LISTEN      27807/slapd         ", 
            "tcp        0      0 0.0.0.0:389             0.0.0.0:*               LISTEN      27807/slapd         ", 
            "tcp6       0      0 :::636                  :::*                    LISTEN      27807/slapd         ", 
            "tcp6       0      0 :::389                  :::*                    LISTEN      27807/slapd         "
        ], 
        "warnings": []
    }
}

TASK [add the LDAP schemas] ****************************************************
changed: [54.213.43.28]

TASK [debug] *******************************************************************
ok: [54.213.43.28] => {
    "msg": {
        "changed": true, 
        "cmd": "ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/cosine.ldif\n ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/nis.ldif\n ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/inetorgperson.ldif", 
        "delta": "0:00:00.019584", 
        "end": "2016-04-07 21:29:01.140506", 
        "rc": 0, 
        "start": "2016-04-07 21:29:01.120922", 
        "stderr": "SASL/EXTERNAL authentication started\nSASL username: gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth\nSASL SSF: 0\nSASL/EXTERNAL authentication started\nSASL username: gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth\nSASL SSF: 0\nSASL/EXTERNAL authentication started\nSASL username: gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth\nSASL SSF: 0", 
        "stdout": "adding new entry \"cn=cosine,cn=schema,cn=config\"\n\nadding new entry \"cn=nis,cn=schema,cn=config\"\n\nadding new entry \"cn=inetorgperson,cn=schema,cn=config\"", 
        "stdout_lines": [
            "adding new entry \"cn=cosine,cn=schema,cn=config\"", 
            "", 
            "adding new entry \"cn=nis,cn=schema,cn=config\"", 
            "", 
            "adding new entry \"cn=inetorgperson,cn=schema,cn=config\""
        ], 
        "warnings": []
    }
}

TASK [edit migrate_common.ph] **************************************************
changed: [54.213.43.28] => (item={u'line': u'$DEFAULT_MAIL_DOMAIN = "ldap-coding-challenge.com";', u'reg': u'DEFAULT_MAIL_DOMAIN = ".*$'})
changed: [54.213.43.28] => (item={u'line': u'$DEFAULT_BASE = "dc=ldap-coding-challenge,dc=com";', u'reg': u'DEFAULT_BASE = ".*$'})
changed: [54.213.43.28] => (item={u'line': u'$EXTENDED_SCHEMA = 1;', u'reg': u'EXTENDED_SCHEMA = 0.*$'})

TASK [generate and load base.ldif] *********************************************
changed: [54.213.43.28]

TASK [debug] *******************************************************************
ok: [54.213.43.28] => {
    "msg": {
        "changed": true, 
        "cmd": "/usr/share/migrationtools/migrate_base.pl > /root/base.ldif\n ldapadd -x -w redhat -D \"cn=Manager,dc=ldap-coding-challenge,dc=com\" -f /root/base.ldif", 
        "delta": "0:00:00.041698", 
        "end": "2016-04-07 21:29:07.388306", 
        "rc": 0, 
        "start": "2016-04-07 21:29:07.346608", 
        "stderr": "", 
        "stdout": "adding new entry \"dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"ou=Hosts,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"ou=Rpc,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"ou=Services,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"nisMapName=netgroup.byuser,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"ou=Mounts,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"ou=Networks,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"ou=People,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"ou=Group,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"ou=Netgroup,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"ou=Protocols,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"ou=Aliases,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"nisMapName=netgroup.byhost,dc=ldap-coding-challenge,dc=com\"", 
        "stdout_lines": [
            "adding new entry \"dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"ou=Hosts,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"ou=Rpc,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"ou=Services,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"nisMapName=netgroup.byuser,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"ou=Mounts,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"ou=Networks,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"ou=People,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"ou=Group,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"ou=Netgroup,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"ou=Protocols,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"ou=Aliases,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"nisMapName=netgroup.byhost,dc=ldap-coding-challenge,dc=com\""
        ], 
        "warnings": []
    }
}

TASK [add ldapuser1/2] *********************************************************
changed: [54.213.43.28]

TASK [generate /root/users, root/shadow, /root/groups for ldap auth] ***********
changed: [54.213.43.28]

TASK [remove ldapuser1/2] ******************************************************
changed: [54.213.43.28] => (item=ldapuser1)
changed: [54.213.43.28] => (item=ldapuser2)

TASK [edit migrate_common.ph] **************************************************
changed: [54.213.43.28] => (item={u'line': u'        open(SHADOW, "/root/shadow") || return;', u'reg': u'SHADOW, "/etc/shadow"'})

TASK [create /root/users.ldif, /root/groups.ldif for ldap auth] ****************
changed: [54.213.43.28]

TASK [upload users and groups ldif file to LDAP DB] ****************************
changed: [54.213.43.28]

TASK [debug] *******************************************************************
ok: [54.213.43.28] => {
    "msg": {
        "changed": true, 
        "cmd": "ldapadd -x -w redhat -D \"cn=Manager,dc=ldap-coding-challenge,dc=com\" -f /root/users.ldif\n ldapadd -x -w redhat -D \"cn=Manager,dc=ldap-coding-challenge,dc=com\" -f /root/groups.ldif", 
        "delta": "0:00:00.046407", 
        "end": "2016-04-07 21:29:18.921169", 
        "rc": 0, 
        "start": "2016-04-07 21:29:18.874762", 
        "stderr": "", 
        "stdout": "adding new entry \"uid=ec2-user,ou=People,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"uid=ldapuser1,ou=People,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"uid=ldapuser2,ou=People,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"cn=ec2-user,ou=Group,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"cn=ldapuser1,ou=Group,dc=ldap-coding-challenge,dc=com\"\n\nadding new entry \"cn=ldapuser2,ou=Group,dc=ldap-coding-challenge,dc=com\"", 
        "stdout_lines": [
            "adding new entry \"uid=ec2-user,ou=People,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"uid=ldapuser1,ou=People,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"uid=ldapuser2,ou=People,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"cn=ec2-user,ou=Group,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"cn=ldapuser1,ou=Group,dc=ldap-coding-challenge,dc=com\"", 
            "", 
            "adding new entry \"cn=ldapuser2,ou=Group,dc=ldap-coding-challenge,dc=com\""
        ], 
        "warnings": []
    }
}

TASK [test LDAP] ***************************************************************
changed: [54.213.43.28]

TASK [debug] *******************************************************************
ok: [54.213.43.28] => {
    "msg": [
        "# extended LDIF", 
        "#", 
        "# LDAPv3", 
        "# base <dc=ldap-coding-challenge,dc=com> with scope subtree", 
        "# filter: (objectclass=*)", 
        "# requesting: ALL", 
        "#", 
        "", 
        "# ldap-coding-challenge.com", 
        "dn: dc=ldap-coding-challenge,dc=com", 
        "dc: ldap-coding-challenge", 
        "objectClass: top", 
        "objectClass: domain", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# Hosts, ldap-coding-challenge.com", 
        "dn: ou=Hosts,dc=ldap-coding-challenge,dc=com", 
        "ou: Hosts", 
        "objectClass: top", 
        "objectClass: organizationalUnit", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# Rpc, ldap-coding-challenge.com", 
        "dn: ou=Rpc,dc=ldap-coding-challenge,dc=com", 
        "ou: Rpc", 
        "objectClass: top", 
        "objectClass: organizationalUnit", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# Services, ldap-coding-challenge.com", 
        "dn: ou=Services,dc=ldap-coding-challenge,dc=com", 
        "ou: Services", 
        "objectClass: top", 
        "objectClass: organizationalUnit", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# netgroup.byuser, ldap-coding-challenge.com", 
        "dn: nisMapName=netgroup.byuser,dc=ldap-coding-challenge,dc=com", 
        "nisMapName: netgroup.byuser", 
        "objectClass: top", 
        "objectClass: nisMap", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# Mounts, ldap-coding-challenge.com", 
        "dn: ou=Mounts,dc=ldap-coding-challenge,dc=com", 
        "ou: Mounts", 
        "objectClass: top", 
        "objectClass: organizationalUnit", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# Networks, ldap-coding-challenge.com", 
        "dn: ou=Networks,dc=ldap-coding-challenge,dc=com", 
        "ou: Networks", 
        "objectClass: top", 
        "objectClass: organizationalUnit", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# People, ldap-coding-challenge.com", 
        "dn: ou=People,dc=ldap-coding-challenge,dc=com", 
        "ou: People", 
        "objectClass: top", 
        "objectClass: organizationalUnit", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# Group, ldap-coding-challenge.com", 
        "dn: ou=Group,dc=ldap-coding-challenge,dc=com", 
        "ou: Group", 
        "objectClass: top", 
        "objectClass: organizationalUnit", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# Netgroup, ldap-coding-challenge.com", 
        "dn: ou=Netgroup,dc=ldap-coding-challenge,dc=com", 
        "ou: Netgroup", 
        "objectClass: top", 
        "objectClass: organizationalUnit", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# Protocols, ldap-coding-challenge.com", 
        "dn: ou=Protocols,dc=ldap-coding-challenge,dc=com", 
        "ou: Protocols", 
        "objectClass: top", 
        "objectClass: organizationalUnit", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# Aliases, ldap-coding-challenge.com", 
        "dn: ou=Aliases,dc=ldap-coding-challenge,dc=com", 
        "ou: Aliases", 
        "objectClass: top", 
        "objectClass: organizationalUnit", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# netgroup.byhost, ldap-coding-challenge.com", 
        "dn: nisMapName=netgroup.byhost,dc=ldap-coding-challenge,dc=com", 
        "nisMapName: netgroup.byhost", 
        "objectClass: top", 
        "objectClass: nisMap", 
        "objectClass: domainRelatedObject", 
        "associatedDomain: ldap-coding-challenge.com", 
        "", 
        "# ec2-user, People, ldap-coding-challenge.com", 
        "dn: uid=ec2-user,ou=People,dc=ldap-coding-challenge,dc=com", 
        "uid: ec2-user", 
        "cn: Cloud User", 
        "givenName: Cloud", 
        "sn: User", 
        "mail: ec2-user@ldap-coding-challenge.com", 
        "objectClass: person", 
        "objectClass: organizationalPerson", 
        "objectClass: inetOrgPerson", 
        "objectClass: posixAccount", 
        "objectClass: top", 
        "userPassword:: e2NyeXB0fXg=", 
        "loginShell: /bin/bash", 
        "uidNumber: 1000", 
        "gidNumber: 1000", 
        "homeDirectory: /home/ec2-user", 
        "gecos: Cloud User", 
        "", 
        "# ldapuser1, People, ldap-coding-challenge.com", 
        "dn: uid=ldapuser1,ou=People,dc=ldap-coding-challenge,dc=com", 
        "uid: ldapuser1", 
        "cn: ldapuser1", 
        "sn: ldapuser1", 
        "mail: ldapuser1@ldap-coding-challenge.com", 
        "objectClass: person", 
        "objectClass: organizationalPerson", 
        "objectClass: inetOrgPerson", 
        "objectClass: posixAccount", 
        "objectClass: top", 
        "objectClass: shadowAccount", 
        "userPassword:: e2NyeXB0fSQ2JDZSRG1OS1dOJDYzczF0cjA3Q0R6WFN2WFJOZXJkbVFXSnpBSmx", 
        " DVEo1b0svcy9rdVBKWjhodDd4Vi4xLmlJZlo4bDNUM3VJUDkxZmRDZHo0cDhEVDdPMnFGM1JnQk8v", 
        "shadowLastChange: 16899", 
        "shadowMin: 0", 
        "shadowMax: 99999", 
        "shadowWarning: 7", 
        "loginShell: /bin/bash", 
        "uidNumber: 1001", 
        "gidNumber: 1001", 
        "homeDirectory: /home/ldapuser1", 
        "", 
        "# ldapuser2, People, ldap-coding-challenge.com", 
        "dn: uid=ldapuser2,ou=People,dc=ldap-coding-challenge,dc=com", 
        "uid: ldapuser2", 
        "cn: ldapuser2", 
        "sn: ldapuser2", 
        "mail: ldapuser2@ldap-coding-challenge.com", 
        "objectClass: person", 
        "objectClass: organizationalPerson", 
        "objectClass: inetOrgPerson", 
        "objectClass: posixAccount", 
        "objectClass: top", 
        "objectClass: shadowAccount", 
        "userPassword:: e2NyeXB0fSQ2JHNwYkYxZUVWJHNaMFhkUDhSWFBxZHd0L3YwaHduQWNPSE1pcG1", 
        " PQWUySjhRbERnMWkvY2liMEhUVDd1MWRyZkR4ZVphZmlLWFVPaUFSTXNWU21YaW5VSXI3R0Q4aTMv", 
        "shadowLastChange: 16899", 
        "shadowMin: 0", 
        "shadowMax: 99999", 
        "shadowWarning: 7", 
        "loginShell: /bin/bash", 
        "uidNumber: 1002", 
        "gidNumber: 1002", 
        "homeDirectory: /home/ldapuser2", 
        "", 
        "# ec2-user, Group, ldap-coding-challenge.com", 
        "dn: cn=ec2-user,ou=Group,dc=ldap-coding-challenge,dc=com", 
        "objectClass: posixGroup", 
        "objectClass: top", 
        "cn: ec2-user", 
        "userPassword:: e2NyeXB0fXg=", 
        "gidNumber: 1000", 
        "", 
        "# ldapuser1, Group, ldap-coding-challenge.com", 
        "dn: cn=ldapuser1,ou=Group,dc=ldap-coding-challenge,dc=com", 
        "objectClass: posixGroup", 
        "objectClass: top", 
        "cn: ldapuser1", 
        "userPassword:: e2NyeXB0fXg=", 
        "gidNumber: 1001", 
        "", 
        "# ldapuser2, Group, ldap-coding-challenge.com", 
        "dn: cn=ldapuser2,ou=Group,dc=ldap-coding-challenge,dc=com", 
        "objectClass: posixGroup", 
        "objectClass: top", 
        "cn: ldapuser2", 
        "userPassword:: e2NyeXB0fXg=", 
        "gidNumber: 1002", 
        "", 
        "# search result", 
        "search: 2", 
        "result: 0 Success", 
        "", 
        "# numResponses: 20", 
        "# numEntries: 19"
    ]
}

TASK [edit /etc/exports] *******************************************************
changed: [54.213.43.28]

TASK [start and enable nfs at boot] ********************************************
failed: [54.213.43.28] => (item=nfs) => {"failed": true, "item": "nfs", "msg": "Error when trying to enable nfs: rc=1 Failed to execute operation: No such file or directory\n"}
changed: [54.213.43.28] => (item=rpcbind)
...ignoring

TASK [test nfs] ****************************************************************
fatal: [54.213.43.28]: FAILED! => {"changed": true, "cmd": "showmount -e", "delta": "0:00:00.050058", "end": "2016-04-07 21:29:26.844296", "failed": true, "rc": 1, "start": "2016-04-07 21:29:26.794238", "stderr": "clnt_create: RPC: Program not registered", "stdout": "", "stdout_lines": [], "warnings": []}
...ignoring

TASK [debug] *******************************************************************
ok: [54.213.43.28] => {
    "msg": []
}

PLAY RECAP *********************************************************************
54.213.43.28               : ok=41   changed=29   unreachable=0    failed=0  
```


