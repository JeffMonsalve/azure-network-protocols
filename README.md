<p align="center">
 <img src="https://github.com/user-attachments/assets/26ea713f-94b8-4f83-9cb5-517b8e295bb7" alt="Transcript Screenshot" width="600"/>
</p>







<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>

In this tutorial, we'll be observing two virtual machines, each running a different operating system. Each VM will be associated with its own Network Security Group (firewall), and we’ll be observing network traffic exchanged between the two.
 <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, DNS, RDH)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Actions and Observations</h2>

<p>
</p>
<p>
We’ll start by creating two virtual machines in Azure—one running Windows and the other running Linux. As part of this process, two separate virtual networks will also be created. Each VM should have at least 2 vCPUs and be in the same region & VNET. 
</p>
<img src="https://github.com/user-attachments/assets/047d3d27-9b19-4318-a8f3-0d103c779959" alt="Sixteenth Screenshot" width="800"/>
</p>
<br />

<p>
</p>
<p>
Use Remote Desktop to connect to your Windows 10 Virtual Machine by using its Public IP address  
</p>
<img src="https://github.com/user-attachments/assets/38050980-979b-4031-9b49-0448e2924b74" alt="Eighteenth Screenshot" width="800"/>
</p>
<br />

<p>
</p>
<p>
Within Windows 10 VM, use this link: https://www.wireshark.org/download.html to download and install Wireshark.
</p>
<img src="https://github.com/user-attachments/assets/1a4a0995-7210-4143-91fb-5c686d775745" alt="Screenshot Preview" width="800"/>
</p>
<br />

<p>
</p>
<p>
When we open Wireshark, we'll see all the network traffic occurring behind the scenes on this virtual machine. We'll begin a packet capture session, which allows us to monitor packets — small units of data sent across the network. Using Wireshark, we can see where each packet is coming from and where it’s going, based on its IP addresses.
</p>
<img src="https://github.com/user-attachments/assets/72bbcd9d-9e71-4a27-aed1-c78b0cd65e36" alt="Fifth Screenshot" width="800"/>
</p>
<br />

<p>
</p>
<p>
We will get the private IP address of the Linux virtual machine, then use PowerShell on Windows 10 VM to ping that IP. In Wireshark, we'll apply a filter to display only ICMP traffic, allowing us to see all the network traffic between the 2 virtual machines. 
</p>
<img src="https://github.com/user-attachments/assets/5e6cbe98-93fc-4901-8733-371586934c2b" alt="Sixth Screenshot" width="800"/>
</p>
<br />

<p>
</p>
<p>
Then we will initiate a continuous ping to the Linux VM from the Windows 10 VM by typing ping 10.0.0.5 -t in PowerShell. Meanwhile, in the Azure portal, we will configure a firewall rule on the Linux VM to block ICMP traffic.
</p>
<img src="https://github.com/user-attachments/assets/d968dfcb-4ca1-4a45-90a4-2c1456384c13" alt="Seventh Screenshot" width="800"/>
<img src="https://github.com/user-attachments/assets/36db1209-2dac-41a1-975c-5a70825b7d27" alt="Eighth Screenshot" width="800"/>
</p>
<br />

<p>
</p>
<p>
<Next, we will use SSH from the Windows 10 VM to remotely access the Linux VM. SSH provides a secure, text-based interface that encrypts all data transmitted between the two machines. We’ll establish the connection by entering ssh Labuser@10.0.0.5 in PowerShell and the password. Once connected, we’ll set Wireshark filter to capture SSH packets only.

<img src="https://github.com/user-attachments/assets/aa6fbd1a-7452-492d-ad02-4565d0c8508b" alt="Ninth Screenshot" width="800"/>
</p>
<br />

<p>
</p>
<p>
Next, we will use SSH from the Windows 10 VM to remotely access the Linux VM. SSH provides a secure, text-based interface that encrypts all data transmitted between the two machines. We’ll establish the connection by entering ssh Labuser@10.0.0.5 in PowerShell and the password. Once connected, we’ll set Wireshark filter to capture SSH packets only.
<img src="https://github.com/user-attachments/assets/55a0b6f3-507c-40a6-9db3-100c4406c086" alt="Nineteenth Screenshot" width="800"/>
</p>
<br />

<p>
</p>
<p>
Now it’s time to filter DNS traffic. We'll configure Wireshark to capture only DNS packets. To generate DNS traffic, we’ll use the command nslookup www.disney.com, which sends a request to the DNS server asking for the IP address associated with the Disney website.
</p>

<img src="https://github.com/user-attachments/assets/e3e24000-6a7a-4034-a335-bc3de1d653ec" alt="Tenth Screenshot" width="800"/>
</p>
<br />

<p>
</p>
<p>
Lastly, we will filter for RDP traffic. By applying the filter tcp.port == 3389 in Wireshark, we can isolate Remote Desktop Protocol packets. You'll notice a continuous stream of traffic, as RDP is constantly sending data to your computer so that the screen looks exactly like the Windows 10 machine.
</p>
<img src="https://github.com/user-attachments/assets/550d952b-07db-4dc4-9ccd-7a4c8086b1c4" alt="Eleventh Screenshot" width="800"/>

