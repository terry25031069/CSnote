---
title: 網路實習LAB2
---
### 1. Setup IP addresses on all routers. 20% A-B 192.168.1.0, B-C: 192.168.2.0, C-D: 192.168.3.0
Go into router 0 and open CLI

    Router>enable
    Router#conf t    // enter "configure terminal" will work the same
    Router(config)#int fa0/0
    Router(config-if)#ip addr 192.168.1.1 255.255.255.0	
    Router(config-if)#no sh

exit router 0 
Go into router 1 and open CLI

    Router>ENABLE
    Router#conf t    // congfigure terminal will work the same
    Router(config)#int fa0/0
    Router(config-if)#ip addr 192.168.1.2 255.255.255.0
    Router(config-if)#no sh	  
    Router(config-if)#do show ip route
    Router(config)#int fa0/1
    Router(config-if)#ip addr 192.168.2.1 255.255.255.0
    Router(config-if)#no sh

exit router 1
Go into router 2 and open CLI

    Router>ENABLE
    Router#conf t    // congfigure terminal will work the same
    Router(config)#int fa0/0
    Router(config-if)#ip addr 192.168.2.2 255.255.255.0
    Router(config-if)#no sh	  
    Router(config-if)#do sh ip ro
    Router(config)#int fa0/1
    Router(config-if)#ip addr 192.168.3.1 255.255.255.0
    Router(config-if)#no sh

exit router 2
Go into router 3 and open CLI

    Router>ENABLE
    Router#conf t    // congfigure terminal will work the same
    Router(config)#int fa0/0
    Router(config-if)#ip addr 192.168.3.2 255.255.255.0
    Router(config-if)#no sh	  
    Router(config-if)#do sh ip ro

### 2. Setup RIP(Routing information Protocol) at Router 1 & 2. 40%

go into router 1

    Router(config)#router rip  // make sure it is Router(config)#
    Router(config-router)#network 192.168.1.0
    Router(config-router)#network 192.168.2.0
    
    check for setup ip
    Router#sh ip ro  // R    192.168.3.0/24 [120/1] via 192.168.2.2, 00:00:25, FastEthernet0/1  will appear


go into router 2

    Router(config)#router rip  // make sure it is Router(config)#
    Router(config-router)#network 192.168.2.0
    Router(config-router)#network 192.168.3.0

    check for setup ip
    Router#sh ip ro  // R    192.168.1.0/24 [120/1] via 192.168.2.1, 00:00:03, FastEthernet0/0  will appear

### 3. Setup a static route at A to 192.168.3.0, and ping it at A. 20%

go into router 0

    Router(config)#ip route 192.168.2.0 255.255.255.0 192.168.1.2  // make sure its Router(config)#
    Router(config)#ip route 192.168.3.0 255.255.255.0 192.168.1.2
    Router(config)#do ping 192.168.2.0
    Router(config)#do ping 192.168.3.0

### 4. Setup  a default route at router D,  ping 192.168.1.0 at D. 20%


go into router 3 

    Router(config)#ip route 0.0.0.0 0.0.0.0 192.168.3.1
    Router(config)#exit
    Router#ping 192.168.1.0
###### tags: `Computer Network Lab` `CSnote`