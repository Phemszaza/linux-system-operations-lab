Day 3 Documentation

User, Group, and Security Hardening

⸻

Day 3 Overview

Day 3 focuses on user and group management, access control, and basic system security hardening.
The goal is to apply least privilege principles, enforce password policies, secure SSH access, and perform basic security auditing.

All changes were tested on the test system before being applied to production.

⸻

Environment

Server Name	Role
test-linux-01	Test Server
prod-linux-01	Production Server

Operating System:
	•	Ubuntu Server 22.04 LTS

⸻

Day 3 Objectives
	•	Review existing users and groups
	•	Implement role based access control
	•	Enforce password expiration policies
	•	Harden SSH configuration
	•	Restrict sudo privileges
	•	Perform basic security auditing
	•	Document security related changes

⸻

STEP 1: User and Group Review

User Enumeration

Command used:

cut -d: -f1 /etc/passwd

Purpose:
	•	Identify system users
	•	Distinguish service accounts from human users

⸻

Group Membership Verification

Commands used:

groups sysadmin
groups appuser

Verified:
	•	sysadmin is a member of the sudo group
	•	appuser does not have administrative privileges

⸻

STEP 2: Role Based Group Management

Group Creation

Commands used:

sudo groupadd webadmins
sudo groupadd auditors

Purpose:
	•	Manage permissions using groups instead of individual users

⸻

Assign Users to Groups

Commands used:

sudo usermod -aG webadmins sysadmin
sudo usermod -aG auditors appuser

Verification:

groups sysadmin
groups appuser

Result:
	•	Role based access successfully applied

⸻

STEP 3: Password Policy Enforcement

Review Password Settings

Command used:

sudo chage -l sysadmin


⸻

Enforce Password Expiration

Commands used:

sudo chage -M 90 sysadmin
sudo chage -W 7 sysadmin

Policy applied:
	•	Password expires every 90 days
	•	User receives warning 7 days before expiration

⸻

Force Password Change on Next Login

Command used:

sudo chage -d 0 appuser

Purpose:
	•	Enforce secure first login behavior

⸻

STEP 4: SSH Hardening

SSH Configuration Changes

File edited:

/etc/ssh/sshd_config

Settings applied:

PermitRootLogin no
StrictModes yes
MaxAuthTries 3
PasswordAuthentication yes

Purpose:
	•	Disable direct root SSH access
	•	Reduce brute force attack attempts
	•	Enforce secure file permission checks

⸻

Apply SSH Configuration

Command used:

sudo systemctl restart ssh

Verification:
	•	SSH access tested successfully using non root user
	•	Existing session kept open during testing to prevent lockout

⸻

STEP 5: Sudo Access Restriction

Review Sudo Group Membership

Command used:

getent group sudo

Verified:
	•	Only sysadmin has full sudo privileges

⸻

Limited Sudo Rule Configuration

Command used:

sudo visudo

Rule added:

%webadmins ALL=(ALL) /bin/systemctl restart apache2

Purpose:
	•	Allow web administrators to restart Apache only
	•	Prevent unrestricted administrative access

⸻

Verification

Commands tested:

sudo systemctl restart apache2
sudo reboot

Result:
	•	Apache restart permitted
	•	System reboot denied

⸻

STEP 6: Basic Security Auditing

Failed Login Attempts

Command used:

sudo grep "Failed password" /var/log/auth.log


⸻

Login History

Command used:

last


⸻

Active Sessions

Command used:

who

Purpose:
	•	Monitor authentication activity
	•	Detect unusual access patterns

⸻

Change and Deployment Discipline
	•	All security changes tested on test-linux-01
	•	Verified for correct behavior
	•	Applied to prod-linux-01 after validation
	•	SSH access tested after every configuration change
	•	Documentation updated for traceability

⸻

Day 3 Outcome

By completing Day 3, the following skills were demonstrated:
	•	Linux user and group management
	•	Role based access control
	•	Password expiration and enforcement
	•	SSH service hardening
	•	Sudo privilege restriction
	•	Basic system security auditing
	•	Professional documentation practices

⸻
Summary Statement

Managed users and groups using role based access control, enforced password policies, hardened SSH by 
disabling root login and limiting authentication attempts, restricted sudo privileges using command 
level rules, and performed basic security auditing.

⸻

Next Steps

Day 4 will focus on:
	•	Storage management
	•	Filesystems and mounts
	•	Disk usage monitoring
	•	Backup and recovery extension

⸻

