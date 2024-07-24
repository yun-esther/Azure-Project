# Azure-Project

The Azure Honeypot & Sentinel SIEM project is a comprehensive cybersecurity initiative that uses the power of Microsoft Azure to create a simulated environment for attracting, monitoring, and analyzing potential cyber threats. The honeynet in Microsoft Azure aggregated seven log sources into Microsoft Sentinel (SIEM), enabling a comprehensive analysis of security data. The project's primary objective is to create a secure cloud infrastructure, demonstrating adherence to industry security standards and best practices.

Below is the project walk-through:


1. I created a WindowsVM and a LinuxVM in Microsoft Azure
   
2. Then, I created a resource group named 'RG-SOC'. For each VM, I assigned them RG-SOC resource group.
   
3. After the creation of the VMs, I configured the Network security groups and edited the inbound security rules for both WindowsVM and LinuxVM and changed the destination port ranges to all(*). I then turned off the firewall in the WindowsVM.

5. Next, I went into Microsoft Sentinel 
