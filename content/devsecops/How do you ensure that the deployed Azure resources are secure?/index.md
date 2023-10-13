---
title: How do you ensure that the deployed Azure resources are secure?
date: 2023-10-13
tags: ["devsecops","L100"]
image : "/img/devsecops/ai-generated-secure-azure-resources.jpeg"
Description  : "Shift security to the very left and apply industry best practices"
featured: true
---

The work of securing Azure resources never ends. It is a continuous process that starts with the design of the resources and continues through the life cycle of the resources. The following are some of the best practices that you can follow to ensure that the deployed Azure resources are secure:

Use **Azure Defender for Cloud** to monitor and secure your Azure resources. It is a cloud-native application protection platform (CNAPP) with a set of security measures and practices designed to protect cloud-based applications from various cyber threats and vulnerabilities. Defender for Cloud relies on 3 main pillars:
  1. **CSPM** or Cloud Security Posture Management which is a solution that surfaces actions that you can take to prevent breaches.
  2. **CWPP** or Cloud Workload Protection Platform which is a solution built specifically for the protection of servers, containers, storage, databases, and other workloads.
  3. **DSO** or DevSecOps which is a solution that unifies security management at the code level across multicloud and multiple-pipeline environments (now available to integrate with GitHub Actions and Azure Pipelines). You can protect your code management environments and your code pipelines, and get insights into your development environment security posture from a single location. Defender for DevOps, a service available in Defender for Cloud, empowers security teams to manage DevOps security across multi-pipeline environments.

Let's go through each of them one by one:

1. Improving the **Security Posture** of your organization can be achieved by developing the following capabilities in your organization:
    - Leverage ***Azure Policies** to enforce compliance with your corporate standards and to assess the compliance of your Azure resources. Azure Policy can be used to audit the compliance of your Azure resources and also to automatically remediate non-compliant resources.
    - Track your **Secure Score** and improve the security of your workloads as you build them. A healthy Secure Score is of a minimum of 65% per each subscription, yet at least 80% should be your main goal.
    - Connect to your multicloud environments with agentless methods for CSPM insight and CWP protection.
    - Use the default dashboard to see weaknesses in your security posture.
    - Get advanced tools to identify weaknesses in your security posture, including governance to drive actions to improve your security posture, regulatory compliance to verify compliance with security standards and cloud security explorer to build a comprehensive view of your environment.
    - Enable Data Aware Security Posture to discover datastores containing sensitive data, and reduce the risk of data breaches.
    - Model traffic on your network to identify potential risks before you implement changes to your environment.
    - In Azure, setting the correct RBAC permissions is key to a secure environment. You can also use Azure Policies to audit and enforce RBAC permissions in your Azure environment. Constantly review who has access to what and always go ahead with the minimum set of permissions needed to perform a task.
    - Leverage resource identities (system or user assigned managed identities) for service to service authentication instead of using credentials. This will reduce the atack surface of credentials that can be compromised.

2. Protecting your cloud workloads or **CWPP** has to do with chosing the correct protection plan for each of your workload types, get alerted when something is happening using Action Groups and act accordingly as soon as possible.
Choose the right defender plan and configure it as you build your infrastructure, not at a later time. Think of the following:
    - Defender for Servers
    - Defender for Storage
    - Defender for Azure SQL Databases
    - Defender for SQL servers on machines
    - Defender for Open-source relational databases
    - Defender for Azure Cosmos DB
    - Defender for Containers
    - Defender for App Service
    - Defender for Key Vault
    - Defender for Resource Manager
    - Defender for DNS

Get informed of real-time events that threaten the security of your environment and immediately correlate them your SIEM (Security Information and Event Management), SOAR (Security Orchestration Automated Response) and ITSM (IT Service Management) systems.

3. **Shift Left** and apply security best practices early in the development process. This is also known as **DevSecOps**. DevSecOps is a set of practices that combines software development (Dev) and IT operations (Ops) with security (Sec). DevSecOps aims to shorten the development life cycle and provide continuous delivery with high software quality. The teams who start rolling out Azure workloads with security in mind will anticipate and mitigate security issues early in the development process. This will also reduce the cost of fixing security issues later in the development process or in production stages.

On top of everything, use **Azure Key Vaults** to store and manage cryptographic keys, secrets, and certificates. Azure Key Vault can be used to protect secrets such as passwords and connection strings. Azure Key Vault can also be used to encrypt data at rest and data in transit. Here we distinguish between the different types of Azure KeyVaults:
- **Standard Azure KeyVault** is a software backed vault that uses FIPS 140-2 Level 1 validated HSMs. It is the most cost effective option and is suitable for most scenarios.
- **Premium Azure KeyVault** is a software backed vault that uses FIPS 140-2 Level 2 validated HSMs. It is suitable for scenarios that require FIPS 140-2 Level 2 validation.
- **Hardware Security Modules (HSM) backed Azure KeyVault** is a hardware backed vault that uses FIPS 140-2 Level 3 validated HSMs. It is suitable for scenarios that require FIPS 140-2 Level 3 validation. There is also a possibility to have dedicated HSM Vaults but companies must understand that implementing such high security measures will have a massive cost impact and during downtime, the vault will be unavailable.

Out of all the vaults available in Azure, my favourite is the Premium Azure Key Vault, as it offers an excellent balance between cost, functionality and enterprise level security. If we also change our mentality and implement RBAC over indepent vault secrets _instead_ of Vault policies, we can achieve a very high level of security while maintaining a decent operational cost. Sharing the same vault across multiple applications and landing zones and think about how you can implement honeypotting practices to detect malicious activity.

Is this enough? Never, as it all starts with humans. Educate your teams and make them aware of the security risks and how they can mitigate them. Learn to embrace failure and learn from it. Implement a culture of continuous improvement and always be ready to adapt to new challenges.