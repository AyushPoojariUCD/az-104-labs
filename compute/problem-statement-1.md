```md
## MedCare Company

**MedCare Healthcare Group**

---

## Background

MedCare Healthcare Group is migrating its legacy hospital administration application from on-premises infrastructure to Microsoft Azure. The application supports patient admissions and must remain accessible to hospital administrators 24×7.

As an Azure Administrator, you have been tasked with deploying the initial production virtual machine that will host the application and its supporting services.

The solution must follow organizational security and operational standards while ensuring the Operations Team can remotely administer the server.

---

## Requirements

### Resource Group

Create a Resource Group with the following configuration:

| Setting | Value |
|----------|---------|
| Resource Group Name | `RG-MedCare-Prod` |
| Region | `East US 2` |

---

### Virtual Machine

Deploy a production virtual machine using the following specifications:

| Setting | Value |
|----------|---------|
| VM Name | `MC-HOSP-APP01` |
| Image | `Windows Server 2022 Datacenter: Azure Edition` |
| Size | `Standard_D4s_v5` |
| Region | `East US 2` |
| OS Disk Type | `Premium SSD` |

---

### Networking

Configure networking according to the following requirements:

| Setting | Value |
|----------|---------|
| Virtual Network | Create a dedicated VNet |
| Subnet | Create a dedicated subnet |
| Public IP | Standard SKU |
| Network Security | Restrict inbound access to RDP only |

---

### Security

Implement the following security controls:

- Allow inbound **RDP (TCP 3389)** traffic only.
- Use a **Standard SKU Public IP Address**.
- Ensure the virtual machine follows production security standards.

---

### Monitoring and Diagnostics

Configure diagnostics using the following settings:

| Setting | Requirement |
|-----------|--------------|
| Boot Diagnostics | Enabled |
| Diagnostic Screenshots | Available for troubleshooting |

---

### Resource Tagging

Apply the following tags to all deployed resources:

| Tag Name | Value |
|-----------|---------|
| Environment | `Production` |
| Department | `Healthcare` |
| Application | `Admissions` |

---

## Success Criteria

The lab is considered successful when all the following conditions are met:

- [ ] Resource Group `RG-MedCare-Prod` exists.
- [ ] Virtual Machine `MC-HOSP-APP01` is deployed successfully.
- [ ] The virtual machine status is **Running**.
- [ ] The Operations Team can establish an RDP connection.
- [ ] Boot Diagnostics screenshots are accessible.
- [ ] The OS disk uses **Premium SSD** storage.
- [ ] A **Standard SKU Public IP** is assigned.
- [ ] The Network Security Group allows only RDP access.
- [ ] All required tags are applied correctly.

---

## Skills Covered

This lab aligns with the following AZ-104 objectives:

- Create and configure virtual machines.
- Configure Network Security Groups (NSGs).
- Configure Public IP addresses.
- Configure Boot Diagnostics.
- Manage Azure Managed Disks.
- Apply resource tags.
- Validate production VM deployments.

---

## Deliverables

At the completion of this lab, provide the following evidence:

1. Screenshot of the deployed virtual machine overview page.
2. Screenshot showing successful RDP connectivity.
3. Screenshot of Boot Diagnostics.
4. Screenshot of the Network Security Group inbound rules.
5. Screenshot showing the Premium SSD OS disk configuration.
6. Screenshot verifying resource tags.

---

## Estimated Duration

**20–30 Minutes**

---

## Estimated Cost

Approximately **USD $0.40–$0.80 per hour**, depending on VM runtime.

> **Note:** Stop (deallocate) the virtual machine after completing the lab to minimize Azure charges.

---

## Challenge Tasks (Optional)

1. Resize the virtual machine to `Standard_D8s_v5`.
2. Attach a `128 GB Premium SSD` data disk.
3. Enable Just-In-Time VM Access using Microsoft Defender for Cloud.
4. Move the virtual machine to a new resource group within the same subscription.
5. Document the impact of each change.

---

## Learning Outcome

Upon completion of this lab, you will be able to deploy and secure a production-ready Azure virtual machine following enterprise requirements and best practices commonly encountered by Azure Administrators.
```
