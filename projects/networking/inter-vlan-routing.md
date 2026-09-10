Scenario:  TechCorp is opening a new regional branch office.  As the Tier 2 Network Technician, you have been assigned to build out the local network infrastructure from scratch.  The branch requires network segmentation to isolate administrative traffic, employee data, and guest Wi-Fi/devices.

Required Topology:
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

VLAN & Subnet Design: Create three distinct VLANs on SW1-Core:
* VLAN 10: Management | Subnet: 192.168.10.0/24
* VLAN 20: Staff | Subnet: 192.168.20.0/24
* VLAN 30: Guest | Subnet: 192.168.30.0/24

Port Assignments: Assign ports accordingly and make sure Trunk Port is on Gi0/1 as an 802.1Q
R1-Branch will act as the DHCP server for VLAN 20 & VLAN 30.

---



