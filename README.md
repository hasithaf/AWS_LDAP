##  Coding Challenge
1. Using AWS or another cloud provider, create and deploy a running instance of an LDAP server using a configuration management tool.

2. In the created instance, add a group named “techops_dba” to /etc/security/access.conf and /etc/sudoers. This may be done before or after the instance starts.

3. What is the NTP stratum of the created host? What is an acceptable load average threshold for the host?

4. Instantiate a second host and implement security so that clients are only able to access the first host from the second host. Use SSH for connectivity. This is commonly referred to as a “jump box” configuration.

5. Develop and apply automated tests to verify correctness of the LDAP server of step 1, the configuration of step 2, the results of the NTP findings of step 3, and the security restrictions of step 4.




### Refer to LDAP-Server.md
Tested on RHEL 7, running on AWS
Includes playbook and debug screens

## Second add group "techops_dba"
### Refer to ADD-Group.md


## Third check NTP stratum and load average
### Refer to NTP-stratum.md


## Forth initiate second host
### Refer to LDAP-Client.md
Tested on RHEL 7, running on AWS
Includes playbook and debug screens



