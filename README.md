Project URL: https://roadmap.sh/projects/ssh-remote-server-setup

# AWS EC2 SSH Connection Guide

This repository provides a step-by-step technical reference for configuring AWS network security and establishing a secure SSH connection to an Amazon Elastic Compute Cloud (EC2) instance.

## Prerequisites

Before connecting, ensure your EC2 instance meets the following networking and access control requirements.

### 1. Network Configuration

* Public IPv4 Address: The instance must have an Elastic IP or an auto-assigned public IPv4 address enabled.
* Network Access Control List (NACL): Ensure the subnet's stateless NACL allows the necessary traffic:
  * Inbound: Allow port 22 (SSH) from your source IP.
  * Outbound: Allow ephemeral ports (1024-65535) or all traffic to permit return packets.

### 2. Firewall Rules (Security Group)

Attach a Security Group to your EC2 instance with the following stateful rules:

* Inbound: Port 22
* Outbound: All traffic

<img width="1625" height="233" alt="Screenshot From 2026-09-29 01-12-52" src="https://github.com/user-attachments/assets/1b515935-abc8-4059-8a66-4fc2a847c633" />

<img width="1625" height="233" alt="Screenshot From 2026-09-29 01-14-42" src="https://github.com/user-attachments/assets/b50d4e78-2a99-4286-a52a-84817f198325" />

## Connection Steps

When you launch the EC2 instance, AWS prompts you to generate or select an asymmetric key pair. Download the private key (e.g., mykey.pem) and keep it secure.

### 1. Restrict Private Key Permissions

SSH requires strict permissions on private key files. If the file permissions are too open, the SSH client will reject the key.
Open your local terminal and run:

```bash
$chmod 400 mykey.pem
```

### 2. Execute the SSH Command

Connect to your instance using the private key, default OS username, and the public IPv4 address:

```bash
$ssh -i "mykey.pem" username@<PUBLIC_IPv4_ADDRESS>
```

NB: The username depends entirely on the Operating System (OS) image or Amazon Machine Image (AMI) you chose:

* Amazon Linux: ec2-user
* Ubuntu: ubuntu
* CentOS: centos
* Debian: admin
