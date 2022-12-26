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
<img width="1677" alt="Network_Diagram" src="https://user-images.githubusercontent.com/117952272/206298370-d6be8abf-e0f5-45fb-bcbe-f0be332a7cff.png">
<br />
<br />
<b>I created in VirtualBox the first Virtual Machine for the Server 2019 and named it DC for Domain Controller.</b> <br/><br />
<img src="https://user-images.githubusercontent.com/117952272/206299795-86d59fd5-e101-4de8-96fd-722e1c794e86.png" width="1677" alt="The first Virtual Machine for the Server 2019"/>
<br />
<br />
<br/>
<br />
<b>According to our network diagram we need two Network adapters.</b>
<b>We set Network adapter 1 as NAT which will connect to the home network.</b> <br/><br />
<img src="https://user-images.githubusercontent.com/117952272/206301688-eec8da11-6993-4929-864f-be5360b48158.png" width="1677" alt="Network Adapter 1"/>
<br />
<br />
<br/>
<b>Here we set up the second Network Adapter that is dedicated to the internal virtual network.</b> <br/><br />
<img src="https://user-images.githubusercontent.com/117952272/206302580-16ceda9c-3450-473d-86bd-16b207de09c0.png" width="1677" alt="Network Adapter 2"/>
<br />
<br />

<br />
<b>We installed Windows Server 2019 and created an Administrator account and a password for the lab purpose.</b> <br/><br />


https://user-images.githubusercontent.com/117952272/209251268-f0754ef1-4830-4493-a39d-e914a5acf7fe.mp4


<br />
<br />
<br/>
  <b>To improve overall VM usability we installed VirtualBox VM Guest Edition</b><br/><br />

https://user-images.githubusercontent.com/117952272/206577016-f6435850-780a-43fd-bd60-c195d3fcf7ef.mp4

<br />
<br />
<br/>
  <b>Here we will see which of the two adapters is an Internal NIC and which one is External NIC.</b><br /><br />
<img width="1677" alt="NIC Adapters" src="https://user-images.githubusercontent.com/117952272/206579161-6e95da1f-f01f-4b34-a7b7-645e255b2648.png">

<br />
<br />
<br/>
<b>This is the Ethernet2 NIC status states that the following network adapter is connected to the internet through ATT DNS server and has the IPv4 address of 10.0.2.15<b><br /><br />
<img width="1677" alt="Ethernet2 NIC" src="https://user-images.githubusercontent.com/117952272/206580367-a306617c-c1ae-43d3-a093-a7089d3f4dc2.png">
<br />
<br />
<br/>
<b>This is the Ethernet NIC status states that the following network adapter was looking for a DHCP server and couldn’t find one and was assigned an automatic internal address of 169.254.59.157</b><br /><br /> 
<img width="1677" alt="Ethernet NIC" src="https://user-images.githubusercontent.com/117952272/206581038-f304de97-60d5-4f80-bd90-2e506dc582d1.png">
<br />
<br />
<br/>
<b>I renamed the adapters so it’s easier to tell which one is which during the DC and DHCP set up.</b><br /><br />
<img width="1677" alt="Renamed NIC Adapters" src="https://user-images.githubusercontent.com/117952272/206582327-b3be7895-a334-4d5b-9c18-ece55429c907.png">
<br />
<br />
<br/>
<b>Now we configure the internal network adapter according to our network diagram and assign it with the IP address of 172.16.0.1. We do not need to provide a default gateway since the Domain Controller is the gateway. Instead of using a DNS server address we assigned the preferred DNS Server with the loopback address since when we install Active Directory it automatically installs DNS so this server will use itself as a DNS.</b><br /><br /> 
<img width="1677" alt="Internal NIC Config" src="https://user-images.githubusercontent.com/117952272/206583052-9334381e-9f41-4570-be52-34fa17410fb3.png">
<br />
<br />
<br/>
<b>In the System Settings we gave the PC a proper name as DC which stands for Domain Controller.</b><br /> <br /> 
<img width="1677" alt="Renamed PC to DC" src="https://user-images.githubusercontent.com/117952272/206584207-c9f3ba90-3654-427b-b97f-5ded6bc41f38.png">
<br />
<br />
<br/>
<b>After we renamed the PC we pursued to install the Active Directory.</b><br /><br />  
  
https://user-images.githubusercontent.com/117952272/206587478-7639ba7b-91f5-44ff-bcef-0c548a912ad2.mp4

<br />
<br />
<br/>
<b>After the Server was promoted to a Domain and it restarted we could see the Administrator account has MYDOMAIN in from of it and the installation was successful.</b><br /> <br />   
<img width="1677" alt="MyDomain" src="https://user-images.githubusercontent.com/117952272/206784055-16226ca3-5e83-4a8b-8e70-9b5e33a99c3f.png">
<br />
<br />
<br/>
<b>Here we have build a new dedicated Admin account in the Active Directory.</b><br /> <br />   
  
  
https://user-images.githubusercontent.com/117952272/206786470-e9a4b41e-151d-4ae6-a595-59b22d1e53d9.mp4

<br />
<br />
<br/>
<b>Next step will be installing and configuring RAS (Remote Access Server) / NAT (Network Address Translation)</b><br /><br />  


https://user-images.githubusercontent.com/117952272/206788909-38954410-5767-44ea-beca-29464531056a.mp4

<br />
<br />
<br/>
<b>After adding roles and features we will continue with configuration of the Routing and Remote Access.</b><br /> <br /> 

https://user-images.githubusercontent.com/117952272/207141743-908d7ca1-7782-42b0-be6c-e167c5364db2.mp4

<br />
<br />
<br/>
<b>Configuration of the Remote Access and Routing is done now is time to install DHCP Server. This will allow Windows 10 client to be assigned IP address and browse the internet.</b><br /> <br /> 

https://user-images.githubusercontent.com/117952272/207143661-c7fd8928-1c22-4aa3-8c06-5df389b3b92c.mp4

<br />
<br />
<br/>
<b>DHCP was installed successfully, now is time to configure it and setup a scope.  Dynamic Host Configuration Protocol (DHCP) is a protocol that automatically provides to a host an IP address and other related information like the subnet mask and gateway.  The scope that we will create will allow the DHCP server to assign Ip addresses from a specifically defined range in our case it will be from 172.16.0.100 to 172.16.0.200.</b><br /> <br /> 
  
https://user-images.githubusercontent.com/117952272/207146606-368598ee-b261-4115-8bf0-f85dd6e45bfa.mp4

<br />
<br />
<br/>
<b>Domain Controller and Active Directory is now configured. Next we will run a PowerShell script to create over 1000 user accounts. First, we have to update the PowerShell execution policy so we are able to run the script.</b><br /> <br />

<img width="1677" alt="Powershell Policy Update" src="https://user-images.githubusercontent.com/117952272/207148832-639638a8-dbc7-4077-859a-4bdb25259d91.png">

<br />
<br />
<br/>
<b>We run the script below and created over 1000 Active Directory users.</b><br /> <br />



https://user-images.githubusercontent.com/117952272/207984392-f114d1d5-2660-4508-bd11-30d59e6a8ec4.mp4

<br />
<br />
<br/>
<b>We are setting up a Windows 10 Virtual Machine in Oracle VirtualBox.</b><br /> <br />
<img width="1677" alt="WIN10 INSTAL" src="https://user-images.githubusercontent.com/117952272/207985542-aeb647cb-9169-4c1e-ba6a-684b35d9860e.png">

<br />
<br />
<br/>
<b>Afterwards in the windows created virtual machine we set up the 1st network adapter as an internal Network named intent.</b><br /> <br />

<img width="1677" alt="Net adapter VM" src="https://user-images.githubusercontent.com/117952272/207985774-a5de2fba-914e-4852-b1db-fa3a53255d5c.png">

<br />
<br />
<br/>
<b>After we are finished with the Windows 10 installation process we go to the System Proprieties we press Rename this PC (advance) then press change and rename the computer according to our diagram as CLIENT1 and join our domain named as mydomain.com. You should receive a welcome to the domain message if you were successful.</b><br /> <br />

<img width="1677" alt="Renamed PC_Join Domain" src="https://user-images.githubusercontent.com/117952272/207986222-672aa497-32be-488e-a0ff-59794b89fa8f.png">

<br />
<br />
<br/>
<b>For changes to take place we restarted the computer and try to log in into mydomain.com with our admin account.</b><br /> <br />
  

https://user-images.githubusercontent.com/117952272/207988354-cc6984f4-391f-4331-801d-0161587d9ca3.mp4


<br />
<br />
<br/>
<b>We accessed Command Prompt on our Client1 computer and use the ipconfig command to check if we succesfully joined the domain.</b><br /> <br /> 

  

<img width="1677" alt="mydomain_cmd" src="https://user-images.githubusercontent.com/117952272/207988856-1311ce8d-d782-4cec-be16-3f4cb3264ff4.png">

<br />
<br />
<br/>
<b>In active directory we can check in DHCP our IPv4 Address Leases and find our Client 1 with the leased IP address of 172.16.0.100.</b><br /> <br />


<img width="1677" width="80%" alt="Address Lease" src="https://user-images.githubusercontent.com/117952272/207989385-0640eb1e-0f9c-48d9-9841-b1f3eba340c6.png">

<br />
<br />
<br/>
<b>In Active Directory Users and Computers we could seee our Client1 computer and that is where we would see all the machines that are part of the domain.</b><br /> <br />

<img width="1677" alt="AD computers" src="https://user-images.githubusercontent.com/117952272/207989704-86a327e8-0769-4aaf-aea8-06ce1812b5e5.png">

<br />
<br />
<br/>
<b>In order to be able to assign group policies settings to a particular group of objects and to ease the administration of the organization we creating a hierachy of all the users so if we want to implement a policy that affects only one group we should be able to do that. We opened Active Directory Users and Computer console and then right clicked on the domain and selected New, after that select Organizational Unit.</b><br /> <br /> 

<img width="1677" alt="AD_OU" src="https://user-images.githubusercontent.com/117952272/208204219-000d5494-c3e6-4a7e-92fc-9ca7d51fdfaf.png">

<br />
<br />
<br/>

<b>Below we created the Root Organizational Unit and named "Business Units" to save it press the ok button.</b><br /> <br /> 
 
<img width="1677" alt="New OU" src="https://user-images.githubusercontent.com/117952272/208523166-07ad5e8b-1e0b-45d9-acf0-ed6e3248ff95.png">

<br />
<br />
<br/>

<b>To simulate an Active Directory of an organization we create two Organizational Units. One for All Managers to list separate children Organizational Units for all the managers in separate Organizational Units for each department and the second one for Departments and list all the individual departments. This will create structure and facilitate an easier manangment of the Active Directory.</b><br /> <br /> 

<img width="1677" alt="AD Organization" src="https://user-images.githubusercontent.com/117952272/208526961-012dda7e-53dc-4dda-8820-0a1bb4abe8c2.png">

<br />
<br />
<br/>
<b>In the video below we will trasnfer all the users to the Organizational Units that they belong.</b><br /> <br />

https://user-images.githubusercontent.com/117952272/208545952-dc73de34-8659-4177-a7ed-deefdc8ec801.mp4

<br />
<br />
<br/>

<b>After we assigned all the users to the Organizational Units we will created inside every Organizational Unit individual Groups and eventually assign users to those Groups. We will start from the Parent OU all the way to every child OU. This will help us to impliment security policies a lot more efficiently.</b><br /> <br /> 


<img width="1677" alt="Group inside OU" src="https://user-images.githubusercontent.com/117952272/209221264-2cf59da5-d2d2-4b9f-8aa2-2f93c4be1ab8.png">

<br />
<br />
<br/>
<b>We named our Group "Accounting Managers Group".</b><br /> <br /> 

<img width="1677" alt="Naming of Group" src="https://user-images.githubusercontent.com/117952272/209221910-5972db15-f4e3-49ab-95ce-434f9bb26c24.png">

<br />
<br />
<br/>

<b>After we created all the Groups inside of every Organizational Unit of our organization, we will assigne all the users to the newly created Groups that they belong to. Below you can see the "Accounting Managers" Organizational Unit Users being assigned to the "Accounting Managers Group".</b><br /> <br /> 


https://user-images.githubusercontent.com/117952272/209226776-b4a5f881-6ca9-4aa5-849b-f3d44996ef1c.mp4

  
<br />
<br />
<br/>


<b>Here we can see that "All Departments Groups" was assigned a list of members which in our case are all the departments that are part of our Organization.</b><br /> <br /> 
  
<img width="1677" alt="All Dept Groups" src="https://user-images.githubusercontent.com/117952272/209222524-48b9f653-36e7-49be-9741-9eec23a5871a.png">
  
 
<br />
<br />
<br/>


<b>Therefore, we can see that the object "All Departments Groups" was assigned to be a member of "Business Units All Groups" which is the Parent OU.</b><br /> <br /> 



<img width="1677" alt="Member of BU all groups" src="https://user-images.githubusercontent.com/117952272/209245909-c46142bc-1947-454c-a2d7-c2bee8b4a74b.png">


<br />
<br />
<br/>

<b>I created a Diagram for our Organization Active Directory where we can see the structure of our Company. Later we can add other objects inside of our Organizational Units like servers, workstations, printers, applications and file shares and assign them with security policies. </b><br /> <br /> 



<img width="1392" alt="AD_Diagram" src="https://user-images.githubusercontent.com/117952272/209244979-93d2334b-944c-4451-b5b5-c7677a505edf.png">


<br />
<br />
<br/>

<b>In the following video we added as members of the Parent Group "Business Units All Groups" all the groups of our organization so when we have to assign a policy to the whole organization we just assigned it to the Parent Group so everyone else will inherit it.</b><br /> <br /> 


https://user-images.githubusercontent.com/117952272/209232405-9cadc947-3adb-400b-9378-0c3e01afd0fb.mp4


<br />
<br/>
  
<b>Here is a the walk through our Company's Organizational Units and the User Groups we created.</b><br /> <br /> 
  
   

https://user-images.githubusercontent.com/117952272/209243404-c9e7694c-55f0-4f7f-b252-569124c67e3b.mp4


<br />
<br />
<br/>

<b>Below we created and implimented a Group Policy Objective to secure our network. We blocked access to Control Panel to the Parent Group "Business Units All Groups" therefore the security policy was inherited by all the children groups. To create a Group Policy Objective you open Server Manager go to Tools then find the Group Policy Managment. In our domain we will find the Group Policy Obejctives Organizational Unit right click it and create a new GPO and named accordingly to what it is supposed to do. After creation we will right click the newly created GPO and press Edit from there we will find Policies OU / Adminisrative  Templates / Control Panel / Prohibit access to Control Panel and PC settings. After we double clicked on it we will click on enable press apply and ok for the policy to take effect. To make sure that our Policy will take authority over our company's Organizational Unit we will right click Link an Existing GPO and find our newly created Policy and press ok.
As soon as the Policy applied we opened our Client1 machine and picked a random user from our company to log in and tried to access Control Panel and check if the restrictions were applied. See the video for a detailed walk through. </b><br /> <br /> 


https://user-images.githubusercontent.com/117952272/209409506-eb25a0ea-f9c6-4dc4-8484-2650cd913723.mp4


<br />
<br />
<br/>

<b>Below we followed the same directions and created and implimented another Group Policy for our Organization. To ensure system resources safety we decided to block access to Command Prompt to all members of our company except the IT Managers and IT Department. See the stept by step guide. </b><br /> <br /> 


<img width="1316" alt="New GPO" src="https://user-images.githubusercontent.com/117952272/209413149-a341c55e-7204-41fd-b971-3d16a5e65f06.png">


<img width="1319" alt="Block Command Prompt GPO" src="https://user-images.githubusercontent.com/117952272/209413169-b1632521-8783-4d67-9c15-8383d3465164.png">

<img width="1320" alt="Edit_GPO" src="https://user-images.githubusercontent.com/117952272/209413199-62f7e4da-9f64-4519-8250-f802be5592e2.png">


<img width="1320" alt="Config GPO" src="https://user-images.githubusercontent.com/117952272/209413204-b45f78cf-b23c-4239-b5d2-250a435f6226.png">


<img width="1316" alt="Link GPO" src="https://user-images.githubusercontent.com/117952272/209413214-c3723d48-fd19-48b1-9587-888c2927b611.png">


<img width="1321" alt="Link GPO 2" src="https://user-images.githubusercontent.com/117952272/209413224-c68a25e9-cd11-4575-92ee-088176f3041b.png">

</b><br /> <br /> 


<b>Exclude IT Managers and IT Department users from this Group Policy. See below all the steps of how to exclude a user or group of users from a specific GPO.</b><br /> <br /> 



<img width="1317" alt="Exclude IT" src="https://user-images.githubusercontent.com/117952272/209579619-6bc21b75-fd24-4883-b38b-b4750f6b1c62.png">


<img width="1318" alt="Exclude IT2" src="https://user-images.githubusercontent.com/117952272/209579519-f471a891-a05c-4de4-b990-e283aca1f60b.png">


<img width="1315" alt="Exclude IT3" src="https://user-images.githubusercontent.com/117952272/209413259-b8b447df-57cc-4ecc-aa0e-9a530cbf7917.png">


<img width="1316" alt="Exclude IT4" src="https://user-images.githubusercontent.com/117952272/209413265-d06df7f1-2373-4b95-a25d-1e8538062bdd.png">


<img width="1316" alt="Exclude IT5" src="https://user-images.githubusercontent.com/117952272/209413268-da705704-d9e3-46ce-b2e3-7450939a4e4d.png">


</b><br /> <br /> 



<b>Here we will try to access the Command Prompt from a random user from our organization named Alane Dove, username "adove" that happend to be member of the Sales Managers Group. If our policy took effect and the access to Command Prompt was disabled for all users we can proceed and check if the execption for the IT Department and IT Managers was implimented as well. </b><br /> <br /> 

https://user-images.githubusercontent.com/117952272/209578473-c8b29d7a-1ead-4899-9105-787f6d8c1bc6.mp4


</b><br />

<b>To harden our Organization we should continusly work on updating and improving our Group Polices so they are up to date to the most current security treats and vulnerabilities.</b>
<b>To keep data and other resources safe we denied access to Control Panel and to Command Prompt for our users in our organization.
To further secure our Organization's Active Directory as an Administrator I would impliment the following list of Group Policies:</b> 

- <b>Prevent Windows from Storing LAN Manager Hash since they are weak and prone to hacking.</b><br /> 
- <b>Disallow Removable Media Drives, DVDs, CDs, and Floppy Drives since they are pone to infection and could affect our entire Network.</b> <br /> 
- <b>Restrict Software Installations since unwanted software can seriously compromise our network.</b> 
- <b>Disable Guest Account is needed eventhough they are disabled by default. Since there is an risk of an override by haveing this Group Policy in place such attemps will be blocked.</b> <br /> 
- <b>Disable Forced System Restarts to avoid important unsaved work.</b> <br /> 
- <b>Set Minimum Password Length to Higher Limits for example elevated accounts passwords should be set to 15 charachters and regular at least 12 to avoid unnecessary risk.</b> <br /> 
- <b>Set Maximum Password Age to Lower Limits to protect the network from stolen passwords.</b> <br /> 
- <b>Disable Anonymous SID Enumeration Setting is disabled by default to avoid exploits and unauthorized access to data make sure it remains that way.</b>

<br />
<br />
<br/> 
