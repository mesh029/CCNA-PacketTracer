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

Automatically