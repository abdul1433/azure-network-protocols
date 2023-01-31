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


![ezgif com-gif-maker (20)](https://user-images.githubusercontent.com/121186222/215884674-9543f568-14fd-495e-a0fc-7b96e2b0c8c2.gif)



![ezgif com-gif-maker (18)](https://user-images.githubusercontent.com/121186222/215884680-7301a68b-684a-4244-9e84-4ff9af900aa8.gif)






In the Wireshark set the filter to SSH packets only


Now lets SSH  into the linux machine, in the CMD type "ssh labuser@10.0.0.6" (ssh <username>@<private ip address>), enter "YES" and then enter the passwork for the following user of the linux machine

  
Notice how it is capturing SSH packets in the Wireshark 
  

  ![ezgif com-gif-maker (19)](https://user-images.githubusercontent.com/121186222/215889080-a366d44c-b300-46d2-9852-8bff231ddc47.gif)

  

 

In our last step we will assign a new IP Address for the linux machine, open the CMD in VM-1 Virtual Machine and enter "ipconfig /renew". Filter DHCP in the Wireshark and notice the aptured packets.




![ezgif com-gif-maker (21)](https://user-images.githubusercontent.com/121186222/215891161-d702f5fe-46fa-461f-bbe3-b96eec2406ac.gif)






