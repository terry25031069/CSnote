---
title: 網路實習LAB1
---

Switch:

Open CLI: Click on the switch and then click the CLI Tab
### 1.  Setup privileged mode password. 10%
	
	shown by CLI		type this column into CLI

	Switch>			    enable 
	Switch#			    configure terminal
	Switch(config)# 	enable secret ntpu	
	
### 2.  Setup a new VLAN and add an interface to the new VLAN 20%

	Switch(config)# 	vlan 2
	Switch(config-vlan)#exit
	Switch(config)#		interface fa 0/2
	Switch(config-if)#	switchport  access vlan 2
	Switch(config-if)#	exit

### 3.  Setup VLAN with IP address  20%

	Switch(config)#		interface vlan 1
	Switch(config-if)#	ip	address 192.168.4.1 255.255.255.0
	Switch(config-if)#	no sh	//short for no shutdown	
	Switch(config-if)#	exit

### 4.  Setup port security on switch at the new Vlan 50%
	
	Switch(config)#		interface fastethernet  0/2
	Switch(config-if)#	switchport mode access 
	Switch(config-if)#	switchport port-security
	Switch(config-if)#	switchport port-security mac-address sticky 
	Switch(config-if)#	exit
	Switch(config)#		exit

### Final. Check result

	Switch#			sh running-config
	Switch#			show port-security  interface fa 0/2
	Switch#			show vlan br
    
    
###### tags: `Computer Network Lab` `CSnote`