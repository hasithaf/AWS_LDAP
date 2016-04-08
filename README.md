##  Coding Challenge
###1. Using AWS or another cloud provider, create and deploy a running instance of an LDAP server using a configuration management tool.
- ldapserversetup.yml has insctructions to install and configure LDAP.
- Refer to LDAP-Server.md for playbook run and output of LDAP install and authentication.


###2. In the created instance, add a group named “techops_dba” to /etc/security/access.conf and /etc/sudoers. This may be done before or after the instance starts.
- addgroup.yml take care of adding  “techops_dba” to access.conf and sudoers.
- Refer to ADD-Group.md for playbook run and output of passwd, access.conf and sudoers files.


###3. What is the NTP stratum of the created host? What is an acceptable load average threshold for the host?
- ntp-loadaverage.yml does install NTP service and check for stratum, also check for cpu load.
- Refer to NTP-stratum.md for playbook run and output of stratum and load average. 


###4. Instantiate a second host and implement security so that clients are only able to access the first host from the second host. Use SSH for connectivity. This is commonly referred to as a “jump box” configuration.
- ldapclientsetup.yml does install LDAP client portion and binds to LDAP server.
- Refer to LDAP-Client.md for playbook run, and client verification.


###5. Develop and apply automated tests to verify correctness of the LDAP server of step 1, the configuration of step 2, the results of the NTP findings of step 3, and the security restrictions of step 4.
1. LDAP-Server.md has debug capture to show LDAP server setup and its function.
2. ADD-Group.md shows debug capture and output of passwd, access.conf and sudoers files to support configuration.
3. NTP-stratum.md has results of NTP findings.
4. LDAP-Client.md has results for security restrictions as a junp-server.






