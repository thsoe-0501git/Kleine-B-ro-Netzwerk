## Project Overview
This project simulates a small customer service office network. 
The goal was to provide **secure employee access** to tenant data while offering 
**free Guest Wi-Fi** in the waiting room, ensuring complete separation between 
the two networks so guests cannot access the employee database.


## Network Topology
![Network Topology](diagrams/topology.png)

*   **R1 (Router):** Cisco 2911 (Inter-VLAN routing, DHCP, ACL)
*   **S1 (Switch):** Cisco 2960 (VLANs, Trunking)
*   **AP1:** Access Point for Guest Wi-Fi
*   **End Devices:** Employee PCs, Database Server, Guest Client

## IP Addressing Scheme
| VLAN | Purpose | Subnet | Gateway |
| :--- | :--- | :--- | :--- |
| **VLAN 10** | Employees | `192.168.10.0/24` | `192.168.10.1` |
| **VLAN 20** | Guest Wi-Fi | `192.168.20.0/24` | `192.168.20.1` |


## Technologies Implemented
*   **VLAN Segmentation:** Isolated Employee (VLAN 10) and Guest (VLAN 20) traffic.
*   **Router-on-a-Stick:** 802.1Q encapsulation on router sub-interfaces for Inter-VLAN routing.
*   **DHCP:** Dedicated pools for each VLAN to automate IP assignment.
*   **ACLs (Access Control Lists):** Blocked Guest-to-Employee traffic while allowing DHCP requests and Internet access.


## Final Verification & Proof of Security
| Test | Source | Destination | Result |
| :--- | :--- | :--- | :--- |
| Employee Access | PC1 | Server1 (`192.168.10.100`) | ✅ Success |
| Guest Internet Access | Guest PC | `8.8.8.8` | ✅ Success |
| **Guest Hacking Attempt** | **Guest PC** | **Server1 (`192.168.10.100`)** | **❌ Blocked (Request Timed Out)** |
