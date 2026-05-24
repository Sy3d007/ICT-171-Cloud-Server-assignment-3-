# ICT-171 Cloud Server (assignment 3)

Name: Syed Shah
ID number: 35932261
Email: 35932261@student.murdoch.edu.au 
Unit: ICT171 Introduction to Server Environments and Architectures



Project overview: This repository documents the setup of a cloud based anime review website hosted on Microsoft Azure. The server runs WordPress on a manually configured LAMP stack, featuring anime reviews, ratings, and recommendations organised by genre.

# VM Setup

## Azure Virtual Machine

- **VM Name:** ict171-vm
- **Region:** Australia East
- **Size:** Standard B2ats v2 (2 vCPUs, 1 GiB RAM)
- **OS:** Ubuntu Server 24.04 LTS
- **Public IP:** 20.213.8.117

## SSH Access

Connect to the server from a Mac terminal:

```bash
ssh -i ~/Desktop/ict171-vm_key.pem azureuser@20.213.8.117
```

## Web Server Installation

Install Apache:

```bash
sudo apt install apache2 -y
```

Verify Apache is running:

```bash
sudo systemctl status apache2
```

Apache can be confirmed by visiting http://20.213.8.117 in a browser — the default Ubuntu Apache page should appear.


