# VTP Lab

- Test VTP server/client/transparent modes and synchronization.

In reference to the network diagram provided, I configured 4 switches and a router.  
(See uploaded configs in `/configs` for running configurations.)

---

## Steps Performed

### Router-01

**Configured router to act as a Router-on-a-Stick**

- Created 2 subinterfaces for VLANs 10 & 20  
- Statically assigned IP addresses to act as the default gateways for each VLAN  
  *(Used a /24 for simplicity; a /29 could have been used to reduce broadcast traffic.)*  
- Brought the main interface up  

🔧 Config located in: `/configs/Router-01`

---

### Switch-01
** Acting a Primary VTP Server **

- Selected interfaces using interface range cmd 
- Enanbled Dot1Q encapsulation on links 
- Configured Trunk links towards Router-01 & Switch-02
- Allowed VLANs 10,20 (VLAN 1 acting as control plane / default VLAN)
- Set VTP Primary within priviledged exec mode
- Set VTP domain
- Set VTP password
- Set VTP Version 3
- Set VTP mode Server
- Created Vlans 10,20

🔧 Config located in: `/configs/Switch-01`

---

### Switch-02
** Acting as VTP Client **

- Selected interfaces using interface range cmd 
- Enanbled Dot1Q encapsulation on links 
- Configured Trunk links towards Switct-01 & Switch-03 & Switch-04
- Allowed VLANs 10,20 (VLAN 1 acting as control plane / default VLAN)
- Set VTP domain
- Set VTP password
- Set VTP Version 3
- Set VTP mode client

🔧 Config located in: `/configs/Switch-02`

---

### Switch-03
** Acting as VTP Client **

- Selected interfaces using interface range cmd 
- Enanbled Dot1Q encapsulation on links 
- Configured Trunk links towards Switct-02
- Allowed VLANs 10,20 (VLAN 1 acting as control plane / default VLAN)
- Set VTP domain
- Set VTP password
- Set VTP Version 3
- Set VTP mode client
- Set Access ports for x2 End device and added them to their designated VLANs

🔧 Config located in: `/configs/Switch-03`

---

### Switch-04
** Acting as VTP Transparent **

- Selected interfaces using interface range cmd 
- Enanbled Dot1Q encapsulation on links 
- Configured Trunk links towards Switct-02
- Allowed VLANs 10,20 (VLAN 1 acting as control plane / default VLAN)
- Set VTP domain
- Set VTP password
- Set VTP Version 3
- Set VTP mode transparent
- Set Access ports for x1 End device and added them to their designated VLANs

🔧 Config located in: `/configs/Switch-04`


---

### Additonal Notes

- Used MorbaXterm and selected the Switches and executed commands via 'Multi Exec' mode to speed things up
- Opted to not used DHCP for sake of simplicity and size of the VTP lab
- Configured Webterm (Docker based VMs) - with static IPs, Subnet masks and Default gateways (Pointed towards the apprpiate sub-interfaces for VLAN tagging)
