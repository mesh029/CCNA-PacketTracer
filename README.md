# CCNA Packet tracer

A repo on CCNA and packet tracer



Packet tracer is a cross platform visual simulation tool designed by cisco systems that allows users to create *network topologies* and imitate modern *computer networks*.



## Packet tracer labs

> This is a documentation on packet tracer lab practicals by me.





### Configuring name and passwords on cisco router



#### Lab tasks:



* Setting router name to R1

> command: *enable*
> > *configure*
>>> *hostname R1*

* Set privileged mode password to cisco

> command: *enable password cisco*



* Set privileged mode secret to cisco

> command: *enable secret cisco*



* Set console line to lab 

> command: *line con 0*
> > password lab
> > login



* Set auxilary line password to cisco lab

> command: *line aux 0*
> > password lab
> > login





### Basic router configuration

This includes nameing, giving some recognizable names to the devices and then setting up the passwords to prevent unauthorized access.

Configuring routers and enable routers for dynamic routing using RIP protocal(Routing Information Protocol)

RIP uses hop counts while directing traffic in the network. RIP is widely used compared to other routing protocols because of its simplicity. RIP has a simple working mechanism that uses hop oounts while directing traffic in the network.

To set up routers we assign ip adddresses to the router interfaces. Its best practice to assign unique names to the routers.



We use a basic routing protocol. The RIP. After implementing the RIP protocol to all users we can now look into the routing table of every router to check if it has learned the routes with the help of RIP protocil.



To check the routing table:

> command: *show IP route*



After successful configuration of the routing protocol, we must see the routes in the routing table and if we are unable to see the router then check what was done wrong.



By default RIP auto summarizes the routes so we have to disable the summarization on each router.



#### Lab tasks:



* Assign IP Addresses for all routers

> command: *enable*
> > *configure*
>>> *in fa 0/0 (fa means fast ethernet port)*
> ip add 192.168.1.2 255.255.255.0 / 192.168.2.1/ 192.168.2.1
> no sh





* Enable rip protocol and disable auto summarization

> command: *enable secret cisco*



* Set router 0 name as Arizona, router 1 as Virginia, router 2 as NY

> command: *line con 0*
> > password lab
> > login



* Set description of the interfaces as follows

fa 0/0 of router 1 - connection to branch 1

se 2/0 of router 1 - connection to branch 1

se 2/0 of router 2 - connection to branch 1





> command: *line aux 0*
> > password ciscolab
> > login



* Set MOTD on all routers to UNAUTHORISED ACCESS IS NOT ALLOWED





# CCNA CERTIFICATION



## Datalink layer/ Layer 2 



### VLAN's



#### Commands



Remote features dont have any physical ports on the router thats why we use virtual lines/ port inside of a router

Vty - virtual teletype

You can set exec timeouts for console ports

Vty commands applies to people who are remotely logging in to the router

There are different types of password

> Logging password



Power cycling a router when all configurations are sitting in the running config loses all configurations. It is recommended to add them to the startup config



| Command     | Description |
| ----------- | ----------- |
| exec-timeout x xx    | Sets time before user is logged out automatic from the console     |
|logging synchronous| keeps console logging messages from interrupting typping        |
|config-t | enter config mode|
|line console x| to head to the console port|
|password xxxxx| creating a password|
|exit | one mode at a time|
|end| back to privileged mode|
|logout| log completely out of the router|
|enable| use privileged cli mode|
|line vty ?|configure virtual lines or ports for remote login|
|line vty 0-15|enter config mode for the listed ports|
|do show running-config|view configurations on the running configuration |
|service password-encryption|encrypts all current and future passwords|
|show startup-config|shows start up config|
|copy running-config startup-config/ copy run start/ write memory/ wr|Copies contents of the running config to the startup config|
|fastEthernet 0/24| Entering the port number|
|switchport mode access|unconditionally going to be an access point|
|switchport access vlan 150| you are going to be part of VLAN 150 at this point|
|shwo VLAN brief|shows details about the VLAN|
|show interface fastEthernet 0/24 switchport||
|switch port mode access|Unconditionally sets a port to access mode|
|switch port mode access vlan 150|Puts the port to 150|
|name XXXX|naming a VLAN|


### Links on a switch



##### Access link



Two steps to create an access port:

- Create a VLAN 

- Assign that VLAN to a port



As soon as that port becomes part of the VLAN it becomes an access port

Then the port becomes an access port.



### Trunk Link

Can have multple VLANS at once/ at a time



#### frame tagging



Switch puts a tag on each frame so the other can identify it

Each frame has an identifier



frame tagging is done using protocols



#### InterSwitch link

Cisco propriety



Takes an original frame from one switch and encapsulates it in a new 26 byte head with a 4 byte footer with a frame

The new frame has a new field in it that identifies the VLANS being carried inside



#### IEEE802.1Q dot1q

Open standard

Inserts a 4 byte field in the original field and it is a tag identifying what field that VLAN belongs to.

Maximum transmission unit for ehtenet is 1500bytes

Adding 4 bytes of a dot1q to it giveth you 1504 bytes



> Native VLAN feature of a dot1q trunk

This is the VLAN not tagged

Transverses the trunk without a tag



ISL adds a 26 byte header, 4 byte tag is much easier to process hence IEE802.1q is better





#### Dynamic trunking protocol/ DTP



Perfoms automatic trunk negotiation between switches that are connected on port. 



- Dynamic desireable mode



It will send DTP frames and respond to DTP frames from the other end of the link

Switch models that end with the number 50 will have all its ports in Dynamic desirable mode.

When connected with crossover cables....an Trunk will automatically come up.



> Crossover cables are used for simillar devices
> Straight-through cables are used for disimilar devices



Both sides are going to send and respond to frames from the other side.

Port initiates trunking



- Dynamic auto mode 



Port does not initiate trunking

Port responds to DTP frames from the other side but will not send DTP frames from the other side.





Switch modes with their number 60 have their ports in dynamic auto mode by default. So when switches connected back to back with each other with a crossover cable, trunk won't come up.



You respond to DTP frames you don't send them.



- Simply mode on



Sets the local port to trunking unconditionally

Will send and respond to DTP frames





A VLAN IS A LAYER 2 BRODDCAST DOMAIN



### Trunking configuration 



n.802.1q

> n - negotiate
> 108.1q- Trunking protocol



Native vlan of a .1q trunk is the vlan that goes across the trunk untagged

By default all vlans are allowed on a trunk



|Command|Description|
|-----------|-----------|
|configure t|Enter config mode|
|int fastethernet 0/1||
|do show interface fastethernet 0/1 switchport, switch port mode dynamic desirable, do show interface trunk|Autonegotiate trunking|
|switchport trunk allowed vlan|View alloed vlans on the trunk|
|trunk allowed vlan 1, 150, 200-220|set allowed vlans over the trunk|
|switchport trunk native vlan 150|vlan will not add a tag to vlan 150 unless its not native|
|switchport mode trun, do show interface trunk||
|switch port encapsulation dot1q|Set protocol manually|
|shut|shuts down the swithc|
|no shutdown|powers it back on|
|switchport no negotiate|No trunk negotiation with the other end at this point/ turns off dtp|
|do show interface fastethernet0/1 switchport|checks trunking info of the switch|
|do show running-config|current configurations|
|do show start|startukp configuration|
|copy running-config startup-config||
|show interface trunk|view details about the trunking|





No n infront of the trunking protocol means you are not negotiating the trunking anymore



## Spanning tree protocol



Created by Radia Prolman (1970) while working for zerox

- Prevents links or loops from looping around a network when there are redundant path present

- Switch floods out unknown unicast frames resulting in a loop 

- PC's can crush since too much frames will gather looping around the network

- This is a LAYER 2 STORM OR A BROADCAST STORM

- Switches update their MAC address tables (TRASHING THE MAC TABLE), no forwarding decisions are made hence enough traffic cues up on the switch causing it to crush. So the spanning tree protocol shuts down redundant links.

- Works to prevent loops tbetween switches when there are redundant links present.

- Spanning ttree is on by default on all switches

- When switches powrer up, the spanning tree protocol is sent between each other spanning tree protocoal frames called BPDU (Bridge protocol Data Unit) Sent every two seconds outS



 # Steps for the Spanning Tree Protocol to Converge

 1.  Elect one root bridge per layer 2 domain/ elect one designated port per segment
- Elect one switch to be a root bridge

 2. Elect a root port per non root switch
- For the others, we elect a root port

 3. Elect one designated port per segment
- A segment is a link between two switches






#Spanning tree decision process

### i) Lowest bridge ID

### ii) Lowest path cost
- Route port election per non root switch

>  - Only happens on non root switches
>  - Happens according to Root PAth Cost
> - Root path cost - This is the distance for each link speed

|SPEED|Root Path Cost|
|-----------|--------------|
|10mb/s| 100 |
|100mb/s| 19 |
|1000mb/s| 4 |

>- Btw...FastEthernet - Path cost = 19 and the root switch is the only one sending BPDUs
> - The root path cost inside of a BPDu is incremented when a BPDU enters a switch not when it leaves a switch
> - So Root Path Cost starts at zero
> - Lowest Root Path Cost is elected





### ii) Lowest sender bridge ID
 - When the route path costs are equivalent, the switch has got no choice but to move to the next step in spanning tree decision process
 - The sender bridge ID, is the bridge ID of the switch sending the BPDU.

 - Switch compares the sender bridge ID, then selects the one with the lower bridge ID. I.e, a switch withe the MAC address BBBB will be selected over one with the MAC Address CCCC

- if there are two or more ports with the same sender bridge ID, then the switch moves to the last step of the spanning tree decision process



### ii) Lowest sender port ID

- Id of the sending switch

- The port with the lowest sender port ID becomes the root port


When switches power up they imediately start sending frames to each other out of all ports called BPDU's

- BPDU's havefour fields

### i) Route bridge id

Route bridge id = Priority field + MAC address

| |MAC ADDRESS|PRIORITY FIELD|
|------------|-----------|--------------|
|BITS|48|16|
|^ 2||65536|
|RANGE|48|0-65535|
|SWITCH SETTINGS ID BRIDGE ID|_|32768|

- Switch with the lowest MAC Address becomes the route because the switch with the loweest bridge
- Each switch initially announces itself as the root and sets the Root Bridge ID field id in the BPDU equal to the its Sender ID field
- When a switch recievesa a BPDU from another switch with a better Bridge ID(lower bridge ID) It stops sending its own BPDU and starts relaying superior BPDU's
- Given enough time, the switch with the lowest Bridge ID(In this case one with the lowest MAC address) becomes the root switch

- So switch A becomes root and continues sending BPDUs and every other switch relaying BPDUs sent by the root switch


### ii) Route path crossed

### iii) Sender bridge id
- Id of the sending switch

 ### iv) Sender port id

- Id of the sending switch

### Electing one designated port per segment

Designated port per segment is also selected according to the route path cost

- The lowest route path cost wins

- All ports on a route bridge will become a designated port


### Root ports and designated ports

- Initally all ports are put in blocking(no BPDPUs are being fowarded- lasts 20seconds)

- Listening then happens for 15 senconds(BPDU's are being sent are being received, route bridge and  route bridge elections are happening ) AKA spanning tree forward delay

- Learning stage also lasts 15 seconds and is called forward delay(No data traffic flowing but switches are still populating the MAC address tables, to reduce flooding, once the switch is due start fowarding data traffic the mac address tables is populated as much as possible to reduce flooding once forwarding starts )

- The switch starts forwarding data traffic

- Designated and root ports are put in forwarding now.

- Non designated/ alternate ports are put in blocing

- hence no loops because the alternate ports are blocked






### Per VLAN spanning tree protocol PVST


- 5 vlans means 1 spanning tree per vlan

> Common spanning tree 
> or Regular spanning tree



- Each link is blocking for a seperate VLAN however it is being used for some traffic so bandwidth is not wasted completely because each link is being used for each of the vlans

- Better bandwidth utilization

- The Bridge ID now consists of a 4 bit vlan id plus 12 bit priority plus 48 bit MAC



![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/pvst1.PNG)



#### Demo

Commands



|Command| Function|
|---------|--------|
|show vlan brief||
|show spanning-tree vlan xxxx|Shows details about the spanning tree protocol|
|spanning-tree vlan xxxxx priority||
|spanning-tree|int f0/24, spanning-tree portfast|
|do wr|save work|



### Spanning tree enhancements



- Takes 50 seconds for spanning trees to converge and put the ports from blocking to forwarding

- Port fast feature - Port skips all transition states and immediately jumps to forwarding

- BPDU guard frature - used in conjunction with the port fast feature (One with malicious intent can replace your switch with one of theirs and get traffic info) As soon as BPDU guard feature is enabled on port 3 say...as soon as port 3 receives a BPDU from unknown switch, it will be shut down



- ROUTERS DO NOT UNDERSTAND BPDUs

- Switch ports that have routers connected to them can have port fast feature enabled since they don't need to wait for the spanning tree protocol to complete so they can start communicating]

- Switch ports by default are disabled...ports on routers, however, are in administratively down mode




|Command| Function|
|---------|--------|
|configure t||
|interface fastEthernet0/0||
|no shut|That command turns on the router port|
|shutdown|put the router administratively down|



- note it will take about 50 seconds before the link is active because of the spanning tree protocol



|Command| Function|
|---------|--------|
|configure t|admin mode|
|int fa0/24|Going into a port|
|spanning-tree portfast |pops directly into forwarding regardless of the spanning tree protocol|
|do wr|saving our commands|



- Now the router will come alive real fast





# Virtual trunking protocol



- Only works over trunked links/ trunked ports

- Employs a server client mechanism

- VLANs on the switch are stored in a file in flash called vlan.dat

- Operates in 3 modes

### VTP Server mode
 > The Server switch can modify its vlan.dat
 > modifications include: 
 > > - Adding a vlan
 > > - Deleting a vlan
 > > - Renaming a vlan
 > > - Changing a vlan's mtu(maximum transmision unit(default = 1500bytes))
 > The modifications are carried downstream from the server swtich in VTP advertisemends

### VTP client mode

 > - The client switch will listen to this modifications sent by the server switch and do so accordingly
 > - The client switch however is not allowed to edit the vlan.dat


### VTP transparent mode

 > - The VTP transparent mode switch will relay VTP advertisments but won't comply with the server switche's demands
 > - The switch will however foward VTP advertisements to downstream clients
 > Can modify its vlan.dat file
 > > - Can add its own vlans
 > > - Can delete its own vlans
 > > - Change the vlan mtu
 > > - Change the vlane name


### Lab on vlan trunking protocol

- By default, all switches are VTP server switches

- All network, if ur using DTP, must be in the same domain else switches wont communicate

- Configuration revision - how many changes have been made to vlan.dat file

- A vtp transparent switch has its configuration revision set to zero because it is a count of the modifications made by the server switch to the vlan.dat file

- A transparent switch does not participate in vtp. It only relays vtp information.

- VTP version 2 supports token ring VLANs 1 does not support token ring





| Command     | Description |
|-----------|-----------|
|vtp mode server|sets a switch to VTP server mode|
|vtp domain ccna|Creates a |
|vtp password cisco| changes password|
|do show vtp status|shows details of the vtp|
|vtp version 2|run a different version of vtp|
|vlan 123| creates VLAN 123|
|do show vlan brief|shows vlan details|
|no vlan 123| negates the vlan|
|do show vtp password|shows the vtp password|
|vtp mode transparent|puts the switch in transparent mode|




# Network layer (Layer 3)

Network layer controlls communication between broadcast domains

- You will need layer 3 to move from one broadcast domain to another

- You will need a router in layer 3

- Routing is a layer 3 function

- Sends data between broadcast domains

- The pdu(protocol data unit) at layer 3 is called a packet



## Layer 3 addressing scheme



- The addressing scheme at layer 2 is MAC addresses

- Addressing scheme = ip addresses



### Ip addresses

- 32  bits in length 

- written in 4 fields of 8 bits each seperated by a dot(dotted decimal format)

- Each of the octects can range between 0-255

- Each bit in the octed can be turned on (1) or off (0)



 ![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/octed.PNG)
 
 
 - Example
 > *10.0.128.50*
 > Depending on which bits are turned on and off in this ip address within each successive octet, the IP address is assigned.
 
 
 ### Classfull ip addressing
 
 - Ip addressing was broken down into classes called classfull ip addressing
 - Ip addresses are not broken down classfully but classlessly

#### Class A
- Class A addresses
- The value of the first octed has to be a number between 1 and 126
- Subnet musk has to be 255.0.0.0
- Unicast - One to one transmision
- Broadcast - One to many transmition
- Multicast - Magazine like transmision, one to many transmission but the host has to be subscribed
Apply for the below table

|Class|Value of first octet|Subnet mask|Classless interdomain routing notation(CIDR)||
|--------|---------|--------|---------|----------------|
|A|1-126|255.0.0|/8|example: 10.10.10.10/8|
|B|128-191|255.255.0.0|/16|150.101.45.45/16|
|C|192-223|255.255.255.0|/24|200.0.0.30/24|
|D|224-239|MULTICASTIG |MULTICASTING||
|E|240-255|EXPERIMENTAL/UNUSED|EXPERIMENTAL/UNUSED|
||127.0.0.0|RESERVED FOR TESTING|
||127.0.0.1|LOCAL LOOP BACK|If you can reach or ping this address,then the tcp/ip stack was properly installed on your machine|


- Ip address has a network portion and a host portion
- A subnet ask seperates a network address from the host address
- If a corresponding bit of the ip address in the subnet mask is on, that bit belongs to the network portion of the ip address
- The host portion's corresponding bits in the subnet mask turned off


![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/CIA1.PNG)


- For example: 200.10.10.10

> The network address here will be 200.10.10.0/24
> The first address will be 200.10.10.1
> The last address 200.10.10.255
> Valid range of addresses that can be asssigned to pcs is 200.10.10.1 - 200.10.10.10.254
> Formula of valid addresses is 2^n - 2 where n = number of host bits(8 in this case)
> So 2^8-2 = 256-2 n= 254

- Example: 150.100.10.10

> Mask = 255.255.0.0
> Network address = 150.100.0.0/16
> First valid address = 150.100.0.1
> Last possible address = 150.100.255.255(broadcast address)
> Last valid address = 150.100.255.254
> Range = 150.100.0.1 - 150.100.255.254 (valid range)
> Number of hosts = 2^16-2 = 65536-2 = 65534

- Example 10.10.10.10

> Mask = 255.0.0.0
> Network address = 10.0.0.0/8
> First valid address = 10.0.0.1
> Last possible address = 10.255.255.255(broadcast address)
> Last valid address = 10.255.255.254
> Range = 10.0.0.1- 10.255.255.254(valid range)
> Number fo hosts = 2^24-2 = 16777216-2 = 1677214


- The right most octed full before adding one to the octed to the left of it

- You cannot use the first and last address of any network for your pc (The first address is the network address itself, the last address in any network is the broadcast, any messages sent to this address will be received by all hosts in this netork)
- Any message sent to the  *Broadcast address* will be received by all hosts in the network


*****



### Classless ip addressing

- In real sense, when buying a class of say 30 IP addresses, one would have to come up with a class c range but you would have acquired an entire class C for example
- Classfull ip addresses won't work if we needed Addresses less than 254


- Example:

> 150.101.45.0
> This is a clsas B address
> Should be a /16
> We need 30 addresses
> what would the mask look like if we gave it a /27?
> So 3 bits are turend on in the last octet
> 255.255.255.224

Last octet....

|1|1|1|0|0|0|0|0|
|----|----|----|----|----|----|---|---|
|128|64|32|16|8|4|2|1|

> - 128+64+32 = 224
> - How many total hosts can be had in this network?
>> - Network address = 150.101.45.0
>> - Look at the value of the last bit turned on in the subnet mask which is 32
>> - This gives you your **block size ** = 32

|Address||
|---|---|
 |150.101.45|.0|
 |First valid host address|.1|
 |Last valid address on this street|.31|
|Last possible address on this network|.32|
 ||.64|
|||
 ||.96|
 
> - number of hosts = 2^n - 2 = 2^5-2 = 32-2 = 30
> - In actual sense we can work backwards
> - By finding the number of host(n) bits that need to be available to get 30 possible network hosts(in this case 5)
> - Then subtracting from the subnet mask 32 bits = 32-5 = 27
> - This will enable you get the subnet mask notation == /27
> - **Since a /30 or a 252 mask only allows 2 addresses, it should only be used over point to point links**
> - example:
> network  address - 150.101.45.0/30
> subnet mask - 255.255.255.252

|Address||
|---|---|
 |150.101.45|.0|
 |First valid host address|.1|
 |Last valid address on this street|.2|
|Last possible address on this network(broadcast)|.3|
 ||.4|
|||
 ||.8|
 
 
> - example:
> network  address - 150.101.64.0/19
> subnet mask - 255.255.224.0

 |Address|||
|---|---|---|
 |150.101|.0|.0|
 |First valid host address|||
 |Last valid address on this street|||
|Last possible address on this network|||
 ||.64|
 |First valid host address|.64|.1|
 |Last valid address on this street|.95|.254|
|Last possible address on this network(broadcast)|.95|.255|
|Valid range|.64|.1|
|through|.95|.254|
|||
 ||.96|



 _Hence classless ip addressing_


*****


# Process of encapsulation and deencapsulation with ARP(Address resolution protocol)

*subnettingquestions.com*

- The pdu at layer 3 are packets

### PACKET

|Destination|Source Ip address|Data Field|Frame Check Sequence(CRC)|
|---|---|----|---|
|Ip address of the destination|Ip address of the source||Frame Check sequence that handles the C Redundancy check|

### Encapsulation

- Host 1 and host 2 are connected in the same LAN
- Host 1's ip address is 10.10.10.1 and host 2's ip address is 10.10.10.2
- Host 1 wants to ping host 2


> **What's Ping**
- Ping is a testing utility
- Works with the internet control messaging protocol (icmp)
- Ping has 2 parts, an echo and an echo reply


- Host 1 creates a packet with the source ip address and destination ip address
- A switch is one data link by default
- Host 1 needs to create an ethernet frame to send the packet over to host 2, because it uses data link for transmision or local data link
- Host 1 knows its own mac address but not host 2's
- Host 1 generate generate an ARP request, requesting for the mac address, for a host with an ip address 10.10.10.2
- The ARP request is a broadcast sent to the destination address 255.255.255.255 which is the all networks all broadcast subnet address
- Host 2 replies to the ARP broadcast and the reply is a unicast back to the IP address of host 1
- Host 2 replies with its own MAC address
- ARP basically resolves ip addresses to their relevant mac addresses and then stores them in a table
- The process happens once in host 1
- Once host 1 has a binding in the table relating the ip of host 2 to its MAC address it wont need to go through the same process again
- Host1 encapsulates the original ICMP packet and puts it inside the data portion of the ethernet frame it created it'd look sth like this.


|Destination|Source Ip address|Data Field|Frame Check Sequence(CRC)|
|---|---|----|---|
|BBBB|AAAA|<table><tr><td>Destination MAC<td>Src MAC<td>Data<td>FCS (CRC)</tr><tr><td>10.10.10.2<td/>10.10.10.1<td>data<td>FCS(CRC)</td><tr/></table>|FCS handling CRC|


- The act of encapsulation means I take the layer 3 packet and put it into the data portion of the frame
- Host1 will thn transmit the frame over to host2
- Host2 receives the frame and matches the destination MAC address with its own MAC
- Host2 knows the frame is meant for it
- Host2 decapsulates the frame and extracts the original packet 
- Host2 matches the destination packet in the packet with its own
- Host2 sends back the ICMP echo reply!!



*****

# Layer 3 labs

**Commands**

- To make changes go into that port

**Router house keeping* **

|Command|description|
|-----|------|
|conf t||
|no ip domain-look||
|hos r2||
|line con 0||
|logg synch||
|no exec-timeout||


|Command|description|
|-----|------|
|do show ip interface brief|Look at all the router interfaces at the same time|
|ip address ?|Assigns an ip address|
|ip address 105.101.45.1 ?|Assign subnet mask|
|no shutdown|Brings a port up|
|do wr|save work|
|show ip arp|show arp cache or table|
|clear arp-cahe|clear arp cache|
|show interfaces fastEthernet0/0|shows details about an interface|
|debug ip icmp|takes internal processing of the router and puts it on the screeen. Don't use debug command in production|
|u(debug) all|turn off debug|
|debug ip packet||
|ping broadcast address|ping goes to everybody in the network|




*****

# Serial connections
How to bring up serial point to point links

- A router will have a serial connection to a CSUDSU(Termination point/ demarcation point for the ISP)
- The CSUDSU connects to the ISP Cloud and another CSUDSU on the other end connecting to the remote site router
- CSDSU is also called A DCE (Data connection Equimpment device)
- A router is considered a DTE(Data termination equipment device)
- CSUDSU provides clocking for the router(which is teh physical bit transfer rate between the CSDSU and the router)
- CSUDSU - Channel Service Unit, Data Service Unit
- CSUDSU provides these functions:
- CSUDSU is like a digital modem
> Clocking- physical bit transfer rate btetween two end devices(Local router and remote router)
> A DCU provides clocking
- show ip interface brief command has 3 fields
> method - layer 1
> protocol - layer 2

- Denoted with up or down, so up down or up up
- Layer 2 issues
> no  keepalive
> mismatch encapsulation
> no clock rate set on dce end

### Labs

- The default encapsulation type for a serial interface is High level data link layer control (HDLC)
- Serial interfaces do not have MAC addresses

**Commands**

|Command|description|
|-----|------|
|conf t||
|show ip interface brief||
|int serial 0/1/0||
|ip address x u| where x is the ip address and u is the subnet mask|
|no shh=|Brings the interface up|
|no exec-timeout||
|show controllers serial 0/0/0|show details about the serial|
|show running config|shows the running configuration|
|clock rate 128000|sets clock rate|
|encapsulation frame relay|changes encapsulation type|
|encapsulation hdlc|changes encapsulation type|
|no keepalive||


*****

# Ip routing theory

- Routing is the process of going from one broadcast domain to another
- Routing is a layer 3 function
- One layer 3 broadcast doman to anohter layer 3 broadcast domain
- A switch link within a diagram is one broadcast domain

![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/routing1.PNG)

- Host 1 wants to ping host 2
- Host 2 creates an ICMP(Internect Control messaging protocol) echo message with a source ip address of 10.10.10.1 and a destination address of 20.20.20.2
- Host 1 needs to create a frame for transmission over the local data link
- Remember layer 2 controls transmissions on the local data link
- Host 1 has its own MAC address
- It however does not have the MAC address of host 2
- Host 1 sends an ARP request requesting the MAC address of host 2
- Arp requests are broadcasts and cannot transverse a router by default
- Arp is a broadcast sent to the address 255.255.255.255 which is an all host broadcast address
- Arp request reaches router 1
- It does not know where 20.20.20.2 is because it is not directly connected to it
- \Since it is not a locally connected net, it replies back to host 1 with the MAC address resideing on f0/0 
- All routers run a protocol called proxy ARP on the internet interfaces
- So router 1 proxy's for host 2 and returns its own MAC address to host 1
- Host 1 creates a frame with source mac address, and destination mac address
- Host 1 creates the ethernet frame, encapsulates the original ICMP echo packetinside of the data portion of the packet and sends the frame over to R1
- R1 receives the frame and matches the destination address to its own address and decapsulates the frame
- Inside of each router, there is a table called the routing table, which has a listing of all remote destianations available to the router and how to gget to them
- Router needs to create another frame for transmission on the local data link between R1 and R2
- R1 encapsulates original echo packet in an htlc frame and pushes it out serial 0/0/0 because it discovered, after checking its ip routing table, that network 20.20.20.0/30 is available out serial 0/0/0 thats the route you take to the other network
- R2 receives the hdlc frame, deencapsulates it and extracts the original echo packet, then compares the destination ip address agains its ip routing table and discovers that the network is directly connected to fa 0/1
- R2 creates an ethernet frame for transmission on the local data link between R2 and host2
- If it does not know h2's mac address, it sends an ARP broadcast looking for the MAC address that belongs to the ip address 20.20.20.2
- H2 receives the broadcast and unicasts back a reply to R2
- R2 now has host 2's MAC address
- R2 creates an ethernet frame with source MAC being the MAC address of  the f0/1 interface and destination MAc being BBBB
- R2 pushes the frame to H2
- H2 matches the destination mac adddres in the frame with its own address
- h2, decapsulates the frame and extract the original packet, 
- Matches the destination address with its own address and if they match H2 will send back an echo reply

**What would be the destination mac address on the return frame from H@?**
the mac address of the f0/1 interface on R2
**How many times was the packet encapsulated between H! and H2?**
3
***What is the destination mac address as it leaves router one serial 0/0/0?***
There is no mac address in that frame*




*****

# Static routing

There are two typss of routing a router can perform

## Static routing
Manually entering routes to remote destinations in your router

|Command|description|
|-----|------|
|conf t||
|ip route (destination ip) (destination mask) (next hop ip address/exit interface of local router)(administrative distance)|- Next hop ip address is the ip address of the router immediate to you once traffic leaves your router, Adminsitrative distance is the trust worthiness of a routing protocol/ route (the lower administrative route the more trust)|





|Route| Admministrative distance|
|-----|------|
|Connected 0|0|
|static route|1|
|route information protocol(rip) route|120|
|Ennhanced interia gateway routing protocol(EIGRP)|90|
|Open shortest path first|110|

- Next hop ip address is the ip address of the router immediate to you once traffic leaves your router

### Lab

![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/SRL2.PNG)

Create a static routing table that routes from R1 to 10.10.254 and  20.20.20.254 networks
Put routes of the 10 and 20 networks on the routing table


|Command|description|
|-----|------|
|show ip route|show routing table|
|ctrl+shift+6|escape ping sezuence|
|debug ip pack|debugs|
|undebug all|turns off ip debuging|
|show ip address 0.10/1.10|ip interface of the interface|
|||
|||

**R 201**

- Always connect routes pointing out an exit interface when you are over a point to point link for example here its s0/0/1
- Administrative distance can run between 0 and 255
- Static routes by default have an andministrative route of 1
- U.U.U is an ICMP message(internet control messageing protocol)
**Since a route shows as directly corrected does it remain one or changes?**
ANS: remains at 1

- RIB Route information Base and Routing table are synonymous
- When creating routes that will leave a multi access interface(Fast ethernet) Always use the next hop router's ip address, not the exit interface
- 

|Command|description|
|-----|------|
|config t||
|ip route 10.10.10.0 255.255.255.0 150.101.45.2 1||
|ip route 20.20.20.20 255.255.255.0 s0/0/1 8 (use 150.101.45.2 instead of s0/0/1)||
|show running config||
|show ip route static|the output in [] indicates the addministrative distance|
|show running config|shows running config|
|traceroute|U can get the ips between onee source and one destination, every router that the trace passes through will send its ip address|
|debug ip icmp||
|debug ip packet||
|do ping address|executing the ping command from config t|
|ip route 150.101.45.3 255.255.255.255 s0/0/1||
|ip route 0.0.0.0 0.0.0.0 150.101.45.1|Gateway of last resort|
|do show ip route|show routing table|


- A route to a single address with an all 255 mask is called a host route because it is to a single host

## Dynamic routing
When two routers share remote networks/routes/ routes to remote destinations automatically by running programs called routing protocols on them.

### Distance Vector running protocols
- Posses some general qualities

> When a router is running a distance vector protocol, it sends teh contents of its whole routing table every set interval in routing updates
> Every 30 seconds, route information protocol is gonna send the contents of its whole routing table to all its directly connected neighboring devices
> This is not a good thing coz every 30 seconds the router next to you is getting hit by the info whether it needs it or not

- The DVRP send their routing updates to 255.255.255.255(All hosts, all networks, all subnets broadcast), not good coz every body on the network is going to hear this update whether or not they want. Unless there is a router to stop the broadcast(Broadcasts can't transverse a router)
- They use hop count as their metric(measure of distance between the local router and a remote destination/ destination network)
- Prone to routing loops because they route by rumor(the closer to the destination network you are, that is the source, it becomes supstream)
- The router doesn't actually know dets about the network
- Distance Vector Running protocols have an inbuilt loop prevention mechanisms

**Loop prevention**

* Maximum hop count
* Split horizon(if i send an update about a network outbound on an interface, I will not accept an inbound update about the same network coming in on that interface)
* Rule of route poisoning - advertise a down route with an infinite metric(rip is set to 15 is max hop count is 16)
* Route invalid timer(if a router does not hear from)- A lenght of time a router will wait to hear from an upstream router before declaring that route to be possibly down and stops any routing towards it
* Hold down timer - Router will not accept any updates about that route for that rate of time. When the route invalid timer has expired after 180seconds, hold down timer is started which is another 180seconds. While the route is in holder 
* Routers send poisoned updates upstream about a route being possibly down(poison reverse) while in hold down. Advertising a poisoned route back upstream towards the origin of the network with infinite/unreachable metric is called route poisoning.
* Rotue flush timer - time at which the route is completely remove from the ip routing table(120 seconds for rip). RIP Version 1 is classfull(only understands class A,B and C addressing hence subent mask info is **not carried within the routing update** )


### RIP configuration labs

- We are going to run rip between routers
- Static routes have administrative routes of 1 but dynamic have 120 so if static routes are still present dynamic ones will not start
- Network statement defines a range of ip addresses that when present, the interface on which that ip is sitting is included in the routing protocol
- The primary function /purpose is not to enables the router to send routing updates but to define a range of addresses which when present on the router, then the inteface on which that interface is present is included in the routing protocol 
- **Rip is a classfull routing protocol and subnet info is not sent in network updates**
- The right way to put an ip address in the rip is 150.101.0.0 and not 150.101.45.1 depending on the mask
- Default administrative distance for RIP is 2
- If 4 paths are available between a destination and your router, RIP version 1 can load balance across the links across verion 1 for up to 4 paths(equal cost paths)

|Command| Description|
|-----|------|
|router rip|start routing process on the router|
|network 200.200.200.0|network statement|
|do show ip interface brief||
|show ip route rip|rip specific routes|
|show ip protocols|check flash times and etc on the test|
|debug ip rip||
|version 2| change rip version|
|No auto summary|makes routing table reflect subnet info |
|no route rip|removes rip from router| 


- Rip version 2 is a classless routing protocol whcih means subnet mask info is sent in the routing updates
- Rip version 2 updates are sent to 223.0.0.9
- 

Route Information Protocol (RIP)(The only purte dvrp)
### Link state routing protocols


Automatically

# Enhanced Interior Gateway Routing Protocol
- Its an Advanced distance vector running protocol
- This is because EIGRP updates are non periodic, partial and bounded
> non-periodic - Only sends an update when there is a change in the topology
> partial - The contents of the whole routing table are not sent directly connected devices, only changes are sent to neighboring devices
> bounded - Changes are sent to only devices that need them hence efficients

- Updates are sent to the multicast address 224.0.0.10
- Since updates are periodic, EIGRP uses hello packets to keep the links alive
- An erigp packet has a hold time before a neighboring devicee is supposed to wait for me to send another hello packet before considering me time(hold time is usually 3 times the hello interval)
- For link speeds greater than t1 speeds(1544kbps), hellos are sent every 5 seconds
- For link speeds less than t1 speeds, the hold time is set to 30 seconds
- EIRGP stores all its routes in the topology table; even multiple routes to the same destiantion points(feasible successor points)
- Each route has an associated metric called the feasible distance
- The best of each of thse routes is plucked from the topology table and implanted into the ip routing table/ route information base and called a successor route.
- The best route will be the one with the lowest metric/ feasible distance 
- Reported/advertising distance - Feasible distance for your uplink distance(closer to the network) as reported to you
- Feasibility condition(also a loop prevention mechanism) - A routes reported distance must be less than the route's feasible distance for the route to be installed in the topology table as a successor route

![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/eigrp1.PNG)

calculate the feasible distance and reported distance 

|PATH|Feasibility distance|Reported distance|
|------|-----|-----|
|A|80|30|
|B|100|90|
|C|110|70|

- So path A becomes the **feasible successor route**
- If the successor route fails, the next best feasible successor which is path C becomes the beast feasible successor which helps which convergence coz alternate paths to the same destination already exists in the topology table



- - -

**EIRGP feasible distance

**



- EIRGP uses feasible distance as its metric



![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/eigrpFormula.PNG)



> Load - current traffic on the link

> Delay - delay a packet will incur while transversing that link

> Reliability - how many times in the past hour the link has failed and come back up

> BandWidt



- If k5 is 0, ignore that half part of the formula

- K values range between 0-255

- K is a knob that u can turn (like a weight)

- If default values are being used, the formula reduces to:



> (BW + Delay)256



**EIRGP variance

**



- EIRGP can send equal amounts of traffic over multiple links if the metrics match(equal cost load sharing)

- EIRGP can also do unequal cost load sharing through a concept called variance

- Variance is the multiplier for the fasible distance/ metric of a successor route in the routing table

- Any route in the topology table with the metric/ feasible distance less than the product of the feasible distance of the successor route and the variance is also installed in the route info base/routing table

- The feasible distanc default is q and can range btwn 1 and 128



![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/variance%20eigrp.PNG)



- Both paths here have the feasibility condition

- Both routes get installed in the topology table

- The top path goes to the routing table for you because it has a less total distance

- Since variance is set to 1 by default, the top route will be the only one headed to the routing table

- Bottom route sits in the topology table because it is a feasible successor

- However for unequal cost sharing, one can add the bottom link to the routing table by picking a variance..eg 2



> FB = 15

> V = 2

> 15*2=30



- If variance is set to 2, any feasible successor route that has a feasible distance less than 30 will also get installed in the routing table





**EIGRP lab

**



- EIRGP is classless - does send subnetting information in its routing updates



|command|description|

|------|------|

|router eigrp someNo|enable routing protocol|

|network x.x.x.x wild card||





- Getting wildcards:



![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/wildCardBitsEIGRP.PNG)



- In a wild card..an on bit is i do not car andd vice versa



** inc...review **



## Eigrp manual sumarization



- 3 networks exist in our topology,



![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/eirgpManualSum.PNG)



- A network engineering tells you to stop cluttering their routing table with all the three networks and summarize them into one address

- Look at an octed that is different in all that network

- The last octed is different



![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/eigrpSum1.PNG)



- The 1s match up 

- So the rummarized network address would be 30.10.8.0

- the mask is going to change to 255.255.248.0 /21



![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/eirgpsum2.PNG)



- Loop back interfaces - virtual interfaces on the router



|command|description|

|-----|------|

|interface loopback 8| creates a loop back interface|

|ip address 30.10.80.0 255.255.255.0/24|assigns an ip address to the interface|

|shutdown|shuts down an interface|

|router eirgp 100||

|netwfork 30.10.0.0.0.0||



- An off bit in a wild card is a care bit (match it completely)



- Loopback interfaces are up by default







# Open shortest path first (Link state routing protocol)



- A routing protocol

- Not a distance routing protocol

- Routing updates are not sent every set intervals or when the topology changes like in eigrp and rip

- Each router in ospf upon initialization defines itself in packets called linked state advertisment whcich contains:

> Routers' links/ interfaces (such as a serial )

> Ip networks attached on that link (eg 200.0.0.0/30)

> The metric to get to that network



- each router floods the lsa's through out the topology

- At the end of the flooding process each router has an LSA from every other router and builds a database of all these LSA's called a link statte databas built on every router. The link state database on one router looks exactly like the one on other routers

- After the lsdatabase has been built, the shrotest first algorithm is run over the link state database and each router independently calcualates routes to remote destination and puts them in the rib(route information base)

- thats the difference between ospf and eirgp(rumor approach) because it independently calculates route and puts it in the ** rib**

- ospf independently the route to remote destinations

- When two ospf routers first come up, they send each other all their lsa's and synchronize their databases with each other and set to be adjacent/neighboring each other

- The neighbors are kept in touch through hello message like the eigrp/ the link is kept alive through hello messages

- The hello message cntains the dead timer inside of it (amount of time im going to wait for the neighboring router to send a hello before considering it down)

- The dead timer is set by default to 4 times the hello timer

- Hellos are sent every 30 seconds over non broadcast multi access networks like **frame relays**

- Hellos are sent to the multicast address 224.0.0.5

- Certain fields in the hello packet must match for two routers to become ospf neighbors

-

> ip subnet and subnet mask of other interface that is talking to the other neighbor

> Authentication information (for adjacency to form between two ospf neighbors), both sides must have authentication passwords

> Heallo and dead timers must also  match

> Area id must match



- Each router picks for itself out of all ip addresses available on the router an router id(an identifier for the router)

- The  router will prefer the router id if configured with the router id command

- Else the highest configured loopback ip if the router ip command is not run; else highest physical address





>loop back 1000

>1.1.1.1 /32

>loop 50

>loop back 150.150.150/32

>150.150.150/32 will become the router router id automatically because it doesnt matter what the loop back iterface is but what the ip address is 





- over multi access network, if every router became neighbours with each other, you will have alot of adjacency.



> 2(n-1) neighbour relationships where n is the number of routers



- As the number of routers go up, the adjacency increases and this is way too much overhead

- Multi access networks elect a router called a dr or a designated router/ a back up destinated dr and every router becomes adgacent with the dr and the bdr

- A designated router is elected according to the ospf router priority

- All routers have a priority value of 1

- The higher the priority the better

- The highest priority router becomes the dr

- Priority 0 routers do not participoate in designated router and back up designated router election

- If everyones priority is 1 by default, the router whith the highest router id becomes the designated router

- However in real networks it doesn't really work that way because you are one person so the routere you configure first sets itself a dr then you have to go change it yourself

- Dr other routesrs are other routers that are not the designated routers. They send their LSA"s in update packets to the multicast address 224.0.0.6

- The only routers listening to this address are the dr and the bdr(back up designated routers)

- The drs reflect these LSA's back to  to eery one else over 224.0.0.5



# OSPF neighbor states



- Hello fields you should know

> Router id of the router originatint the hello

> Hello(how often i send hellos) and dead timer(how long should i wait to hear from a neighboring router before considering it down/dead)
> All your neighbors router ids(to be contained in hello messages ur sending)
> Area id of the originating interface
> Router priority(by default is 1 )- **The router with the highest priority becomes dr**
> The dr ip address
> The back up dr ip address
> Any authentication information if present.


- After routers exchange this info with hellos, they become neighbors and initiate the link state database eschange which happens in 7 steps
- Two ospf neighbors start in the down state(router has received hello from the other end)
- Rotuere transition to the attempt state(neighbors must be configured maually with the neighbor command)
- Init state(hello packet has been received from the opposite side)
- 2 way state( have received a hello packet from my neighbor with my own router id in that hello)
- Exstart state- routers prepare for link state synchronization by exchanging packets called database description package; the router with the highest router id amongst all becomes the master router and controls the database exchange with the other routers.
- Exchange state - DD/ Database description, link state request and updatae packets are used to exchange the link state database between two or more packets
- Loading state - Link state request packets are sent requesting missing link state advertisement that might have not reache me yet but are in your link state database; this link state request packets are responded to by link state update packages containing these LSAs
- Dull adjacency state - All databases are synchronized 


# OSPF areas and LSA types

- A router that borders area 0 and another area is called an area border router(ABR)
- A router that takes us out of our network and into another is called an autonomous system boundary network
- Area internal routers are internal to just one area

**LSA TYPES**

- ** Router LSA** - Describtes the router links, the ip networks connected to those links, the neighboring routers and the cost/ metric to those routers
- The** network LSA** is only produced by the dr of those networks(to describe the ip address of the network and all attached routers by their network ids)
- **Network summary LSAs** - Produced by ABRs(takes the ip network from one areaa and injects it into another area)
- **Atonomous System Boundary Router Summary LSA** - Produced by the =ABRs and injected into non backbone areas/ non transit. Points to the location of the ASBR- System router
- ** External LSA** - carries all external networks to your OSPF domain


# TrANSPORT LAYER

- Controls communication between end devices / host
- It can either be reliable or unreliable
- TCP provides for this reliable communication/service by sending data then expecting an acknowledgment for this data and retrying 
- PDU at layer 2 is called a segment
- Addressing scheme - **ports**
- Ports 1-1023
> Telnet - TCP port 23

- 1024-49151 - Registerd ports with IANA (designated for companies
- 49152-65535 -  open/ Ephemeral used by any protocols or servers
- When you add ports to a packet, it is called a segment.

![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/layer4Segment.PNG)

- Before the segments are sent between devices/ reliable communication can happen, the devices create a virtual connection with each other by going through a 3 way handshake

![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/3wayhandshake.PNG)

> H1 sends H2 a segment with the synchronized bit turn on(syn segment)
> H2 replies with an acknowledment with a sync/Ack
> H1 sennds back an acknowledment acknoqledging the sync/ack

- THen a virtual connection is built btwn the 2 end devices, then data transfer may begin
- For every response, an acknowledgemt is expected, else the segmennt is resent
- The number of segments that can be sent per data flow without receiving an acknowledgment back is called a window size which is 1 by default
- The window size can increase

## Access control lists

- Controls traffic passing through/to the router
- Have the ability to permit/deny certain traffic
- Entries in the Access control lists are read from top to bottom sequentially
- Once created has its last entry as an implicit deny any entry/deny all

### Standard Access control lists

- Can permit and deny traffic only based on the source address

### Named Access control lists

### Extended Access List

### Named Extended Access List
 
- - -
## User Datagram protocol

- Unlike TCP, udp does connectionless/ unreliable transport
- Seglments are sent and there are no acknowledgements expected for sent segments without expectation
- Rip protocol uses udp port 520 and does not expect an acknowledgement everytime it sends out its routing table? Because its going to resend its routing table anyways every 30 seconds

## Rapid spanning tree protocol(802.1w)

- The IEEE designation for RSTP is 802.1w
- Spanning tree takes a total of 50 seconds to converge to go from blocking to forwarding
- Rapid spanning tree protocol minimizes this

- Ports upon power up are put in the diocarding state(when spanning tree has its port in the blocking state)


## Network address translation

- Process of translating/ converting a private ip address to a public ip address
- Private ip address - (as defined by International Engineering Task Force) as described in the article RFC(request for comments)1918 IEEE documents that define standards and protocols in the it community. Describes the ranges of addresses not allowed on the internet.
- Companies/addresses are allowed to use this addresses within their environs and when they need to transfer traffic to the internet, they need to convert to a public ip address

![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/Network%20address%20translation.PNG)

## static NAT


# Point to point protocol

- LAYER 2 encapsulation trype
- Default encapsulation type on a serial interface is HDLC (High level data link control)
- PpP is an open standard, so u could connect a diff router to another
- Uses authentication to make sure the person at the other end of the link is who they say they are
- Can also do comproession on your data or data headers
- Compression- large chunk of data and take redundant values within that data and use set numbers for those values and turn a larger chunk of data into a smaller chunk of data
- PPP has a ppp multi link feature where pp can look at multiple physical links as one logical pipe

### LCP - Link Control Protocol

- Controls the link establishment protocol of ppp
- After the link is established, ppp can negotiate multiple layer 3 routed protocol
- ip is a routed protocol; not a routed protocol. It is what is carried in routing protocols
- The function of ppp to carry diff routed protocols  is controlled by a sub protocol called NEtwork control protocol 
- Internet Protocol control protocl is a Network Control Protocol that enables ppp to carry ip information

# CHAP - Challenge handshake authentication protocol
- Chap sends a message digest 5 md5 of the original password over the link and will never be exchanged over that link so both sides must have a database to begin with.
- The original password/cleartext password is never sent over the link

# Cisco discovery protocol

- A layer two protocol used to map out your network

# Frame relay

- Non Broad Cast Multi access technology(NBMA)
- ethernet is a multi access technology
- Frame relay supports no MORE THAN TWO DEVICES BEING ON THE NETWORK AT THE SAME TIME, THERE IS HOWEVER NO lAYER 2 FRAM RELAY DESTINATION BROADCAST ADDRESS
- In ethernet a destination broadcast address is all left

![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/frameRelayPic.PNG)

- The CE on top stands for customer edge
- PE router/ first frame relay switch(router with special configuration) is the Provider Edge router
- Frame relay cloud is a collection of frame relay cloud(collection of frame relay switchs that isfp has done the groundwork connected to each other in a full mesh/almost full mesh)
- A circuit between two virtual circuit is called a **permanent vritual circuit(pvc)**
- All traffic between london and Paris must pass through Dc - The topology is called a hub unspoike topology
- Instead of paying for an extra circuit between london and paris through dc
- FC being the hub
- London and paris being unspoke
- Data link connection Identifier seperates the two circuits (DLCI)
- A dlci is a near to address for frame relay to seperate pvcs from each other
- DLCI's are locally significant (just betweeen dc and first frame relay)
- If the encapsulation type changes from PBC or HDLC, to relay, the DC router starts sending and receiveing LMIs(LOCAL MANAGEMENT Interfaces)
- LMI's are used for two purposes
> Anounce all your DLCIs to you(but u still gotta call ur providers to know ur DLCI)
> Report the end to end circuit health
> 

- LMIs are sent and received every ten seconds(customer and provider edge)
- As soon as an ip interface is set, an invers arp is sent down the circuit/pbc to retrieve and resolve the ip address of the other end of the circuit
- An arp resolves a remote ip to the mac address associated to that ip address at the end of the link
- An erp arp resolves locally received dlci to the remote at the other end
- Once you assign an ip to an interface, an inverse arp request is send down to resolve the ip at the other end(layer 2 to layer 3 mapping) only this is called an inverse arp

## Types of relay interfaces

**Multipoint interfaces**(always send erp arp requests)

**Sub interfaces
** <br>Multipoint and point point
They do not send inverse arp requests by default; you will have to do something manyally for that to work


- - -


# IPV6

- An ip address is a 128 bit address written in 8 fields of 16 bits each seperated by a colon
- Each hex character is 4 bits
- 

## Rules for shortening ipv6 addresses

- Leading zeros may be omitted in a field
- Successive fields of all zeros may be represented by a double collon but only once


![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/ipv6%20address.PNG)

## ipv6 subnet mask

- Only represented in the slash format or slider notation 
- Subnet mask is called the fprefix because whch equates the network address since it tells you how many bits in the address belongs to the network.

![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/ipv6%20subnet%20mask.PNG)

## ipv6 eui address format

- Ipv6 has the ability to create an ipv6 address automatically given the mac address of a host(stateless autoconfiguration)
- If you gave ipv6 a mac address and a64 bit network address or a 64 prefix, it can auto create an ipv6 address by inserting a mac address into the ipv6 address

## ipv6 neighbor discovery protocol

- uses icmp protocol v6 for discovering neighbors on the local data link for directly attached devices

- Functions
> mAC address to ipv6 address resolutions

## Hot standby routing protocol

theswe are first hop redundancy protocols

- Cisco propriety protocol
- Gate way load balancing protocol


# Router boot sequence

- The router perfoms a Power On Self Test (POST) to verify/evaluate if all hardware is functioning accordingly
- A ptogram in rom called bootstrap looks for the os/internet os (defaultly stored in flush) then loads it
- The ios is expanded into ram and the startup config sitting in nvram is loaded
- Router looks for any valid config that it may have in nvram then loads it nvram is loaded into run as the running config
- If startup config is not present in 3, the router will broadcast every ARP interface and start looking for a tftp server
- If ftp server is not found, router goes into initial configuration dialogue