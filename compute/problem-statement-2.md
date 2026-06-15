# Lab 2: Host Encryption Compliance

## Company

**SecureBank Financial Services**

---

## Background

SecureBank Financial Services operates a high-frequency trading platform that processes millions of financial transactions daily.

During a recent security audit, the compliance team discovered that sensitive customer information could potentially be exposed through virtual machine storage components used by production workloads.

The Chief Information Security Officer (CISO) has mandated that all storage associated with production virtual machines must be protected using Azure-native security capabilities while minimizing operational complexity.

As an Azure Administrator, you have been tasked with implementing the required security controls across the bank's production virtual machines.

---

## Requirements

### Existing Environment

The current production environment contains several virtual machines hosting trading applications.

The virtual machines use:

- Operating System Disks
- Data Disks
- Temporary Disks

---

### Security Requirements

Implement a security solution that satisfies the following requirements:

- Protect all production virtual machines.
- Protect Operating System Disks.
- Protect attached Data Disks.
- Protect Temporary Disks.
- Use Azure-native capabilities.
- Use Microsoft-managed encryption.
- Avoid installing or configuring encryption software inside guest operating systems.
- Minimize administrative overhead.
- Ensure the configuration complies with banking security standards.

---

### Operational Requirements

The implementation must:

- Avoid application redesign.
- Minimize disruption to trading services.
- Be repeatable for future production virtual machines.
- Be validated before the security audit closes.

---

## Success Criteria

The lab is considered successful when all of the following conditions are met:

- [ ] Encryption at Host is enabled on all designated production virtual machines.
- [ ] Operating System Disks are protected.
- [ ] Data Disks are protected.
- [ ] Temporary Disks are protected.
- [ ] Microsoft-managed encryption is used.
- [ ] No guest operating system encryption configuration changes are required.
- [ ] Security audit requirements are satisfied.
- [ ] Evidence is available to demonstrate compliance.

---

## Skills Covered

This lab aligns with the following AZ-104 objectives:

- Configure encryption at host for Azure virtual machines.
- Understand the differences between Encryption at Host and Azure Disk Encryption.
- Review virtual machine security configurations.
- Validate encryption settings.
- Implement Azure-native security controls.

---

## Deliverables

At the completion of this lab, provide the following evidence:

1. Screenshot showing the selected production virtual machine.
2. Screenshot confirming **Encryption at Host** is enabled.
3. Documentation identifying which storage components are protected.
4. Summary explaining why the selected approach satisfies compliance requirements.
5. Comparison table describing the differences between:
   - Encryption at Host
   - Azure Disk Encryption (ADE)

---

## Comparison Exercise

Complete the following table during the lab:

| Feature | Encryption at Host | Azure Disk Encryption |
|-----------|-------------------|------------------------|
| Protects OS Disks | | |
| Protects Data Disks | | |
| Protects Temporary Disks | | |
| Requires Guest OS Configuration | | |
| Uses BitLocker/DM-Crypt | | |
| Azure-Native Implementation | | |

---

## Estimated Duration

**15–20 Minutes**

---

## Estimated Cost

**Minimal**

> This lab primarily involves modifying virtual machine configuration settings. Additional costs may be negligible depending on the existing environment.

---

## Challenge Tasks (Optional)

1. Identify virtual machines within the subscription that do not comply with the encryption standard.
2. Document a remediation plan for non-compliant virtual machines.
3. Research scenarios where Azure Disk Encryption may still be preferred.
4. Evaluate how Customer-Managed Keys (CMKs) could be incorporated into the organization's encryption strategy.
5. Propose a governance approach to ensure future production VMs comply automatically.

---

## Learning Outcome

Upon completion of this lab, you will be able to implement Azure-native host encryption for production virtual machines and understand how it differs from other Azure encryption technologies commonly encountered in enterprise environments and the AZ-104 exam.