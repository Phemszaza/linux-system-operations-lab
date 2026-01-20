Linux System Operations and ITIL Practice Lab

Day 1 Documentation

⸻

Project Overview

This project simulates a small enterprise Linux environment to practice system administration, service management, incident handling, logging, and automation.
The lab follows a structured, test before production approach aligned with ITIL and operational best practices.

⸻

Environment Overview

Systems

Server Name	Role	Purpose
prod-linux-01	Production Server	Hosts production services
test-linux-01	Test Server	Used for testing and validation

Operating System
	•	Ubuntu Server 22.04 LTS

Virtualization
	•	Virtual machines running locally
	•	Network mode: NAT or Bridged

⸻

Day 1 Objectives
	•	Build and prepare Linux servers
	•	Install and manage services
	•	Apply user and permission controls
	•	Simulate and resolve incidents
	•	Analyze logs and monitor systems
	•	Implement backups and basic automation
	•	Document all actions professionally

⸻

STEP 1: Linux Environment Setup

Actions Performed
	•	Installed Ubuntu Server 22.04 LTS on two virtual machines
	•	Configured hostnames using hostnamectl
	•	Created a dedicated admin user sysadmin
	•	Enabled and verified SSH access
	•	Updated all system packages
	•	Verified network connectivity
	•	Created initial system documentation

Verification Commands

hostnamectl
whoami
ip a
systemctl status ssh
sudo apt update && sudo apt upgrade -y

Result

Both servers boot successfully, are fully updated, reachable via SSH, and ready for administration.



STEP 2: Service Installation, Users, and Permissions

Service Installation
	•	Installed Apache web server on test system first
	•	Verified service status and accessibility
	•	Repeated installation on production system

Commands used:

sudo apt install apache2 -y
systemctl status apache2
curl http://localhost

User Management
	•	Created a standard non privileged user appuser
	•	Ensured user does not have sudo access

sudo adduser appuser
groups appuser

Permission Configuration
	•	Created controlled shared directory /var/www/appdata
	•	Applied group based permissions following least privilege

sudo mkdir /var/www/appdata
sudo chown root:appuser /var/www/appdata
sudo chmod 750 /var/www/appdata

Result

Service runs correctly, user access is restricted appropriately, and permissions are enforced.

⸻

STEP 3: Incident Simulation and Troubleshooting

Incident 1: Apache Service Down

Symptoms
	•	Website not reachable
	•	Apache inactive

Diagnosis

systemctl status apache2
journalctl -u apache2

Resolution

sudo systemctl start apache2


⸻

Incident 2: Permission Denied Error

Symptoms
	•	User unable to write to web directory

Diagnosis

ls -ld /var/www/html

Resolution

sudo chown root:appuser /var/www/html
sudo chmod 775 /var/www/html


⸻

Incident 3: Service Not Starting at Boot

Symptoms
	•	Apache not running after reboot

Diagnosis

systemctl is-enabled apache2

Resolution

sudo systemctl enable apache2


⸻

STEP 4: Logs, Monitoring, and Security Checks

Log Analysis
	•	Reviewed system logs
	•	Reviewed authentication logs
	•	Analyzed Apache access and error logs

tail /var/log/syslog
tail /var/log/auth.log
tail /var/log/apache2/access.log
tail /var/log/apache2/error.log

Monitoring
	•	Checked system uptime and load
	•	Monitored CPU and memory usage
	•	Verified disk usage

uptime
top
df -h

Security Checks
	•	Reviewed active sessions
	•	Checked sudo usage history

who
last
grep sudo /var/log/auth.log


⸻

STEP 5: Backups and Automation

Backup Setup
	•	Created secured backup directory
	•	Performed manual backup of web data and configuration

sudo mkdir /backup
sudo chmod 700 /backup
sudo tar -czvf /backup/web_backup_YYYY-MM-DD.tar.gz /var/www /etc/apache2

Restore Verification
	•	Tested extraction to temporary location to validate backup integrity

sudo tar -xzvf /backup/web_backup_DATE.tar.gz -C /tmp/restore-test


⸻

Automation with Cron
	•	Configured daily automated backups at 02:00 AM
	•	Backup runs as root
	•	Date based naming implemented

sudo crontab -e

Cron job:

0 2 * * * tar -czf /backup/web_backup_$(date +\%F).tar.gz /var/www /etc/apache2

Result

Backups are automated, protected, and verified.

⸻

Final Outcome of Day 1

By completing Day 1, the following competencies were demonstrated:
	•	Linux system installation and preparation
	•	Service management using systemd
	•	Secure user and permission management
	•	Incident handling and troubleshooting
	•	Log analysis and system monitoring
	•	Backup creation and automation
	•	Professional documentation practices

⸻

Summary Statement

Built and administered a two server Linux environment with production and test separation. Installed and managed services, 
applied least privilege user access, simulated and resolved incidents, analyzed logs, implemented automated backups, 
and documented all operational activities.

⸻

Next Steps

Day 2 will focus on:
	•	Linux networking fundamentals
	•	Port and service inspection
	•	Firewall configuration
	•	Network troubleshooting scenarios

