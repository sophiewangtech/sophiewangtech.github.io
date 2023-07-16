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
