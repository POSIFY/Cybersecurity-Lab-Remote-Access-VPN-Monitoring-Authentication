# Cybersecurity-Lab-Remote-Access-VPN-Monitoring-Authentication

**Project Overview**
This project demonstrates the deployment of an integrated cybersecurity lab that combines firewall management, VPN configuration, centralized logging, and secure authentication. Using pfSense as the primary firewall, a WireGuard VPN for secure remote access, an ELK Stack for real-time log monitoring and visualization, and Authelia for authentication and access control, this lab showcases end-to-end network security practices. The project highlights skills in network architecture, secure remote access, containerized deployments, monitoring, and identity management.

## 1. pfSense Setup
**Network Topology Overview**
Before installation, define your network layout:
* WAN (Internet): External network interface
* LAN (Internal): Trusted local network
* VPN Interface (Optional): For remote VPN connections
* Management Access: Via WebGUI on LAN or management VLAN

**Installation Guide**
**Step-by-step instructions for installing pfSense in VirtualBox.**
**Required Resources:**
* VirtualBox
* pfSense ISO Installer (AMD64, ISO, nearest mirror)

**Create Virtual Machine in VirtualBox**
* Launch VirtualBox → New VM.

   <img width="488" height="405" alt="image" src="https://github.com/user-attachments/assets/1e982497-3dc7-490d-92ea-eed308b0c002" />
   
* Configure:
    1. Name: pfSense (or preferred)
    2. Type: Linux
    3. Version: Debian (64-bit)
    4. Memory Allocation:
    5. Recommended: 1024 MB (1 GB), Increase if anticipating higher traffic
  
  <img width="498" height="407" alt="image" src="https://github.com/user-attachments/assets/a133f867-4a49-49cb-8a3f-0831d82c16d0" />

* Create Virtual Hard Disk:
    1. File Type: VDI (VirtualBox Disk Image)
    2. Storage: Dynamically Allocated
    3. Size: 15 GB (8 GB minimum)
* Configure VM Settings
  System Settings:
    1. Boot Order: Hard Disk > Optical Drive, uncheck Floppy
    2. Network Settings: Adapter 1: NAT → WAN, Adapter 2: Internal Network → LAN (name: LAN1)
       
  <img width="563" height="460" alt="image" src="https://github.com/user-attachments/assets/936af918-df37-4e45-ae69-3bbe35718908" />

* Storage Settings:
    1. Mount the pfSense ISO in Storage → Optical Drive
  
  <img width="639" height="498" alt="image" src="https://github.com/user-attachments/assets/37fa20b5-d5aa-48d1-bacd-e5a63a6bcd7f" />


## Install pfSense
Start VM

<img width="861" height="487" alt="image" src="https://github.com/user-attachments/assets/41651860-fe44-4614-925d-f40a9801042d" />

* Accept default installation options
  
<img width="863" height="482" alt="image" src="https://github.com/user-attachments/assets/85775d45-a1ee-43c5-bd0e-caae6d3dcd46" />

* Use Auto (UFS) as file system
* Avoid ZFS unless supported
* Complete installation and reboot

**Configure Interfaces**

<img width="732" height="416" alt="image" src="https://github.com/user-attachments/assets/9feaf110-8436-4f5d-91de-fe046ddf3564" />

* Detect WAN and LAN interfaces automatically
* Configure LAN IP: 192.168.x.x/24
* Enable DHCP: 192.168.x.x – 192.168.x.x
* Enable web configurator
* Verify Internal Network:

**Create a client VM (e.g., Kali Linux) on LAN1**
<img width="941" height="470" alt="image" src="https://github.com/user-attachments/assets/5b065194-c9df-478c-96c9-a8eafc5e7f6d" />

* Ensure it receives an IP from pfSense DHCP
* Access pfSense WebGUI: http://192.168.X.X


