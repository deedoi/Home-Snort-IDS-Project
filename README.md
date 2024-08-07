# Home Snort IDS Project

## Overview
This project provides a step-by-step guide for setting up and configuring Snort, an open-source Intrusion Detection System (IDS), on Ubuntu Server. It's designed for home users and cybersecurity enthusiasts who want to learn about network security and IDS implementation.

## Introduction
Snort is a powerful tool for detecting and preventing network intrusions. This guide walks you through the process of setting it up on an Ubuntu Server, configuring it for your home network, and creating custom rules to detect specific types of traffic.

## Prerequisites
- Ubuntu Server (24.04 LTS used in this guide)
- Basic knowledge of Linux command line
- Understanding of basic networking concepts

## Installation
Detailed steps for installing Snort on Ubuntu Server, including:
- Updating the system

```
sudo apt-get update
sudo apt-get upgrade
```

- Installing Snort via apt
```
sudo apt-get install snort
```
- Verifying the installation
```
snort -V
```

## Configuration
Guide on configuring Snort for your home network:
- Editing the snort.conf file
```
sudo vim /etc/snort/snort.conf
```
- Setting up your home network range in configuration file. 
```
ipvar HOME_NET [10.0.0.0/24,192.168.0.0/24]
```
Adjust the IP ranges according to your network setup.

- Verify the configuration
```
sudo snort -T -i enp0s3 -c /etc/snort/snort.conf
```
Replace `enp0s3` with your network interface if different.

## Custom Rules
Create custom rules in `/etc/snort/rules/local.rules`. Examples:

1. ICMP Ping Detection:
```
alert icmp any any -> $HOME_NET any (msg:"ICMP Ping Detected"; sid:100001; rev:1;)
```
2. SSH Authentication Attempt:
```
alert tcp any any -> $HOME_NET 22 (msg:"SSH AUTHENTICATION ATTEMPT"; sid:100002; rev:1;)
```

## Running Snort
Run Snort with the following command:
```
sudo snort -q -l /var/log/snort -i enp0s3 -A console -c /etc/snort/snort.conf
```

Options explained:
- `-q`: Quiet mode
- `-l /var/log/snort`: Log directory
- `-i enp0s3`: Network interface
- `-A console`: Alert output to console
- `-c /etc/snort/snort.conf`: Configuration file

## Troubleshooting
- If you encounter permission issues, ensure proper file permissions and ownership.
- For configuration errors, double-check your snort.conf and local.rules files.
- Verify that you're using the correct network interface in your Snort commands.

![IP config on Snort](https://github.com/user-attachments/assets/bf93f296-7561-439a-a05f-3bf1e6e54048)
![Promisc On Bridge mode adapter](https://github.com/user-attachments/assets/76ea599b-85ab-470a-9ba4-1cb8b629a4d1)
![check Snort config file](https://github.com/user-attachments/assets/3cc05751-71a1-46af-8826-e2eb1bd36595)
![Custom rules](https://github.com/user-attachments/assets/bd7b7a9b-e4ba-4aa3-9b35-1b8a5d330de2)
![Ping detection rule](https://github.com/user-attachments/assets/8916dd52-1501-4a25-96f7-c8cccccbc909)
![Snort in Ubuntu shows ping log](https://github.com/user-attachments/assets/0c45c9c6-89d4-4676-9269-2243be4e02bf)





  
