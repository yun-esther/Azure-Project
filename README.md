# Azure-Project

The Azure Honeypot & Sentinel SIEM project is a comprehensive cybersecurity initiative that uses the power of Microsoft Azure to create a simulated environment for attracting, monitoring, and analyzing potential cyber threats. The honeynet in Microsoft Azure aggregated seven log sources into Microsoft Sentinel (SIEM), enabling a comprehensive analysis of security data. The project's primary objective is to create a secure cloud infrastructure, demonstrating adherence to industry security standards and best practices.

Below is the project walk-through:


1. I created a WindowsVM and a LinuxVM in Microsoft Azure
   
2. Then, I created a resource group named 'RG-SOC'. For each VM, I assigned them RG-SOC resource group.
   
3. After the creation of the VMs, I configured the Network security groups and edited the inbound security rules for both WindowsVM and LinuxVM and changed the destination port ranges to all(*). I then turned off the firewall in the WindowsVM.

4. The creation of a private endpoint, 'PE-akv' in Microsoft Azure allows me to connect to my Azure resources securely and privately from my virtual network, 'SOC-VNET', that connects directly to the Azure Key Vault, 'KeyVaultcreated'. This is achieved by using private IP addresses from the virtual network to connect to your resources without being exposed to the public.
![Keyvault created](https://github.com/user-attachments/assets/d37290d7-abcd-42bf-a420-cb3ba425ee41)
<img width="1260" alt="creation of private endpoint" src="https://github.com/user-attachments/assets/4cab9822-38ea-4aff-96cd-a6b58d80c54c">
<img width="981" alt="creation of private endpoint 2" src="https://github.com/user-attachments/assets/ad247d95-1a36-417e-89fa-75702b4d5f9e">

![Private endpoint key vault](https://github.com/user-attachments/assets/b03c4628-edfb-48e0-aaea-1e194780064f)

6. The creation of Data Collection Rules (DCRs) in Microsoft Azure are a feature of Azure Monitor that allows one to define how data is collected from various sources, such as virtual machines, applications, and services, and sent to Azure Monitor for analysis and visualization. Its purpose is to centralize data collection.
<img width="1250" alt="log analytics workspace (LAWS) windows event logs" src="https://github.com/user-attachments/assets/2d7153db-6038-493d-8ea8-d1df5e49f303">
<img width="1255" alt="law attack vm event logs" src="https://github.com/user-attachments/assets/a8792daa-1e66-47dd-abe4-d683a3a4a112">
<img width="1244" alt="data collection rules" src="https://github.com/user-attachments/assets/acb69c78-ca81-46ec-a524-ef747da85b4b">

Collecting and storing log data in Log Analytics allows us to use Sentinel to monitor, track, and manage your Azure environment.


<img width="821" alt="dcr data source windows" src="https://github.com/user-attachments/assets/d2167e29-c729-46f9-b153-07092f263c4d">
<img width="875" alt="dcr data source attackvm" src="https://github.com/user-attachments/assets/e1e1528a-b29f-4276-9c85-09bda42485bb">


Above, we created data collection rules for both WindowsVM and LinuxVM, creating Windows Event Logs and Syslog respectively. These two popular logging mechanisms are used to collect and store log data from various sources.

-Windows Event Logs are divided into three main categories: (1) Application Logs (2) System Logs (3) Security Logs
-Syslogs are formatted in a specific way and provides the following information: (1) Facility (2) Severity (3) Timestamp (4) Message


7. The Azure Blob Storage allows you to store Windows Event Logs and Syslog data.
<img width="1269" alt="grapejuices config" src="https://github.com/user-attachments/assets/f670539d-28ef-4cad-8951-a708cb5bc4c9">
<img width="1262" alt="grapejuices 2" src="https://github.com/user-attachments/assets/2e107237-f0e2-4dc1-8d8c-f1d16d17425d">


8. Next, I set up a Watchlist in Microsoft Sentinel. A Watchlist is a list of entities, such as IP addresses, domains, or users, that are of interest to security analysts and threat hunters. Watchlists are used to identify and track potential security threats, and to alert on suspicious activity related to these entities. Watchlists provide real time monitoring, alerting and notification, and analytics and visualization. This improves threat detection, enhances incident response, and streamlines threat hunting. The 'geoip' watchlist will track and monitor IP addressses based on their geographical locations.
<img width="1242" alt="watchlist" src="https://github.com/user-attachments/assets/90be0f01-68d9-4413-a0c8-f1c7efbd2218">


9. Network Watcher is a network monitoring and diagnostic service in Microsoft Azure that provides visibility into Azure network resources and traffic. The Network Watcher topology is a graphical representation of the network infrastructure and resources in Azure, which helps network administrators and security professionals to understand the network architecture, identify potential security risks, and troubleshoot network issues. Currently, our virtual network resources are deployed in East US.
![region](https://github.com/user-attachments/assets/613fad98-95dd-4a0d-bd41-8ca8028141a9)


![SOC subnet](https://github.com/user-attachments/assets/34e409fb-9605-436f-bb94-61241f92641d)
A virtual network (VNet) is a network or environment that can be used to run Virtual Machines and applications in the cloud. When a VNet is created, the services and VMs within the Azure network interact securely with each other. It allows you to create a private space in the Azure cloud. Components of a VNet comprises of subnets, routing, and network security groups. 


![perimeter external firewall](https://github.com/user-attachments/assets/75a863e7-9818-4a2f-92c7-eaf0ff8a27e6)
The Azure Firewall is a fully managed, scalable, and highly available service that provides a perimeter defense for Azure resources. It is a cloud-native firewall that is easily integrated with Azure Virtual Networks (VNets) to control and filter incoming and outgoing traffic. The Azure Firewall filters traffic, inspects traffic, applies rule-based filtering, and provides threat protection.


![external firewall protecting SOC:defense in depth](https://github.com/user-attachments/assets/ed26e8dc-7021-4c7f-ae30-6c34ae7a12e6)
This diagram shows us interconnected Azure regions with various Virtual Machines and subnets. This hub-and-spoke network architecture allows different network segments to communicate with each other securely.


![Private endpoint storage](https://github.com/user-attachments/assets/9950befb-7abe-4f67-b98c-ce3fae33f9de)
The Private Endpoint for Azure storage is a network interface that privately and securely connects to an Azure storage service. I assigned a private IP address to the private endpoint, which is used to access the Azure storage service. 

