---
title: Cost optimization best practices
date: 2023-10-13
tags: ["azure","L100"]
image : "/img/azure/ai-generated-cost-optimization.jpeg"
Description  : "Keep your Azure costs under control with my notes from the field."
featured: true
---

Azure is not cheap. It is actually one of the most expensive public clouds out there. But it is also one of the most feature rich and the most secure. 
So, how can we optimize our Azure costs? Here are some of the best practices that you can follow to optimize your Azure costs.

To optimize the OPEX costs with Azure, you first need to understand why the costs are high and also to forecast them. To do that, you have a set of tools to help navigate in the Azure cost management space:
- Monitor and analyze your Azure bill with [Microsoft Cost Management](https://azure.microsoft.com/en-us/solutions/cost-optimization/#:~:text=Azure%20bill%20with-,Microsoft%20Cost%20Management,-.%20Set%20budgets%20and). Set budgets and allocate spending to your teams and projects.
- Estimate the costs for your next Azure projects using the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/) and the [Total Cost of Ownership (TCO)](https://azure.microsoft.com/en-us/pricing/tco/calculator/) calculator.
- Build your cloud business case with key financial and technical guidance from Azure Architects.
- Constantly review your Azure Advisor best practice recommendations for cost savings.
- Review your workload architecture for cost optimization using the [Microsoft Azure Well-Architected Review](https://go.microsoft.com/fwlink/?linkid=2237830) assessment and the Microsoft Azure [Well-Architected Framework (WAF)](https://go.microsoft.com/fwlink/?linkid=2237530) design documentation.
- Check out Azure offers and licensing terms such as [Azure Hybrid Benefit](https://azure.microsoft.com/en-us/pricing/hybrid-benefit/), paying in advance for predictable workloads with [Azure reservations](https://azure.microsoft.com/en-us/reservations/), Azure Spot Virtual Machines, Azure savings plan for compute, and Azure dev/test pricing.
- Implement cost controls and guardrails for your environment(-s) with [Azure Policy](https://azure.microsoft.com/en-us/products/azure-policy/). In case you get hacked, maybe you don't want those N-series Virtual Machines to be spun up in the middle of the night next to existing workloads. Hackers love to use GPUs for crypto mining and they don't want to harm you, they want your unsupervised money.

What would I first check to minimize the Azure costs? I would start with the following:
- When configuring Diagnostic Settings for your Azure resources, ensure that you are only sending the minimum required set of logs to the Log Analytics Workspaces and implement cold storage for the logs that you don't need to access frequently.
- Shut down resources that you don't need to run 24/7, espcially VMs. Virtual Machines Scale Sets can be scaled in and out using Azure Automation and Azure Functions or why not your own pipelines.
- Identify wether or not your resources are overprovisioned and resize them accordingly. Find them with Azure Advisor and get recommendations on how to reduce your spend by reconfiguring or consolidating them.
- Implement [saving plans](https://azure.microsoft.com/en-us/pricing/offers/savings-plan-compute/) for raw compute power and save up to 65% off pay-as-you-go pricing when you commit to spend a fixed hourly amount on compute services for one or three years.
- Receive a discount on your Azure services by purchasing [reservations](https://azure.microsoft.com/en-us/pricing/reservations/). Give Microsoft a glance at what you want to do in the upcoming years and they will give you a discount. It's a win-win.
- Migrate your workloads and save with [Azure Hybrid Benefit](https://azure.microsoft.com/en-us/pricing/hybrid-benefit/#overview). If are covered if you have Windows Server or SQL Server core licenses with Software Assurance or a subscription to these products, an active Linux subscription, including Red Hat Enterprise Linux or SUSE Linux Enterprise Server running in Azure. Have a look at the [Azure Hybrid Benefit Savings Calculator](https://azure.microsoft.com/en-us/pricing/hybrid-benefit/#calculator).

A comercial for Toyota I once heard over 10 years ago in the US, said something like this: "after you buy a car, all that matters is the service". 
If you are a partner, you must have an [ASfP Contract](https://partner.microsoft.com/en-us/support/advanced-cloud-support) and skip-the-line of your support cases. 
Get your escalations out and receive the support you need.

Too much too digest on cost optimization? Then learn in a structured approach at your own pace about the [Controlling Azure spending and managing bills with Microsoft Cost Management + Billing](https://learn.microsoft.com/en-us/training/paths/control-spending-manage-bills/). You will learn about:
- Microsoft Azure Well-Architected Framework - Cost optimization
- Introduction to analyzing costs and creating budgets with Microsoft Cost Management
- Save money with Azure Reserved Instances
- Optimize Azure costs with data analysis in Power BI
- Configure and manage costs as a Microsoft partner by using Microsoft Cost Management

My call to action to you is to **set a budget** for your Azure subscriptions and **get alerted** when you are about to exceed it!