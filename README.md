# ICT-171 Cloud Server (assignment 3)

Name: Syed Shah
ID number: 35932261
Email: 35932261@student.murdoch.edu.au 
Unit: ICT171 Introduction to Server Environments and Architectures



Project overview: This repository documents the setup for a cloud based web server on microsoft azure, The server will run 

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
ssh -i ~/path/to/ict171-vm_key.pem azureuser@20.213.8.117
```
