<p align="center">
<img src="https://i.imgur.com/KJgvM7a.png" height="60%" width="60%" alt="Lab Overview"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

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




Create two Virtual Machines in the same resourse group (RG-1) and virtual network

1. VM-1 - Windows 10 Pro (21H2)

2. VM-2 - Ubuntu Server 20.04




![ezgif com-gif-maker (16)](https://user-images.githubusercontent.com/121186222/215424923-3bc60db7-e1d1-44b6-b909-d647fa28ea4c.gif)




![ezgif com-gif-maker (17)](https://user-images.githubusercontent.com/121186222/215424939-c4af0380-35b0-4b3b-8f9d-b5eb71e51b4c.gif)






Connect to VM-1 with remote desktop and dowload Wireshark

Once Wireshark is downloaded, open it and capture ICMP packets

Open Command line in the VM-1 VM and ping the private IP address of the linux machine (VM-2)

For continuous ping type the command "ping  -t private IP address"

The ping is successfull and the ICMP packets are captured 

Now lets see how we can block the ICMP traffic coming from linux machine

Open azure portal, go to VM-2 --> Network Security Group --> Inbound Security Rules --> Create an Inbound security rule denying the ICMP Packets

Once an inbound rule is created go back to VM-1 Virtual Machine and notice how the ping stops receiving packets from ICMP






Now lets capture SSH packets to the linux machine

Set the filter to SSH packets only


















<img src="https://i.imgur.com/QEKbESo.png" height="70%" width="70%" alt="Continuous Ping"/>
</p>
<p>
Now, we will send a continuous ping on VM1 to VM2 so that we can see how a Network Security Group can be used to block ICMP packets.
</p>

<p>
<img src="https://i.imgur.com/jcHE3Oi.png" height="70%" width="70%" alt="Deny ICMP Packets Network Security Group"/>
</p>
<p>
Open up VM2's Network Security Group in Azure so that we can create an Inbound security rule denying ICMP packets from anywhere.
</p>

<p>
<img src="https://i.imgur.com/yxdfjsP.png" height="70%" width="70%" alt="Denied ICMP Packets Result"/>
</p>
<p>
Open up VM1 and notice how the packets are now being denied!
</p>

<p>
<img src="https://i.imgur.com/2FMDf8N.png" height="70%" width="70%" alt="SSH Wireshark"/>
</p>
<p>
Now instead of pinging VM2, we will SSH into VM 2. Update Wireshark's filter to filter SSH packets. Next, SSH into VM2 using the "ssh <username you set up>@<VM2 Private IP>" command. If you receive a message about an ECDSA key, then type YES and when prompted, enter the password you set up. Notice how the CMD has changed and Wireshark has captured SSH packets. To close our SSH session, type exit and hit ENTER
</p>

<p>
<img src="https://i.imgur.com/40NPfSI.png" height="70%" width="70%" alt="DHCP Wireshark"/>
</p>
<p>
Next, type dhcp into the Wireshark filter and enter "ipconfig /renew" into the CMD. Notice that Wireshark has captured the DHCP packets used to request a new IP address.
</p>

<p>
<img src="https://i.imgur.com/liJCe0X.png" height="70%" width="70%" alt="DNS Wireshark"/>
</p>
<p>
After that, type dns into the Wireshark filter and (if there exists) clear the existing captures. Type "nslookup www.google.com" and observe the DNS requests used to find Google's ip address.
</p>
