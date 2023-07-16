---
title: "VMSS Flexible Mode Networking Requirement"
date: 2023-07-16
categories:
  - Azure VM
tags:
  - Azure
  - VMSS
---

You might already notice when you create VMSS using az cli. The default orchestration mode will be changed to Flexible mode in November 2023. One big difference in creating the VMSS Flex is that it requires explicit outbound connectivity configured. 

Recently I took a case that customer has special networking requirements for creating VMSS Flex. I took the chance to have a deep dive of configuring the networking for VMSS Flex. I'd like to share it here. 


Customer's requirements:
Customer needs to create VMSS with Flexible orchestration mode. He needs to create in an existing vNet "prdvmss-vnet" and subnet "prdvmss-subnet1". There are no Load Balancer or NAT gateway allowed to be created in the vNet. Their organization also doesn't allow any public IP used in Azure environment.


The issue Customer met:

Customer tried to create the VMSS in the portal. He chose the existing vnet and subnet. He kept the LB setting as none. 
He edited the vnic to disable the public IP.
After he clicked ok to save and returned to the VMSS creating page, he found a warning showing that "The virtual machine scale set with Flexible orchestration mode does not have outbound connectivity. Please use an Azure load balancer or configure a NAT gateway or user-defined routes (UDR) on the subnet."
He failed to create the VMSS in the Azure portal.
He remembered that previous he created VMSS with uniform orchestration using the same steps and he was able to create it successfully. 