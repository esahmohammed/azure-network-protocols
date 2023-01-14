<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Actions and Observations</h2>

<p>
In the first step of this tutorial we will need to start off by creating two Virtual Machines using Microsoft Azure. One of the VMs will need to be Windows 10 and the other machine will need to be Linux (Ubuntu), both will need to be connected to the same VNET.
</p>
<br />
<p>
<img src="https://i.imgur.com/coEhszo.png" height="40%" width="40%" alt="VNET"/>
</p>

<p>
After completing this step, go over to your Windows 10 machine using remote desktop by entering your VMs Public IP Address and install Wireshark with the following link: https://www.wireshark.org/download.html After installing Wireshark, open and filter for ICMP traffic only. ICMP uses the ping protocol, we can use this protocol to ping our Linux (Ubuntu) Private IP Address in our Command Prompt and observe the ping requests and replies in our Wireshark.
</p>
<br />
<p>
<img src="https://i.imgur.com/uo4bV6Z.png" height="80%" width="80%" alt="Filter ICMP"/>
</p>

<p>
<img src="https://i.imgur.com/it44TK6.png" height="40%" width="40%" alt="Ping ICMP"/>
</p>
<p>
Now we can initiate a perpetual ping which is a non-stop ping from our Windows 10 VM to our Linux (Ubuntu) Machine using the -t command in our command prompt. This will ping the Linux machine until we decide to stop pinging. As the machine perpetually pings, open the Network Security Group of your Linux (Ubuntu) Virtual Machine on Microsoft Azure and disable incoming (inbound) ICMP traffic. We can do so by creating a new Network Security Group and adding an inbound security rule. If we go back to our Windows 10 VM now, we can observe that all ICMP traffic in our command prompt and Wireshark are timed out as we disabled it. Allowing incoming (inbound) ICMP traffic will reenable the ping.
</p>
<br />

<p>
<img src="https://i.imgur.com/s8jor9C.png" height="40%" width="40%" alt="Perpetual Ping"/>
</p>
<p>
<img src="https://i.imgur.com/Lp8bf2z.png" height="40%" width="40%" alt="ICMP DENIED"/>
</p>
<p>

<p>
In our next step we will SSH into our Linux machine through our Windows 10 VM using the command prompt. SSH is similar to RDP (Remote Desktop Protocol) but instead has no GUI. We use SSH to gain access to another machines command line. First we filter for ssh traffic in Wireshark so we can observe the feedback we get, then we shh into our Linux (Ubuntu) VM using the command "ssh labuser@10.0.0.5" in our command prompt. After we have successfully logged in, we can see that Wireshark immediately shows feedback on whatever we type in the command prompt.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Going back to Wireshark, we will filter for only DHCP traffic. DHCP is used to assign ip addresses to computers, so we will use DHCP to give our Windows 10 VM a new IP Address. Using our command prompt on our Windows 10 VM, we will use the command "ipconfig /renew" and observe that Wireshark will start showing DHCP traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next we will filter for only DNS traffic in Wireshark. We can start seeing results in our Wireshark by opening our command prompt and using the command "nslookup www.google.com" or any link of your choice. This command will ask our DNS what is links IP address or for example google's IP address, as DNS takes human readable names and converts them into IP addresses that the computer can use.  
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
For the final step we will filter for RDP traffic only. We can filter for RDP traffic in wireshark by entering tcp.port == 3389. After filtering, we can see that the traffic does not stop in Wireshark as we are using the Remote Desktop Protcol (RDP) to access our virtual machine. 
</p>
<br />
