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
|||
|||
|||
|||
|||
|||
|||



