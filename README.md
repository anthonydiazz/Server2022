# IT Infrastructure : Windows 2022 Domain Setup
This lab project demonstrates the end-to-end setup of a virtualized IT infrastructure using Windows Server 2022 in VirtualBox. The project simulates a real-world enterprise environment by implementing domain services, DHCP, remote access, and user management through a Helpdesk structure

The environment consists of:

- A Windows Server 2022 VM acting as a domain controller, DHCP server, and router

- Two Organizational Units (IT and Finance)

- Two domain users (Helpdesk and Bruce Wayne)

- Two Windows 10 client machines joined to the domain

- Use of RSAT tools for remote helpdesk operations and GPO enforcement

##  Part 1: Setting up the Windows Server 2022 VM

### Step 1: Create the Server VM in VirtualBox and Configure Network Adapters 
- Download the Windows Server 2022 ISO and create a new VM in VirtualBox
- Assign at least
   - 2 CPUs,
   - 4GB RAM,
   - 60GB disk space (dynamically allocated)

### Step 2: Setting Up Network Adapters

#### Step 2.1: Set Adapter 1 (Internet Access)

Purpose - Is to provide internet access to the Server

![Install Requests](./ad_prj/part1.png)


#### Step 2.2: Set Adapter 2 (Internal Network) 

Purpose - Provides LAN connectivity between Server and Client VMs

![Install Requests](./ad_prj/part2.png)


### Step 3 : Assigning Static IP to Internal Adapter

- Go to Control Pannel > Network Connections > 
- Set a Static IP on the Internal Network Adapter:
  
     - IP Address: 192.168.0.1
     - Subnet Mask: 255.255.255.0
     - Default Gateway: Leave Empty
     - Preferred DNS: 127.0.0.1

- This will enable communication with user VMs

![Install Requests](./ad_prj/x_internal.png)


### Step 4 : Install Server Roles 

The main purpose of this Server is for it to act as a router, dhcp server , and domain setup for anthonytech.com

- Open Server Manager and Install the following roles:
  
    - Active Directory
    - DHCP Server
    - Remote Access

#### Step 4.1 - Installing Active Directory

![Install Requests](./ad_prj/activedirectorydownload.png)

Once Installed You will then have to create your domain which in this case mine is anthonytech.com 

![Install Requests](./ad_prj/creatingdomain.png)

To verify that you have installed AD, you can type on the Search bar for Windows administrative tools and it should be in that folder 

![Install Requests](./ad_prj/ADinstalled.png)



#### Step 4.2 - Installing and Configuring Remote Access 

Add the Direct Access and VPN(RAS) role service 

![Install Requests](./ad_prj/RASinstalaltion.png)


Use the Routing and Remote Access (RRAS) wizard to configure NAT routing

![Install Requests](./ad_prj/configurenat.png)


#### Step 4.3 - Installing and Configuring DHCP 

Add the DHCP Server role and tools 
![Install Requests](./ad_prj/installDHCP.png)



![Install Requests](./ad_prj/setupDHCP.png)

Start IP:       192.168.0.100
End IP:         192.168.0.200
Subnet Mask:    255.255.255.0
Default Gateway:192.168.0.1
DNS Server:     192.168.0.1
Domain:         anthonytech.com
Exclusions:     192.168.0.100 - 192.168.0.110
Lease Duration: 7 days


![Install Requests](./ad_prj/iprange.png)



![Install Requests](./ad_prj/DHCPexclusions.png)



![Install Requests](./ad_prj/DG.png)




![Install Requests](./ad_prj/DNS.png)



![Install Requests](./ad_prj/LeastDuration.png)



![Install Requests](./ad_prj/Authorize.png)



![Install Requests](./ad_prj/DHCPactivated.png)



## To Conclude Part 1 > The following infrastructure is in place: 

By the end of Part 1, the following infrastructure is in place:

- Server 2022 VM with dual network adapters

- Static internal IP configured (192.168.0.1)

- AD, DHCP, and RAS roles installed

- Domain created: anthonytech.com

- DHCP scope configured and authorized

- Clients will be able to connect internally and reach the internet through the server




