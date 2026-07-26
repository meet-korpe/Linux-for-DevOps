# Network Firewalls and Security Groups

## 1. What is a Firewall?

A firewall is a security system designed to **block unauthorised access** to or from a private network 1. It acts as a barrier between a trusted internal network and untrusted external networks (like the Internet).

### Primary Functions

| Function | Description |
|---|---|
| IP Filtering | Controlling access based on specific IP addresses. |
| Port Forwarding | Directing traffic from outside to specific services inside the network. |
| NATting/PATting | Managing Network Address Translation and Port Address Translation. |
| Port Management | Opening specific ports based on **Blacklists** (blocking specific items) or **Whitelists** (allowing only specific items). |
| Multi-role Capabilities | Can function as a **proxy server, a VPN, or a router**. |

## 2. Classification of Firewalls

Firewalls are generally categorized into three main types based on their implementation:

1. **Hardware Firewalls:** Dedicated physical appliances. Examples include **Juniper, Sophos, Cisco ASA, Palo Alto, Fortigate, and Checkpoint**.
2. **Software Firewalls:** Installed directly inside an Operating System or Server. Examples include **Windows Firewall** and Linux-based tools like **iptables** and **firewalld**.
3. **Semi-Firewalls / Open Source:** Software that can be installed on bare-metal hardware or as an OS, such as **pfSense or Untangle**.

## 3. Traffic Direction and Rules

Firewalls manage two types of traffic flow:

- **Inbound (Ingress / Incoming):** Traffic coming from the internet or external sources into your network.
- **Outbound (Egress / Outbound / Outgress):** Traffic originating from your internal network going out to the internet.
- **Default Behavior:** Often, firewalls are configured to **"Deny All"** by default, requiring specific "Allow" rules for traffic to pass.

## 4. Stateless vs. Stateful Firewalls

- **Stateless Firewall:** Filters individual packets based on static information (like source/destination IP) without regard to the state of the connection.
- **Stateful Firewall:** Monitors the **state of active connections**. For example, if an outbound connection is established from an internal server, a stateful firewall will automatically allow the related incoming response traffic without needing a separate inbound rule.

## 5. Security Groups (SG)

Security Groups are a specific type of firewall used in cloud environments (like for AWS EC2 instances) to control traffic at the instance level.

### Key Characteristics

- **Default Policy:** "All Deny".
- **Flexibility:** One Security Group can be applied to **many EC2 instances**, and a single EC2 instance can have **many Security Groups**.

### Capacity Limits (per VPC)

- Typically allows for up to **250 Security Groups**.
- Usually supports up to **60 Inbound** and **60 Outbound** rules per group.

