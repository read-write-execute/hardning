Ensure address space layout randomization (ASLR) is enabled	dpkg -s prelink | grep -E '(Status:|not installed)'	kernel.randomize_va_space = 2
![image](https://user-images.githubusercontent.com/30384530/155713248-dc0b7865-5064-4969-94e7-b14759e56e5f.png)


Ensure core dumps are restricted	"1. grep -Es '^(\*|\s).*hard.*core.*(\s+#.*)?$' /etc/security/limits.conf /etc/security/limits.d/*
 2. sysctl fs.suid_dumpable
 3. grep ""fs.suid_dumpable"" /etc/sysctl.conf /etc/sysctl.d/*"	"1. * hard core 0
 2. fs.suid_dumpable = 0
 3. fs.suid_dumpable = 0"
![image](https://user-images.githubusercontent.com/30384530/155713274-5ae0aa6e-8144-4e80-a23d-2efe98c04b8a.png)


Ensure AppArmor is installed	dpkg -s apparmor | grep -E '(Status:|not installed)'	Status: install ok installed
![image](https://user-images.githubusercontent.com/30384530/155713311-3cd04460-1838-4e7d-aec1-de37c966249a.png)


Ensure AppArmor is enabled in the bootloader configuration	"1. grep ""^\s*linux"" /boot/grub/grub.cfg | grep -v ""apparmor=1""
 2. grep ""^\s*linux"" /boot/grub/grub.cfg | grep -v ""security=apparmor"""	"1. Nothing should be returned
 2. Nothing should be returned"
![image](https://user-images.githubusercontent.com/30384530/155713324-c5025671-242d-4b22-b577-44decb180a3b.png)


Ensure IP forwarding is disabled	"1. sysctl net.ipv4.ip_forward
 2. grep -E -s ""^\s*net\.ipv4\.ip_forward\s*=\s*1"" /etc/sysctl.conf
 /etc/sysctl.d/*.conf /usr/lib/sysctl.d/*.conf /run/sysctl.d/*.conf
 3. sysctl net.ipv6.conf.all.forwarding
 4. grep -E -s ""^\s*net\.ipv6\.conf\.all\.forwarding\s*=\s*1"" /etc/sysctl.conf
 /etc/sysctl.d/*.conf /usr/lib/sysctl.d/*.conf /run/sysctl.d/*.conf"	"1. net.ipv4.ip_forward = 0
 2. No value should be returned
 3. net.ipv6.conf.all.forwarding = 0
 4. No value should be returned"
![image](https://user-images.githubusercontent.com/30384530/155713350-0e43855f-3e13-4295-884f-9840677dc11f.png)


Ensure suspicious packets are logged	"1. sysctl net.ipv4.conf.all.log_martians
 2. sysctl net.ipv4.conf.default.log_martians
 3. grep ""net\.ipv4\.conf\.all\.log_martians"" /etc/sysctl.conf /etc/sysctl.d/*
 4. grep ""net\.ipv4\.conf\.default\.log_martians"" /etc/sysctl.conf
 /etc/sysctl.d/*"	"1. net.ipv4.conf.all.log_martians = 1
 2. net.ipv4.conf.default.log_martians = 1
 3. net.ipv4.conf.all.log_martians = 1
 4. net.ipv4.conf.default.log_martians = 1"
![image](https://user-images.githubusercontent.com/30384530/155713368-fa9c79f6-a5c1-4a21-b284-3c09d7e6dbd6.png)


Ensure auditd is installed	dpkg -s auditd audispd-plugins	Verify auditd is installed
![image](https://user-images.githubusercontent.com/30384530/155713403-54cba690-d145-4fd4-8cfc-320589d7307f.png)


Ensure journald is configured to write logfiles to persistent disk	grep -e Storage /etc/systemd/journald.conf	Storage=persistent
![image](https://user-images.githubusercontent.com/30384530/155713645-a9698bef-018e-419c-84fd-b7c56ac8f5c5.png)

Crontab misconfiguration check	crontab -e	Shell not accessible
![image](https://user-images.githubusercontent.com/30384530/155713682-4cd8c172-241d-422a-8b00-715a7facf1fc.png)

SUID and SGID MISCONFIGURATIONS	"find / -perm +4000 -user root -type f -print
find / -perm +2000 -user root -type f -print"	priv esc
![image](https://user-images.githubusercontent.com/30384530/155713704-797ed174-4475-4156-a513-cbbdecd3be2e.png)

Ensure cron is restricted to authorized users	"1. stat /etc/cron.deny
 2. stat /etc/cron.allow"	1. stat: cannot stat `/etc/cron.deny': No such file or directory
![image](https://user-images.githubusercontent.com/30384530/155713753-4c4fa89e-7c7c-47f9-82de-d8277277c398.png)

Ensure sudo log file exists	grep -Ei '^\s*Defaults\s+logfile=\S+' /etc/sudoers /etc/sudoers.d/*	Verify that sudo has a custom log file configured
![image](https://user-images.githubusercontent.com/30384530/155713769-379e9b89-10d4-4158-80f2-35f64b457ace.png)

Ensure permissions on /etc/passwd are configured	"1. stat /etc/passwd
 2. stat /etc/passwd-"	"1. Access: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)
 2. Access: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)"	
![image](https://user-images.githubusercontent.com/30384530/155713789-5e2b54d1-a567-4043-8bce-3538ab078c5d.png)

Kernal not harden	cat /etc/sysctl.conf	Check each configuration
![image](https://user-images.githubusercontent.com/30384530/155713812-8847a5fb-d28b-4b47-8c4e-1a061db83477.png)

sudo version	sudo -V	Check version and its public exploit
![image](https://user-images.githubusercontent.com/30384530/155713843-d7a98e4b-16c5-4b91-a935-db2284f96cf1.png)

Default SSH Port configuation	cat /etc/ssh/ssh_config.d/*.conf	Check for each configuration
![image](https://user-images.githubusercontent.com/30384530/155713876-6e654787-dd0c-49b1-8a7d-413736b26591.png)


sudo misconfiguration	sudo -l	priv esc
![image](https://user-images.githubusercontent.com/30384530/155713890-9f617ebc-e21d-4101-bad1-36030d8c2ddb.png)

check the os version 	uname -a	check version with internet
![image](https://user-images.githubusercontent.com/30384530/155713928-060ecc67-b04e-4a81-bf9a-ed95840f15a9.png)


check the permission	ls -lah	check the permission with read write execute
![image](https://user-images.githubusercontent.com/30384530/155713948-bce3afac-282b-4a67-a75a-92b99305a619.png)









