# Azure-Project

The Azure Honeypot & Sentinel SIEM project is a comprehensive cybersecurity initiative that uses the power of Microsoft Azure to create a simulated environment for attracting, monitoring, and analyzing potential cyber threats. The honeynet in Microsoft Azure aggregated seven log sources into Microsoft Sentinel (SIEM), enabling a comprehensive analysis of security data. The project's primary objective is to create a secure cloud infrastructure, demonstrating adherence to industry security standards and best practices.

Below is the project walk-through:


1. I created a WindowsVM and a LinuxVM in Microsoft Azure
   
2. Then, I created a resource group named 'RG-SOC'. For each VM, I assigned them RG-SOC resource group.
   
3. After the creation of the VMs, I configured the Network security groups and edited the inbound security rules for both WindowsVM and LinuxVM and changed the destination port ranges to all(*). I then turned off the firewall in the WindowsVM.

4. The creation of a private endpoint, 'PE-akv' in Microsoft Azure allows me to connect to my Azure resources securely and privately from my virtual network, 'SOC-VNET', that connects directly to the Azure Key Vault, 'KeyVaultcreated'. This is achieved by using private IP addresses from the virtual network to connect to your resources without being exposed to the public.
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


Above, we created data collection rules for both WindowsVM and LinuxVM, creating Windows Event Logs and Syslog respectively.

