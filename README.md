<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

## 🛠️ Step 1: Create a Network Security Group

1. Go to the **Azure Portal**
2. Search for and select **Network Security Groups**
3. Click **Create**
4. Fill in the required details:
   - Resource Group
   - NSG Name
   - Region
5. Click **Review + Create** → **Create**

---

## 🔗 Step 2: Associate NSG with Subnet or NIC

### Option A: Associate with Subnet
1. In NSG overview, select **Subnets**
2. Choose the VNet and subnet → Click **Associate**

### Option B: Associate with NIC
1. In NSG overview, select **Network Interfaces**
2. Choose the VM's NIC → Click **Associate**

---

## ➕ Step 3: Add Inbound & Outbound Rules

### Example Inbound Rule for HTTP
- **Priority**: 100
- **Name**: Allow-HTTP
- **Port**: 80
- **Protocol**: TCP
- **Source**: Any
- **Destination**: Any
- **Action**: Allow

### Example Outbound Rule to Block FTP
- **Priority**: 200
- **Name**: Block-FTP
- **Port**: 21
- **Protocol**: TCP
- **Source**: Any
- **Destination**: Any
- **Action**: Deny

> ⚠️ Lower priority numbers take precedence.

---

## 🕵️ Step 4: Inspect Network Traffic and Protocols

### Option 1: Using **Network Watcher – Packet Capture**

1. Go to **Network Watcher** in Azure
2. Enable it for your region if needed
3. Select **Packet Capture** → Add
4. Choose the target VM
5. Configure:
   - Duration
   - Protocol: TCP, UDP, or Any
   - Local file path or storage account
6. Start capture → Download the .cap file
7. Open in **Wireshark** for deep protocol analysis

### Option 2: Enable Diagnostic Logs

1. Go to NSG → **Diagnostic Settings**
2. Enable **Flow Logs**
3. Select Storage Account or Log Analytics
4. Use logs to monitor traffic allowed/denied

---

## 🛡️ Best Practices for NSG Configuration

- Use **least privilege**: only allow required ports
- Apply NSGs at **subnet** level for group policies
- Use **application security groups (ASGs)** for role-based access
- Regularly **audit flow logs**
- Monitor with **Azure Monitor Alerts**

---

## ✅ Summary

By the end of this guide, you should be able to:

- Create and apply NSGs
- Configure inbound/outbound rules
- Capture and analyze network traffic using Network Watcher
- Maintain a secure networking posture in Azure
