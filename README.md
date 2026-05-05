# F5_CIS
F5 CIS Benchmark

F5 CIS

1.1.1
change default root password

1.1.2
change default admin password

1.1.3
password policy

Configuring the password policy using the Configuration utility 1. Log in to the Configuration utility. 2. Navigate to System > Users > Authentication. 3. Under Password Policy, locate the Secure Password Enforcement setting and set it to meet below minimum requirements : Configuring the password policy using tmsh 1. Log in to tmsh by typing the following command: tmsh: modify /auth password-policy The minimum requirements : - Secure Password Enforcement : Enabled - Minimum Password Length is 12 - Required Lowercase is 1 - Required Uppercase is 1 - Required Numeric is 1 - Required Special Characters is 1 - Maximum Duration (in Days): 180 - Minimum Duration (in Days): 90 - Expiration Warning ( in days):14 - EnsurePassword Memory is 24 - Ensure Maximum Login Failures is 3


2.1
AAA

3.1
tmsh list sys httpd auth-pam-idle-timeout
tmsh modify /sys httpd auth-pam-idle-timeout 600

3.2
tmsh list sys httpd ssl-protocol
tmsh modify /sys httpd ssl-protocol "TLSv1.2"

3.3
tmsh list /sys httpd allow
modify modify /sys httpd allow replace-all-with { <IP address or IP address range> }

4.1 ssh login banner
System > Configuration > Device > sshd
Authorized access only!
All activity may be monitored and recorded.
Unauthorized use is strictly prohibited.

4.2
tmsh list /sys sshd inactivity-timeout
tmsh modify /sys sshd inactivity-timeout 600

4.3
tmsh list /cli global-settings idle-timeout
tmsh modify /cli global-settings idle-timeout 600

4.4
tmsh list /sys global-settings console-inactivity-timeout
tmsh modify /sys global-settings console-inactivity-timeout 600

4.5 és 6 és 7
tmsh list /sys sshd all-properties
edit /sys sshd all-properties
    include "Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com
    MACs hmac-sha2-256,hmac-sha2-512
    KexAlgorithms curve25519-sha256,ecdh-sha2-nistp256"

4.8
list /sys sshd allow
tmsh modify sys sshd allow add { 192.168. 10.8. }

5.2 CVE-2003-1418
14 felett nem kell

5.1
list sys ntp servers

5.2
http e-tag - nem kell

5.3
list net self-allow

5.4
unused service - maintanace window-ban

6.1
snmp v3
1-Login to Configuration utilit
2- Go to System > SNMP > Agent > Configuration
3- Check "Client Allow List" under SNMP Access

6.2
snmp v3 only
1-Login to Configuration utility
2- Go to System > SNMP > Agent > SNMP Access (v1, v2c) : Select all listed entries and click “Delete”
3-Go to System > SNMP > Agent > SNMP Access (v3) : Make sure there is one entry at least , otherwise create one

6.3
lockdown access logs - ez ok

6.4
audit logging for "MCP, tmsh and GUI" is set to enabled
1-Login to Configuration utility
2-Go to System > Logs > Configuration > Options
3- Under Audit Logging : Select “Enable” for all items : “MCP” , “tmsh” and "GUI"

GUI-t be kell kapcsolni
