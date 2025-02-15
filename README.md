<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>




# On-Premises Active Directory Deployed in the Cloud (Azure)

## Environments and Technology Used
- **Cloud Provider:** Microsoft Azure
- **Directory Service:** Active Directory Domain Services (AD DS)
- **Networking:** Virtual Network (VNet), VPN Gateway (Optional), Private Endpoints
- **Virtualization:** Azure Virtual Machines (VMs)
- **Storage:** Azure Managed Disks
- **Security:** Network Security Groups (NSGs), Azure Bastion, Multi-Factor Authentication (MFA)

---

## Operating Systems Used
- **Domain Controllers:** Windows Server 2022 Datacenter (or 2019)
- **Client Systems:** Windows 10/11 (for testing domain-joined machines)

---

## High-Level Deployment and Configuration Steps

### 1. **Provision Azure Infrastructure**
   - Create a **Resource Group**.
   - Deploy an **Azure Virtual Network (VNet)** with multiple subnets:
     - **AD Subnet** (for Domain Controllers)
     - **Management Subnet** (for administrative access)
   - Configure **Network Security Groups (NSGs)** to restrict unnecessary traffic.


### 2. **Deploy Virtual Machines for Domain Controllers**
   - Create **two Windows Server 2022 VMs** for redundancy.
   - Assign **static private IPs** to both VMs.
   - Attach and format a dedicated **disk for Active Directory database (NTDS.dit)**.

### 3. **Install and Configure Active Directory Domain Services (AD DS)**
   - Assign a unique hostname to each VM.
   - Configure TCP/IP settings (DNS should point to itself initially).
   - Install the **Active Directory Domain Services (AD DS)** role.
   - Promote the first server as a **Domain Controller** and create a new **Forest**.
   - Add the second Domain Controller for **redundancy and fault tolerance**.

### 4. **DNS and DHCP Configuration**
   - Configure **Forward Lookup Zones** for internal name resolution.
   - Set up **conditional forwarders** if integrating with external services.
   - (Optional) Install and configure **DHCP Server** if needed.

### 5. **Enable Remote and Secure Access**
   - Deploy **Azure Bastion** or set up a Jumpbox for secure remote access.
   - Configure **VPN Gateway** or **Azure ExpressRoute** if integrating with an on-premises network.
   - Implement **Azure AD Connect** if hybrid identity management is needed.

### 6. **Create and Manage Active Directory Objects**
   - Create **Organizational Units (OUs)** for logical structuring.
   - Add **User Accounts, Groups, and Group Policies (GPOs)**.
   - Implement **Role-Based Access Control (RBAC)** and security policies.

### 7. **Backup and Disaster Recovery**
   - Enable **Azure Backup** for domain controllers.
   - Configure **System State Backups** to recover AD if needed.

### 8. **Monitoring and Maintenance**
   - Enable **Azure Monitor** and set up alerts for Active Directory health.
   - Regularly review **Event Logs** for security and operational issues.
   - Perform periodic **Active Directory health checks** (`dcdiag`, `repadmin`).

---

## Additional Considerations
- **High Availability:** Deploy domain controllers in different **Availability Zones**.
- **Hybrid Identity:** Implement **Azure AD Connect** to sync with Azure AD.
- **Security Hardening:** Implement **Privileged Access Workstations (PAWs)** and **Conditional Access Policies**.
- **Logging and Auditing:** Enable **Azure Sentinel** or SIEM integration for security monitoring.

---

## Conclusion
This guide outlines the deployment of an **On-Premises Active Directory** environment in Azure, providing scalability, security, and hybrid integration options. By leveraging Azure infrastructure, organizations can extend their traditional AD setup into the cloud while maintaining control over identity and access management.

---

### 📌 **References**
- [Microsoft Docs: Deploy AD DS in Azure](https://learn.microsoft.com/en-us/azure/active-directory-domain-services/)
- [Azure AD vs. On-Prem AD Comparison](https://learn.microsoft.com/en-us/azure/active-directory/)
