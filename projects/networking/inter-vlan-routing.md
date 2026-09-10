📋: Scenario:  TechCorp is opening a new regional branch office.  As the Tier 2 Network Technician, you have been assigned to build out the local network infrastructure from scratch.  The branch requires network segmentation to isolate administrative traffic, employee data, and guest Wi-Fi/devices.

🎯: Required Topology:
* 1x Router: Cisco 2911 (Name: R1-Branch)
* 1x Switch: Cisco Catalyst 2960 (Name: SW1-Core)
* 3x PCs:
  * Admin-PC
  * Staff-PC
  * Guest-PC
* Cabling Connections:
  * Connect R1-Branch to SW1-Core
  * Connect Admin-PC to SW1-Core
  * Connect Staff-PC to SW1-Core
  * Connect Guest-PC to SW1-Core

🌐 VLAN & Subnet Design: Create three distinct VLANs on SW1-Core:
* VLAN 10: Management | Subnet: 192.168.10.0/24
* VLAN 20: Staff | Subnet: 192.168.20.0/24
* VLAN 30: Guest | Subnet: 192.168.30.0/24

Port Assignments: Assign ports accordingly and make sure Trunk Port is on Gi0/1 as an 802.1Q
R1-Branch will act as the DHCP server for VLAN 20 & VLAN 30.

---

## Part 1: Adding the devices
* Add the router, Cisco 2911, and name it R1-Branch
* Add the switch, Cisco Catalyst 2960, and name it SW1-Core
* Add the three end user PC's and name them accordingly: Admin-PC, Staff-PC, and Guest-PC

## Part 2: Add the connections
* Using Copper Cross-Over, I connected GigabitEthernet 0/0 on R1-Branch to GigabetEthernet 0/1 on SW1-Core
* Using Copper Cross-Over, I connected FastEthernet 0/1 on SW1-Core to Admin-PC
* Using Copper Cross-Over, I connected FastEthernet 0/2 on SW1-Core to Staff-PC
* Using Copper Cross-Over, I connected FastEthernet 0/3 on SW1-Core to Guest-PC

## Part 3: Setup DHCP Server
* On R1-Branch, using CLI, turned on port GigabitEthernet0/0 using command ``` no shutdown ```
* Ran ``` encapsulation dot1Q 10 ``` (repeat for VLAN 20 and VLAN 30) to enable IEEE 802.1Q VLAN trunking protocol for each protocol
* Ran ``` ip address 192.168.10.1 255.255.255.0``` (repeat for VLAN 20 and VLAN 30) to set the default gateway and subnet maks
* 
