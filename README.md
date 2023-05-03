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

|Command	|Description|
| ----------- | ----------- |
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

> #Steps for the Spanning Tree Protocol to Converge
> > 1. Elect one root bridge per layer 2 domain/ elect one designated port per segment
> > - Elect one switch to be a root bridge
> > 2. Elect a root port per non root switch
> > - For the others, we elect a root port
> > 3. Elect one designated port per segment
> > - A segment is a link between two switches



> #Spanning tree decision process
> >### i) Lowest bridge ID
> >### ii) Lowest path cost
> >Route port election per non root switch
> > > - Only happens on non root switches
> > > - Happens according to Root PAth Cost
> > > >Root path cost - This is the distance for each link speed
> >|SPEED|Root Path Cost|
> >|-----------|--------------|
> >|10mb/s| 100 |
> >> >|100mb/s| 19 |
> >|1000mb/s| 4 |
> > - Btw...FastEthernet - Path cost = 19 and the root switch is the only one sending BPDUs
> > - The root path cost inside of a BPDu is incremented when a BPDU enters a switch not when it leaves a switch
> > - So Root Path Cost starts at zero
> > - Lowest Root Path Cost is elected

> > > - 

> >### ii) Lowest sender bridge ID
> > - When the route path costs are equivalent, the switch has got no choice but to move to the next step in spanning tree decision process
> > - The sender bridge ID, is the bridge ID of the switch sending the BPDU.
> > - Switch compares the sender bridge ID, then selects the one with the lower bridge ID. I.e, a switch withe the MAC address BBBB will be selected over one with the MAC Address CCCC
> > - if there are two or more ports with the same sender bridge ID, then the switch moves to the last step of the spanning tree decision process

> >### ii) Lowest sender port ID
> > Id of the sending switch
> > The port with the lowest sender port ID becomes the root port


> > > 



When switches power up they imediately start sending frames to each other out of all ports called BPDU's
- BPDU's havefour fields
> ### i) Route bridge id
> > Priority field + MAC address
> > | |MAC ADDRESS|PRIORITY FIELD|
> >  |-----------|--------------|
> > |BITS|48|16|
> > |^ 2||65536|
> > |RANGE|48|0-65535|
> > |SWITCH SETTINGS ID BRIDGE ID||32768|
> >- Switch with the lowest MAC Address becomes the route because the switch with the loweest bridge
> >- Each switch initially announces itself as the root and sets the Root Bridge ID field id in the BPDU equal to the its Sender ID field
> >- When a switch recievesa a BPDU from another switch with a better Bridge ID(lower bridge ID) It stops sending its own BPDU and starts relaying superior BPDU's
> >- Given enough time, the switch with the lowest Bridge ID(In this case one with the lowest MAC address) becomes the root switch
> - So switch A becomes root and continues sending BPDUs and every other switch relaying BPDUs sent by the root switch
>
> ### ii) Route path crossed
> ### iii) Sender bridge id
> Id of the sending switch
> ### iv) Sender port id
> Id of the sending switch

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



$## Per VLAN spanning tree protocol PVST

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
|||
|||
|||
|||
|||
### Spanning tree enhancements

- Takes 50 seconds for spanning trees to converge and put the ports from blocking to forwarding
- Port fast feature - Port skips all transition states and immediately jumps to forwarding
- BPDU guard frature - used in conjunction with the port fast feature (One with malicious intent can replace your switch with one of theirs and get traffic info) As soon as BPDU guard feature is enabled on port 3 say...as soon as port 3 receives a BPDU from unknown switch, it will be shut down

- ROUTERS DO NOT UNDERSTAND BPDUs
- Switch ports that have routers connected to them can have port fast feature enabled since they don't need to wait for the spanning tree protocol to complete so they can start communicating]
- Switch ports by default are disabled...ports on routers, however, are in administratively down mode
- 

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
 > ### VTP Server mode
 > The Server switch can modify its vlan.dat
 > - modifications include: 
 > > - Adding a vlan
 > > - Deleting a vlan
 > > - Renaming a vlan
 > > - Changing a vlan's mtu(maximum transmision unit(default = 1500bytes))

 > The modifications are carried downstream from the server swtich in VTP advertisemends
 
 >### VTP client mode
 > - The client switch will listen to this modifications sent by the server switch and do so accordingly
 > - The client switch however is not allowed to edit the vlan.dat
 
 > ### VTP transparent mode
 > - The VTP transparent mode switch will relay VTP advertisments but won't comply with the server switche's demands
 > - The switch will however foward VTP advertisements to downstream clients
 > Can modify its vlan.dat file
 > > - Can add its own vlans
 > > - Can delete its own vlans
 > > - Change the vlan mtu
 > > - Change the vlane name
- 

### Lab on vlan trunking protocol
- By default, all switches are VTP server switches
- All network, if ur using DTP, must be in the same domain else switches wont communicate
- Configuration revision - how many changes have been made to vlan.dat file
- A vtp transparent switch has its configuration revision set to zero because it is a count of the modifications made by the server switch to the vlan.dat file
- A transparent switch does not participate in vtp. It only relays vtp information.
- VTP version 2 supports token ring VLANs 1 does not support token ring


| Command     | Description |
| ----------- | ----------- |
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
|||

# Network layer (Layer 3)
Network layer controlls communication between broadcast domains
- You will need layer 3 to move from one broadcast domain to another
- You will need a router in layer 3
- Routing is a layer 3 function
- Sends data between broadcast domains
- The pdu(protocol data unit) at layer 3 is called a packet

## Layer 3 addressing scheme

- The addressing scheme at layer 2 are MAC addresses
- Addressing scheme = ip addresses

### Ip addresses
- 32  bits in length 
- written in 4 fields of 8 bits each seperated by a dot(dotted decimal format)
- Each of the octects can range between 0-255
- Each bit in the octed can be turned on (1) or off (0)

 ![](https://github.com/mesh029/CCNA-PacketTracer/blob/main/images/octed.PNG)




