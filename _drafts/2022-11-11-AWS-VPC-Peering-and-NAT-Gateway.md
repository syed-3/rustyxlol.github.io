---
title: "AWS VPC Peering and NAT Gateway!"
date: "2022-11-10"
description: &desc "Everything I learnt about VPC and NAT Gateways"
summary: *desc
tags: ["personal"]
showToC: true
---

## Terminology

Let us start with a few keywords and their meanings before we dip ourselves into networking.  
*The definitions are purposely boiled down to something very generic and understandable, but this is networking and things can get really complicated really fast, if you want to know them in-depth, I have added a few resources below*

1. **Virtual Private Cloud(VPC)**: tries to simulate a private network or a private cloud
2. **Subnet**: A *logical* subdivision of a network(Break a bigger network into smaller networks)
3. **Subnet Mask**: The dreaded `/24`. A string on 1s in a network IP address(in binary of course).
When it comes to an IP address, **192.168.54.69** for example.  
**192** is your **country**  
**168** is your **state**  
**54** is your **city**  
**69** is your **home**  
And when your subnet is `/24`, you're basically saying that 192.168.54 will never change, meaning you can have different homes but country, state, and city will be the exact same for every home.  
*Don't go for `/24` unless you know what you're doing, go for `/16`*
4. **Internet Gateway**: The gateway to ~~heaven~~ internet from the VPC.
5. **Route Table**: Set of rules to instruct where the network traffic should go to and/or come from.
6. **NAT Gateway**: One way ticket to either the internet or another subnet
7. **Peering VPCs**: Establishing connection between two VPCs so they can use eachother.
8. **Classless Inter-Domain Routing(CIDR)**: Basically subnet masking but the representation is cooler, like `/24` above.

## VPC

### Background

What VPCs are and why we need them.

Amazon VPC it enables you to launch AWS resource into Virtual Network that you have created. 

It is similar to running your own data centre while utilising AWS scalable infrastructure.

Setting up Amazon VPCs is kind of tricky so follow these steps carefully.

### **VPC Setup**

In this step we will be creating VPC, Subnet, Route Table, and Internet Gateway one by one.

### **VPC**

Goto Services Search for VPC :

Select VPC

1. VPC >> your VPC >> Create VPC
2. Resources to create >> Select VPC only
3. Name tag >> "finance_vpc"
4. IPv4 CIDR block >> "10.0.0.0/16"
5. Tenancy >> default
6. Click Create VPC

We have created our VPC.

Next task is to Create a Subnet for our VPC.  

### **Subnet**

Select Subnet

1. In VPC ID Select your VPC
2. Subnet Name >> "finance_Public_subnet"
3. Availability Zone >> ap-south-1a
4. IPv4 CIDR block >> 10.0.1.0/24
5. Click Create Subnet

### **Route Table**

Select Route Table

1. Route Table Name >> "finance_public_route_table"
2. Select your VPC ID
3. Click Create Route Table

### **Internet Gateway**

Select Internet Gateway

1. Internet Gateway Name >> "finance_internet_gateway"
2. Click Create Internet Gateway
3. Select your Internet Gateway >> Actions >> Attach to VPC
4. Available VPCs >> Select your VPC >> Attach Internet Gateway

The Following Step is to link our Subnet and Route Table

Goto Route Table

1. Select Subnet associations --> Edit Subnet associations
2. Available Subnets >> Select your Subnet
3. Save associations

Back to Route table

1. Select Routes --> Edit Routes
2. Destination >> 0.0.0.0/0
3. Target >> Select Internet Gateway
4. Save changes

We have Created our VPC successfully.

## **Resources**

1. Subnetting Tutorial - [Subnetting](https://www.subnetting.net/Tutorial.aspx)
2. CIDR Blocks/Notation - [Wikipedia](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation)
