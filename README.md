<h1>Active Directory Home Lab With Bulk User Creation</h1>

<h2>Description</h2>
This project is a walkthrough of how I created an Active Directory home lab Environment using VirtualBox. I set up a Microsoft Server to run Active Directory on it. I then configure a Domain Controller that will allow me to run a domain. After that I ran a Powershell script to create over 1000 users in Active Directory and proceed to log into those newly created accounts on another client that uses the domain I set up to connect to the internet. This lab simulates a business environment. In this lab I'll need a Microsoft Server 2019 ISO, A Windows 10 Enterprise ISO, VMWare and a Powershell script. 
<br />

<h2>Languages and Utilities Used</h2>

- <b>Active Directory</b> 
- <b>PowerShell</b>
- <b>CMD</b>

<h2>Environments Used </h2>

- <b>Oracle VM VirtualBox</b>
- <b>Microsoft Server 2019</b>
- <b>Windows 10</b> (21H2)

<h2 align="center">Project walk-through</h2>

<p align="center">
<b>The network diagram I'll be using for this project</b> <br/> <br />
<img height="80%" width="80%" alt="Network_Diagram" src="https://user-images.githubusercontent.com/117952272/206298370-d6be8abf-e0f5-45fb-bcbe-f0be332a7cff.png">
<br />
<br />
<b>I created in VirtualBox the first Virtual Machine for the Server 2019 and named it DC for Domain Controller.</b> <br/><br />
<img src="https://user-images.githubusercontent.com/117952272/206299795-86d59fd5-e101-4de8-96fd-722e1c794e86.png" height="80%" width="80%" alt="The first Virtual Machine for the Server 2019"/>
<br />
<br />
<br/>
<br />
<b>According to our network diagram we need two Network adapters.</b>
<b>We set Network adapter 1 as NAT which will connect to the home network.</b> <br/><br />
<img src="https://user-images.githubusercontent.com/117952272/206301688-eec8da11-6993-4929-864f-be5360b48158.png" height="80%" width="80%" alt="Network Adapter 1"/>
<br />
<br />
<br/>
<br />
<br />
<br/>
<br />
<b>Here we set up the second Network Adapter that is dedicated to the internal virtual network.</b> <br/><br />
<img src="https://user-images.githubusercontent.com/117952272/206302580-16ceda9c-3450-473d-86bd-16b207de09c0.png" height="80%" width="80%" alt="Network Adapter 2"/>
<br />
<br />

<br />
<b>We installed Windows Server 2019 and created an Administrator account and a password for the lab purpose.</b> <br/><br />

https://user-images.githubusercontent.com/117952272/206575393-77ad8ac5-56b7-42bc-b599-9950a827c64a.mp4

<br />
<br />
<br/>
  <b>To improve overall VM usability we installed VirtualBox VM Guest Edition</b><br/><br />

https://user-images.githubusercontent.com/117952272/206577016-f6435850-780a-43fd-bd60-c195d3fcf7ef.mp4

<br />
<br />
<br/>
  <b>Here we will see which of the two adapters is an Internal NIC and which one is External NIC.</b><br /><br />
<img height="80%" width="80%" alt="NIC Adapters" src="https://user-images.githubusercontent.com/117952272/206579161-6e95da1f-f01f-4b34-a7b7-645e255b2648.png">

<br />
<br />
<br/>
<b>This is the Ethernet2 NIC status states that the following network adapter is connected to the internet through ATT DNS server and has the IPv4 address of 10.0.2.15<b><br /><br />
<img height="80%" width="80%" alt="Ethernet2 NIC" src="https://user-images.githubusercontent.com/117952272/206580367-a306617c-c1ae-43d3-a093-a7089d3f4dc2.png">
<br />
<br />
<br/>
<b>This is the Ethernet NIC status states that the following network adapter was looking for a DHCP server and couldn’t find one and was assigned an automatic internal address of 169.254.59.157</b><br /><br />
  
<img height="80%" width="80%" alt="Ethernet NIC" src="https://user-images.githubusercontent.com/117952272/206581038-f304de97-60d5-4f80-bd90-2e506dc582d1.png">



