
Day 2 Documentation

Networking and Security Fundamentals

⸻

Day 2 Overview

Day 2 focuses on Linux networking fundamentals and basic security configuration.
The objective is to understand how a Linux server communicates within a network, how services expose ports, and how firewall rules protect systems.

All tasks were performed on the test system first and then applied to production following test before production best practices.

⸻

Environment

Server Name	Role
test-linux-01	Test Server
prod-linux-01	Production Server

Operating System:
	•	Ubuntu Server 22.04 LTS upgraded to ubuntu server 24.04 LTS

Network Mode:
	•	NAT or Bridged

⸻

Day 2 Objectives
	•	Verify network configuration and connectivity
	•	Understand IP addressing and routing
	•	Inspect open ports and running services
	•	Configure firewall rules securely
	•	Test firewall behavior
	•	Practice structured network troubleshooting
	•	Document networking and security changes

⸻

STEP 1: Network Configuration Verification

Network Interface and IP Address

Command used:

ip a

Verified:
	•	Network interface is UP
	•	IPv4 address assigned via DHCP
	•	Interface name identified correctly

⸻

Routing Configuration

Command used:

ip route

Verified:
	•	Default route exists
	•	Gateway is correctly configured

This confirms how outbound traffic is routed.

⸻

STEP 2: Connectivity and DNS Testing

Local Network Connectivity

ping -c 3 <gateway-ip>

Result:
	•	Successful response from gateway

⸻

External Network Connectivity

ping -c 3 8.8.8.8

Result:
	•	Internet connectivity confirmed

⸻

DNS Resolution Test

ping -c 3 google.com

Result:
	•	Hostname successfully resolved
	•	DNS functioning correctly

⸻

STEP 3: Ports and Services Inspection

Checking Listening Services and Ports

Command used:

ss -tulnp

Observed:
	•	SSH service listening on port 22
	•	Apache service listening on port 80

This confirms services are running and bound to expected ports.

⸻

STEP 4: Firewall Configuration with UFW

Firewall Status Check

sudo ufw status

Initial state:
	•	Firewall inactive

⸻

Safe Firewall Enablement

Allowed essential services before enabling firewall:

sudo ufw allow ssh
sudo ufw allow http
sudo ufw enable

This prevents administrative lockout and ensures service availability.

⸻

Firewall Rule Verification

sudo ufw status verbose

Confirmed:
	•	SSH allowed
	•	HTTP allowed
	•	Default deny incoming policy active
	•	Firewall enabled successfully

⸻

STEP 5: Firewall Behavior Testing

Allowed Traffic Verification
	•	SSH access tested successfully
	•	Apache web page accessible via browser

⸻

Simulated Blocked Traffic

sudo ufw deny http

Result:
	•	Web service became unreachable

Restored access:

sudo ufw allow http

This confirms firewall rules are enforced correctly.

⸻

STEP 6: Network Troubleshooting Scenario

Scenario

Apache service is running but the website is not reachable.

Troubleshooting Steps
	1.	Verify service status

systemctl status apache2
  2.	Confirm service is listening on port 80

ss -tulnp | grep :80
  3.	Check firewall rules

sudo ufw status
	4.	Test IP reachability

ping <server-ip>

This structured approach reflects real world operational troubleshooting.

⸻

Change and Documentation Discipline
	•	All changes were tested on test-linux-01
	•	Verified for impact and correctness
	•	Applied to prod-linux-01 after validation
	•	All steps documented for traceability

⸻

Day 2 Outcome

By completing Day 2, the following skills were demonstrated:
	•	Linux network interface and routing verification
	•	Connectivity and DNS troubleshooting
	•	Port and service inspection
	•	Firewall configuration using UFW
	•	Secure rule deployment
	•	Structured network troubleshooting
	•	Professional documentation practices

⸻

Summary Statement

Verified Linux networking by checking IP configuration, routing, and DNS resolution. Inspected active ports 
and services, configured a firewall using UFW with least privilege rules, tested allowed and blocked traffic, 
and applied structured troubleshooting techniques.

⸻

Next Steps

Day 3 will focus on:
	•	User and group management
	•	Password and access policies
	•	Basic security hardening
	•	Account and permission auditing

