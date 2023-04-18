# packet tracer

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
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||

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

- Simplty mode on

Sets the local port to trunking unconditionally
Will send and respond to DTP frames











