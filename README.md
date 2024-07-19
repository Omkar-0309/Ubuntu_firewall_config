# Ubuntu_Firewall_config
Enabling and configuring a Firewall on Kali Linux

# Configuring a Firewall on Ubuntu or any Linux Distribution

## Project Overview
This project involves implementing and configuring a robust firewall on a Kali Linux virtual machine to enhance system security. The `ufw` (Uncomplicated Firewall) was utilized for firewall management, and network scans were performed using Nmap to verify the effectiveness of the firewall rules.

## Objectives
- **Configure `ufw`** on Kali Linux to manage inbound and outbound traffic.
- **Create and apply firewall rules** to control traffic based on specified criteria.
- **Verify the effectiveness of the firewall rules** using network scanning tools like Nmap.

## System Setup
- **Operating System:** Kali Linux (version 2024.1)
- **Virtual Machine:** VirtualBox or VMware
- **Firewall Tool:** `ufw` (Uncomplicated Firewall)
- **Network Scanning Tool:** Nmap

## Steps Taken
### 1. Update Your System
Ensure that the machine is updated and the necessary updates are being upgraded.
```bash
sudo apt update
sudo apt upgrade -y
```
### 2. Initial Setup
#### Install `ufw`
To install `ufw` on Kali Linux, use the following command:
```bash
sudo apt-get install ufw
```
#### Enable ufw
The ufw is being disabled by-default, so to apply the rules to the firewall it must be enabled first by using the following command :
```bash
sudo ufw enable
```
Press 'y' and then 'Enter' to complete the action.

### 3. Configuring the Firewall Rules
- #### Allowing ssh connections
To prevent locking yourself out from the system, allow ssh connections
```bash
sudo ufw allow ssh
```
- #### Allowing specific services and ports
Below are some of the services or ports. You can allow any of the services or ports as per your need

##### 1. Allow HTTPS Traffic:
```bash
sudo ufw allow https
```
Or by specifying the port :
```bash
sudo ufw allow 443/tcp
```
##### 2. Allow any other specific port:
```bash
sudo ufw allow 8080/tcp
```

##### 3. Allow specific range of ports :
```bash
sudo ufw allow 2000:3000/tcp
```

##### 4. Allow specific IP address : 
```bash
sudo ufw allow from <any_ip>
```
You can also allow specific Subnet!

- #### Denying specific services and ports

Initially ufw blocks all the incoming traffic by-default except for the ones that are allowed. You can also specifically deny any services, ports or IP addresses.

##### 1. Deny specific port :
```bash
sudo ufw deny 23/tcp
```
**Here port 23 is for Telnet. So to block the Telnet service we have blocked it from gaining unauthorized access. You can allow it if needed.**
##### 2. Deny specific IP address :
```bash
sudo ufw deny from <any_IP>
```
### 4.Viewing ufw Status and Rules
To view the current status of the `ufw` rules you can use the following command:
```bash
sudo ufw status verbose
sudo ufw status numbered
```
### 5.Deleting the `ufw` Rules
#### 1. Using Rule Number :
```bash
sudo ufw delete <rule_number>
```
#### 2. Using Rule Specification:
```bash
sudo ufw delete allow 8080/tcp
```
### 6. Advanced `UFW` Configuration (Optional)
#### 1.Logging :
Enable logging to monitor ufw activity:
```bash
sudo ufw logging on
```
#### 2. Default Policies :
Set default policies to deny all incoming traffic and allow all outgoing traffic
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```
#### 3. Application Profiles:
To list the common application profiles included by ufw use the following command :
```bash
sudo ufw app list
```
Allow a specific application:
```bash
sudo ufw allow 'WWW'
```

### 7.Testing the Firewall 
#### 1. Check Open Ports:
From a different machine (e.g., a Windows machine), use Nmap to verify the firewall rules:
```
# Replace the IP with the actual IP of the firewall machine
nmap -v -A 192.168.1.100
nmap -p 23 192.168.1.100
nmap -p 22 192.168.1.100
nmap -p 80 192.168.1.100
nmap -p 443 192.168.1.100
```
### 8.Document Your Setup
**Document all the ufw rules,policies and configurations that you have added in a seperate file. It can be a normal text file.**

### 9.Conclusion
Through this project, I gained a deeper understanding of configuring and managing firewalls using ufw on my Kali Linux Machine. The experience provided valuable insights into network security practices and the importance of controlling inbound and outbound traffic to protect systems from unauthorized access.
