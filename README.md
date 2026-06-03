# Honeypot Test Environment Commands

Commands used for implementing, configuring, running, and monitoring traditional Cowrie and LLM-based honeypots.

This repository supports the dissertation project:

**A Comparative Analysis of Traditional and LLM-Based Honeypots for Cyber Threat Deception**

The project compared a traditional Cowrie SSH honeypot with an LLM-based SSH honeypot inside a controlled VMware lab environment. The purpose was to evaluate differences in realism, interaction depth, dead-end behaviour, misleading command handling, and CPU/memory usage.

## Lab Environment Setup

The experiment was carried out inside a controlled VMware lab environment. VMware was used to host the virtual machines and separate the test environment into different virtual network segments.

The lab environment included four main virtual machines:

- pfSense firewall/router
<img width="1917" height="1031" alt="image" src="https://github.com/user-attachments/assets/9233b82d-d7f6-483e-8b1a-56e4f7406255" />

- Kali Linux attacker VM
<img width="1910" height="977" alt="image" src="https://github.com/user-attachments/assets/05e6ca21-b066-4bac-b08b-02495b5c328d" />

- Cowrie traditional honeypot VM
<img width="1378" height="1011" alt="image" src="https://github.com/user-attachments/assets/6532842f-000b-46db-a297-ae2273ba8a78" />

- LLM-based honeypot VM
<img width="1514" height="1010" alt="image" src="https://github.com/user-attachments/assets/b5f1e72c-f8a1-4db6-8595-0f06f159bf2d" />

The pfSense firewall acted as the central router between the attacker network and the DMZ network. The Kali Linux VM was used as the attacker machine, while both honeypots were placed inside the DMZ network.

## pfSense Interface Overview

Add pfSense dashboard screenshot here.

## Network Segments

| VMnet | Purpose | Subnet |
|---|---|---|
| VMnet2 | Management Network | 10.10.50.0/24 |
| VMnet3 | Attacker Network | 10.10.60.0/24 |
| VMnet4 | DMZ Network | 10.10.70.0/24 |
| VMnet8 | NAT / Outside Access | 192.168.80.0/24 |

## Main IP Addressing

| Device / VM | Purpose | IP Address |
|---|---|---|
| pfSense MGMT interface | Management gateway | 10.10.50.1 |
| pfSense ATTACKER interface | Gateway for attacker network | 10.10.60.1 |
| pfSense DMZ interface | Gateway for DMZ network | 10.10.70.1 |
| Kali Linux VM | Attacker machine | 10.10.60.10 |
| Cowrie Honeypot VM | Traditional SSH honeypot | 10.10.70.10 |
| LLM-Based Honeypot VM | LLM-based SSH honeypot | 10.10.70.20 |

## Honeypot Access

Both honeypots were accessed from the Kali Linux attacker VM through the pfSense firewall. SSH port `2222` was used for the honeypot interaction sessions.

| Honeypot | IP Address | SSH Port |
|---|---|---|
| Cowrie Honeypot | 10.10.70.10 | 2222 |
| LLM-Based Honeypot | 10.10.70.20 | 2222 |
