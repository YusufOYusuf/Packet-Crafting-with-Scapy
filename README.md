<h1>Packet Crafting with Scapy</h1>


<h2>Description</h2>
Building a packet field-by-field demonstrates how someone could manipulate the
packet traffic entering or leaving a network. In this lab I learned how to build packets layer- by-layer using Scapy, a packet manipulation tool, and then implementing the finished
packets to perform various network functions.
<br />



<h2>Environments Used </h2>

- <b>Kali GNU/Linux</b>
- <b>pfSense</b>
- <b>OWASP Broken Web App</b>

<h2>Program walk-through:</h2>

<p align="center">
In the new Terminal window, type the command "scapy" to initialize the Scapy
application. Press Enter: <br/>
<img src="https://i.postimg.cc/3NsPqbZn/Screen-Shot-2022-09-25-at-4-58-38-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/>
<br />
  
  
<br />
List out all of the protocols and layers available for packet manipulation by
typing the "ls()" command, followed by pressing the Enter :  <br/>
<img src="https://i.postimg.cc/4yg0bh4S/Screen-Shot-2022-09-25-at-5-02-16-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/>
<br />
  
  
  
<br />
Enter the "lsc()" command to list the available commands.: <br/>
<img src="https://i.postimg.cc/9fczSL8m/Screen-Shot-2022-09-25-at-5-05-17-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/>
<br />
  
  
  

  
  
  
<br />
Enter the "ip=IP(ttl=10)" command within the Scapy prompt to set the Time to Live for
the IP packet. Then check to ensure the previous modification took effect by entering the command
"ip".:  <br/>
<img src="https://i.postimg.cc/y8KnWzp7/Screen-Shot-2022-09-25-at-5-12-56-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/>
<br />
  
 
 
 
 
 
 
 <br />
Identify the current IP destination by entering the command "ip.dst":  <br/>
<img src="https://i.postimg.cc/XqdfSFDc/Screen-Shot-2022-09-25-at-5-18-54-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/>
<br />
 
 
 
 
 
 
 
  
<br />
Identify the current IP source by entering the command "ip.src".:  <br/>
<img src="https://i.postimg.cc/0Nf6RnfC/Screen-Shot-2022-09-25-at-5-24-15-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/>
  
  
  
  
  
<br />
Change the IP destination with the "ip.dst=”192.168.9.1”" command then verify the changes by typing command "ip":  <br/>
<img src="https://i.postimg.cc/TP7D5QD3/Screen-Shot-2022-09-25-at-5-29-01-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 
  
  
  
  
  
  
  
 <br />
Change the IP source address using the "ip.src=”192.168.9.2" command and then verify modifications by typing command "ip":  <br/>
<img src="https://i.postimg.cc/GpqkJdZr/Screen-Shot-2022-09-25-at-5-32-38-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 
   
  
  
  
  
  
  
 <br />
With the TTL, source address, and destination address populated, remove the
TTL and set it to the default TTL specified in the RFC. Enter the command "del(ip.ttl)" then verify removal by typeing "ip" command.:  <br/>
<img src="https://i.postimg.cc/d3pM7Mqj/Screen-Shot-2022-09-25-at-5-37-07-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 
  
  
  
  
  
  
  
  
  
  <br />
Verify the TTL is the RFC value of 64 by typing the "ip.ttl" command and then Add additional protocol layers by adding TCP on top of IP by using the "ip/TCP()" command:  <br/>
<img src="https://i.postimg.cc/15BCY1xC/Screen-Shot-2022-09-25-at-5-42-19-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 
  
  
  
  
  
  
<br />
Add some information to the TCP protocol fields by typing "tcp=TCP(sport=1025, dport=80)" and then Show the TCP stack by typing the "(tcp/ip).show()".:  <br/>
<img src="https://i.postimg.cc/zvVvZ1tC/Screen-Shot-2022-09-25-at-5-49-57-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 
  
  
  
  
  

<br />
Now we will add an Ethernet layer by typeing "Ether()/ip":  <br/>
<img src="https://i.postimg.cc/MpHrgZ8P/Screen-Shot-2022-09-25-at-5-55-32-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 





<br />
In the new Terminal window, type the "wireshark" command to open up wireshark:  <br/>
<img src="https://i.postimg.cc/R0Vfgq5h/Screen-Shot-2022-09-25-at-5-58-49-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 




<br />
Within the Wireshark window, select the eth0 interface from the Capture panel and press CTRL+E to start capturing.:  <br/>
<img src="https://i.postimg.cc/Dwtkg4bd/Screen-Shot-2022-09-25-at-6-02-18-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 






<br />
Navigate back to the Terminal window with the Scapy prompt. Generate a single ICMP packet to be sent to the OWASP machine. Enter the
command "packet=sr1(IP(dst=”192.168.68.12”)/ICMP()/”XXXXXXXXXXX”)".:  <br/>
<img src="https://i.postimg.cc/6pdqCK83/Screen-Shot-2022-09-25-at-6-09-58-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 






<br />
Go back to the terminal with the Scapy prompt and enter the command "packet" to show the contents of the packet, which was
created. :  <br/>
<img src="https://i.postimg.cc/6pfkn6NY/Screen-Shot-2022-09-25-at-6-15-04-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 





<br />
Enter the command "packet=sr1(IP(dst=”192.168.68.12”)/TCP(dport=80,flags=”S”))" in an attempt to initiate a simple SYN scan on a single port.:  <br/>
<img src="https://i.postimg.cc/W3F48YjW/Screen-Shot-2022-09-25-at-6-20-42-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 







<br />
Navigate back to the Wireshark window. Analyze the given Wireshark output and notice a SYN packet was sent with a SYN, ACK packet being received indicating that port 80 is open.:  <br/>
<img src="https://i.postimg.cc/BbP18QXv/Screen-Shot-2022-09-25-at-6-22-46-PM.png" height="80%" width="80%" alt="Configuring Advanced Ethernet Options Steps"/> 










  
  
  
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
