---
title: How do you ensure that the deployed Azure resources are secure?
date: 2023-10-13
tags: ["devsecops","L100"]
image : "/img/devsecops/ai-generated-secure-azure-resources.jpeg"
Description  : "Shift security to the left and apply industry best practices"
featured: true
---

The work of securing Azure resources never ends. It is a continuous process that starts with the design of the resources and continues through the life cycle of the resources. The following are some of the best practices that you can follow to ensure that the deployed Azure resources are secure:

- **Use Azure Security Center** to monitor the security of your Azure resources. Azure Security Center provides a unified view of the security state of your Azure resources. It also provides recommendations to help you improve the security of your resources. Azure Security Center can also be used to detect and respond to security threats.

- **Leverage Azure Policies** to enforce compliance with your corporate standards and to assess the compliance of your Azure resources. Azure Policy can be used to audit the compliance of your Azure resources and also to automatically remediate non-compliant resources.

- **Use Azure Key Vault** to store and manage cryptographic keys, secrets, and certificates. Azure Key Vault can be used to protect secrets such as passwords and connection strings. Azure Key Vault can also be used to encrypt data at rest and data in transit. Here we distinguish between the different types of Azure KeyVaults:

    - **Standard Azure KeyVault** is a software backed vault that uses FIPS 140-2 Level 1 validated HSMs. It is the most cost effective option and is suitable for most scenarios.

    - **Premium Azure KeyVault** is a software backed vault that uses FIPS 140-2 Level 2 validated HSMs. It is suitable for scenarios that require FIPS 140-2 Level 2 validation.

    - **Hardware Security Modules (HSM) backed Azure KeyVault** is a hardware backed vault that uses FIPS 140-2 Level 3 validated HSMs. It is suitable for scenarios that require FIPS 140-2 Level 3 validation. There is also a possibility to have dedicated HSM Vaults but companies must understand that implementing such high security measures will have a massive cost impact and during downtime, the vault will be unavailable.

Out of all the vaults available in Azure, my favourite is the Premium Azure Key Vault, as it offers an excellent balance between cost and security. If we also change our mentality and implement RBAC over indepent vault secrets instead of Vault policies, we can achieve a very high level of security while maintaining a decent operational cost by sharing the same vault across multiple applications and landing zones.

- **Use Azure Disk Encryption** to encrypt the operating system and data disks of your Azure virtual machines. Azure Disk Encryption uses BitLocker to encrypt the disks. Azure Disk Encryption can be used to encrypt both Windows and Linux virtual machines.