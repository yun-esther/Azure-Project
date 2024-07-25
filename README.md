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

5. The creation of Data Collection Rules (DCRs) in Microsoft Azure are a feature of Azure Monitor that allows one to define how data is collected from various sources, such as virtual machines, applications, and services, and sent to Azure Monitor for analysis and visualization. Its purpose is to centralize data collection.
<img width="1250" alt="log analytics workspace (LAWS) windows event logs" src="https://github.com/user-attachments/assets/2d7153db-6038-493d-8ea8-d1df5e49f303">
<img width="1255" alt="law attack vm event logs" src="https://github.com/user-attachments/assets/a8792daa-1e66-47dd-abe4-d683a3a4a112">
<img width="1244" alt="data collection rules" src="https://github.com/user-attachments/assets/acb69c78-ca81-46ec-a524-ef747da85b4b">

Collecting and storing log data in Log Analytics allows us to use Sentinel to monitor, track, and manage your Azure environment.


<img width="821" alt="dcr data source windows" src="https://github.com/user-attachments/assets/d2167e29-c729-46f9-b153-07092f263c4d">
<img width="875" alt="dcr data source attackvm" src="https://github.com/user-attachments/assets/e1e1528a-b29f-4276-9c85-09bda42485bb">


Above, we created data collection rules for both WindowsVM and LinuxVM, creating Windows Event Logs and Syslog respectively. These two popular logging mechanisms are used to collect and store log data from various sources.

-Windows Event Logs are divided into three main categories: (1) Application Logs (2) System Logs (3) Security Logs
-Syslogs are formatted in a specific way and provides the following information: (1) Facility (2) Severity (3) Timestamp (4) Message


6. The Azure Blob Storage allows you to store Windows Event Logs and Syslog data.
<img width="1269" alt="grapejuices config" src="https://github.com/user-attachments/assets/f670539d-28ef-4cad-8951-a708cb5bc4c9">
<img width="1262" alt="grapejuices 2" src="https://github.com/user-attachments/assets/2e107237-f0e2-4dc1-8d8c-f1d16d17425d">


7. Next, I set up a Watchlist in Microsoft Sentinel. A Watchlist is a list of entities, such as IP addresses, domains, or users, that are of interest to security analysts and threat hunters. Watchlists are used to identify and track potential security threats, and to alert on suspicious activity related to these entities. Watchlists provide real time monitoring, alerting and notification, and analytics and visualization. This improves threat detection, enhances incident response, and streamlines threat hunting. The 'geoip' watchlist will track and monitor IP addressses based on their geographical locations.
<img width="1242" alt="watchlist" src="https://github.com/user-attachments/assets/90be0f01-68d9-4413-a0c8-f1c7efbd2218">


8. Microsoft Sentinel Fusion rules are a type of analytics rule that uses a correlation engine based on scalable machine learning algorithms to automatically detect multistage attacks, also known as advanced persistent threats (APTs). These rules identify combinations of anomalous behaviors and suspicious activities that are observed at various stages of the kill chain, and generate incidents that would otherwise be difficult to catch. They correlate multiple signals from various products, such as Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection, and others, to identify potential threats. 
![Sentinel Fusion rule](https://github.com/user-attachments/assets/4f10b9b5-2823-43fa-888c-75cce5297c20)


   
9. Network Watcher is a network monitoring and diagnostic service in Microsoft Azure that provides visibility into Azure network resources and traffic. The Network Watcher topology is a graphical representation of the network infrastructure and resources in Azure, which helps network administrators and security professionals to understand the network architecture, identify potential security risks, and troubleshoot network issues. Currently, our virtual network resources are deployed in East US.
![region](https://github.com/user-attachments/assets/613fad98-95dd-4a0d-bd41-8ca8028141a9)


![SOC subnet](https://github.com/user-attachments/assets/34e409fb-9605-436f-bb94-61241f92641d)
A virtual network (VNet) is a network or environment that can be used to run Virtual Machines and applications in the cloud. When a VNet is created, the services and VMs within the Azure network interact securely with each other. It allows you to create a private space in the Azure cloud. Components of a VNet comprises of subnets, routing, and network security groups. 


![perimeter external firewall](https://github.com/user-attachments/assets/75a863e7-9818-4a2f-92c7-eaf0ff8a27e6)
The Azure Firewall is a fully managed, scalable, and highly available service that provides a perimeter defense for Azure resources. It is a cloud-native firewall that is easily integrated with Azure Virtual Networks (VNets) to control and filter incoming and outgoing traffic. The Azure Firewall filters traffic, inspects traffic, applies rule-based filtering, and provides threat protection.


![external firewall protecting SOC:defense in depth](https://github.com/user-attachments/assets/ed26e8dc-7021-4c7f-ae30-6c34ae7a12e6)
This diagram shows us interconnected Azure regions with various Virtual Machines and subnets. This hub-and-spoke network architecture allows different network segments to communicate with each other securely.


![Private endpoint storage](https://github.com/user-attachments/assets/9950befb-7abe-4f67-b98c-ce3fae33f9de)

The Private Endpoint for Azure storage is a network interface that privately and securely connects to an Azure storage service. I assigned a private IP address to the private endpoint, which is used to access the grapejuices Azure storage service. 



10. Azure SIEM (Security Information and Event Management), also known as Microsoft Sentinel is a cloud-native SIEM solution that provides advanced threat detection, incident response, and security analytics capabilities. It helps organizations detect, respond to, and prevent security threats in real-time. Key features include: Real-Time threat detection, Incident response, Security analytics, Integration with Azure services, and Multi-Cloud and Hybrid support. 
    
![sentinel analytics- Alerts (SIEM)](https://github.com/user-attachments/assets/4b893023-2f71-4a5d-9bd2-4a13d7e79a4d)



11. Workbooks in Microsoft Azure are a powerful tool for visualizing and monitoring data. They allow users to create custom dashboards that provide insights into their data, enabling them to identify trends, patterns, and anomalies. Its primary purpose is to visualize, monitor, and analyze data. Below are dashboards that show different types of security threats and their originations.
    Geo Locations provide geographical context to the data, allowing us to visualize where threats are coming from. This enhances the security strategy, allowing for quicker response to threats, and a more proactive approach. The combination of workbooks and geo locations in a honeynet is a very powerful tool for threat intelligence and incident response. 

![Screen Shot 2024-04-15 at 8 40 50 PM](https://github.com/user-attachments/assets/dea8b363-b041-4b89-901d-a43496c474cf)
This Linux SSH Threats Workbook shows security threats that are related to Linux Secureshell activities, showing failed SSH authentication attempts from across the world. We can see that a lot of the authentication attempts came from Australia.


![Screen Shot 2024-04-15 at 8 40 13 PM](https://github.com/user-attachments/assets/582663bc-0d3d-4ed9-babc-f38a35821648)
This Microsoft SQL Threats Workbook shows security threats that are related to Microsoft SQL Server activities, showing failed authentication attempts from across the world. This dashboard shows brute-force attacks targeting Microsoft SQL Server installations from all over the globe, with most of the attacks originating from the U.S East Coast and Spain.


![Screen Shot 2024-04-15 at 8 39 56 PM](https://github.com/user-attachments/assets/6bee495d-9594-4078-b7f2-e5521155ed44)
This Windows Remote Desktop Protocol (RDP) Threats Workbook shows security threats that are related to failed Windows RDP authentication attempts from across the globe. We can see that most of the brute-force attempts originated from Spain and Canada.


![Screen Shot 2024-04-15 at 8 40 27 PM](https://github.com/user-attachments/assets/f24dfbb6-8522-4abd-864d-1c88fd801eb0)
This Network Security Group (NSG) Threats Workbook shows security events where malicious traffic or networks were allowed into our networks and systems. The dashboard shows where the malicious activities originated from across the globe, allowing us to identify sources and patterns, and this in turn helps prioritize remediation efforts.
