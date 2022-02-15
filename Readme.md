# ARP Flood and Spoof Detection 

**Executing Steps**

1. Run the Controller using the following coammand: 
    **ryu-manager [filepath]/Mitigate_controller.py**

2. Create the mininet topology using the following coammand:
    **sudo mn --topo single,4 --mac --controller=remote --switch ovsk,protocols=OpenFlow13**

3. Try "pingall" command to check if all links and hosts are connected.

4. Open xterm for each host using **xterm <hostname>** command. 
Assign host 1 as DHCP server and get the ip addresses of other hosts using below commands:

->Assigning h1 as DHCP
    **h1>> echo 1 > /proc/sys/net/ipv4/ip_forward**
    **h1>> service isc-dhcp-server restart &**
 
->Assigning other hosts an ip address
For h2
    **h2>> ifconfig h2-eth0 0**
    **h2>> dhclient h2-eth0**

For h3
    **h3>> ifconfig h3-eth0 0**
    **h3>> dhclient h3-eth0**

For h4
    **h4>> ifconfig h4-eth0 0**
    **h4>> dhclient h4-eth0**
 
5. Running the attack and Testing the Controller 
From host 2 call the Arp_attack.py using following command:
    **python3 [filepath]/arp_attack.py.**

Then when we check the cache of the victim machine we can see the poisoned MAC address of the attacker.
The attacker has successfully implanted a fake Address on the victim machine.
The controller machine checks the mapped MAC address of given ip address and if it finds any discrepency , it raises a Spoofing flag and stops the attack.
 
Similarly, when we run a arp flood attack,
the controller keeps count of number of packets and if the count is greater than threshold,
it raises a flood attack flag.
    **python3 [filepath]/arp_flood_attack.py.**
