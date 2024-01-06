<h1>Active Directory Home Lab </h1>

<h2>Description</h2>
This project is a walkthrough of how I created an Active Directory home lab Environment using VirtualBox. I set up and configured a Domain Controller to run Active Directory. The purpose of this lab is to simulate a business environment and for me to operate as the Administrator.
<br />

<h2>Utilities Used</h2>

- <b>Active Directory</b> 


<h2>Environments Used </h2>

- <b>VirtualBox</b>
- <b>Windows Server 2019</b>
- <b>Windows 10 Pro</b> (22H2)

<h2>Links</h2>

- <b>VirtualBox:</b> https://www.virtualbox.org/wiki/Downloads
- <b>Windows Server 2019 ISO:</b> https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019
- <b>Windows 10 ISO:</b> https://www.microsoft.com/en-us/software-download/windows10

<h2 align="center">Program walk-through</h2>

<p align="center">
<b>The network diagram I'll be using for this project.</b> <br/>
<img src="https://imgur.com/8xT1Sri.jpg" height="80%" width="80%" alt="Network Diagram"/>
<br />
<br />
<br />
<p align="center">
<b>I started by installing the server on the VM.</b> <br/>
<img src="https://imgur.com/LJx50Lv.jpg" height="80%" width="80%" alt="Installing the server on the VM"/>
<br />
<br />
<br />
<img src="https://imgur.com/EzSERWn.jpg" height="80%" width="80%" alt="Choose the right option"/>
<br />
<br />
<br />
<img src="https://imgur.com/GLR768t.jpg" height="80%" width="80%" alt="Custom install"/>
<br />
<br />
<br />
<img src="https://imgur.com/eSceovN.jpg" height="80%" width="80%" alt="Choose the driver"/>
<br />
<br />
<br />
<p align="center">
<b>Once the set-up is complete you will have to reboot your VM. When your machine is on you will need to send a "Ctr+Alt+Delete" command. Go to "Input > Keyboard > Insert", (see the picture below). </b> 
<img src="https://imgur.com/vHEiAyE.jpg" height="80%" width="80%" alt="Commands"/>
<br />
<br />
<br />
<p align="center">
<b> I need two network adapters for the VM that will be hosting my DC. I need the NAT that will use my host IP address from my home router and an Internal Network Adapter so my DC can communicate with other VMs. </b> <br/>
<img src="https://imgur.com/KPhbN22.jpg" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
<br />
<br />
<br />
<img src="https://imgur.com/xMxJiEv.jpg" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
<br />
<br />
<p align="center">
<b>Figuring out which NIC is our NAT and which is our internet network, I rename the adapters to differentiate as it is important later on when setting up the DC and DHCP.</b> <br/>
<img src="https://imgur.com/O7uDmrp.jpg" height="80%" width="80%" alt="Rename"/>
<br />
<br />
<b>Now I’ve configured the Internal network adapter and assigned it an IP address based on the diagram above (172.16.0.1) and I do not need to give it a default gateway as the DC is the gateway. As for the DNS server, I assigned an IP based on the diagram because when we install Active Directory it will install DNS. I set it as a loopback address so it pings itself.</b> <br/>
<img src="https://imgur.com/xMM9gt2.jpg" height="80%" width="80%" alt="IP"/>
<br />
<br />
<b>Now that the NICs are differentiated, I renamed the VM as Practise. This forces a restart</b> <br/>
<img src="https://imgur.com/tKcm0DH.jpg" height="80%" width="80%" alt="Renaming the PC"/>
<br />
<br />
<b>After restarting, I installed Active Directory Domain Services through Server Manager and set up the server as the domain immediately. When the server is promoted to a domain, it forces a restart.</b> <br/>

<img src="https://imgur.com/t0DUH6T.jpg" height="80%" width="80%" alt="AD installation"/>
<br />
<p align="center">
 <img src="https://imgur.com/7ug890z.jpg" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
 <p align="center">
<br />
<br />
<p align="center">
<b>Using the built-in Admin account, I will create a dedicated domain Admin account, granting it Domain Admin permissions on AD. </b> <br/>
</p>
<p align="center">
 <img src="https://imgur.com/HG50Cdg.jpg" height="80%" width="80%" alt="Creating Admin account"/>
<br />
<br />
<p align="center">
<b>Now I need to install RAS/NAT (incl Routing) for my Windows 10 client to gain access to the internet through the internal network via the DC.</b> <br/>
</p>
<p align="center">
 <img src="https://imgur.com/CKYDBRh.jpg" height="80%" width="80%" alt="Installing RAS"/>
<br />
<br />
<p align="center">
<b>Now that the role is installed, I need to configure the Routing and Remote Access under tools in Server Manager. Click Tools in Server Manager and Right click ‘Practice’ and configure and enable routing and remote access. Under configuration, select NAT and the external NIC (the internet).</b> <br/>
</p>
<p align="center">
<img src="https://imgur.com/9sdMtQs.jpg" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
   <img src="https://imgur.com/xBwrlKz.jpg" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
   <img src="https://imgur.com/6ArB8q6.jpg" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
   <img src="https://imgur.com/cWGOFtd.jpg" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
<p align="center">
<b>After Remote Access has been configured, install the DHCP Server. This will allow our Windows 10 clients to be assigned an IP address and gain access to the internet..</b> <br/>
</p>
<p align="center">
 <img src="https://imgur.com/VpQuR04.jpg" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br />
<p align="center">
<b>The purpose of the DHCP server is to allow machines on the network to automatically be assigned an IP address. The scope created will assign IP addresses in a range, that being 172.16.0.100-200 so the DHCP will effectively be able to give out 100 IP addresses (you can also configure the lease time of the IP addresses for the client machines so that the IP cannot be used by other devices).</b> <br/>
</p>
<p align="center">
<img src="https://imgur.com/JTjhG5n.jpg" height="80%" width="80%" alt="Install DCHP"/>
<br />
<p align="center">
<img src="https://imgur.com/4MNAjEQ.jpg" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br />
<p align="center">
<b>Now the DC and AD are configured. This Finalises the Active Directory Lab. This can be further modified by implementing Group Policies, security features, programs etc.</b>  <br/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in grey
@@ text in purple (and bold)@@
```
--!>
