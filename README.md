# Linux Iptables for traffic manipulating   
Iptables Usage in linux


Iptables is a user-space utility program that allows a system administrator to configure the IP packet filter rules of the Linux kernel firewall. The term iptables is also commonly used to inclusively refer to the kernel-level components. x_tables is the name of the kernel module carrying the shared code portion used by all four modules that also provides the API used for extensions; subsequently, Xtables is more or less used to refer to the entire firewall (v4, v6, arp, and eb) architecture.

INPUT modules will use for incomming traffic to our host similarly OUTPUT will use for outgoing traffic and FORWARD will use to all packets that have been routed and were not for local delivery will traverse this chain.


##Linux Iptables

`e.g: Iptables -I (INPUT/OUTPUT/FORWARD) -p tcp –dport (Port) -s (IP) -j accept/reject`


##To save ip tables rule 

`Sudo /sbin/iptables-save`


##Add input rules for http connection

`sudo iptables -A INPUT -p tcp --dport 80 -j REJECT`


##Add output rules http connection

`sudo iptables -A OUTPUT -p tcp --dport 80 -j REJECT`


##list rule with line numbers 

`sudo iptables -L -v --line-numbers`


##delete rules with line number

`sudo iptables -D OUTPUT 2`


##Telnet iptables block if someone telnet host 

`sudo iptables -A INPUT -p tcp --dport 23 -j DROP`


##If host will try to telnet so we can block it 

`sudo iptables -A OUTPUT -p tcp --dport 23 -j DROP`


##Blocking traffic with source IP and port for outbound traffic

`sudo iptables -A OUTPUT -p tcp -s 192.168.41.1 --dport 80 -j REJECT`


##Blocking traffic with source IP and port for outbound traffic

`sudo iptables -A INPUT -p tcp -s 192.168.41.1 --dport 80 -j REJECT`


##We can also block the traffic with complete pool 

`sudo iptables -A INPUT -p tcp -s 192.168.41.0/24 --dport 80 -j REJECT`


##When we are using ping, we are sending "echo request" (type 8) type of ICMP packets & in return we are getting "echo-reply" (type 0) "ICMP" packets, so we can use FORWARD filter to utilize traffic manipulation

`sudo iptables -t filter -A FORWARD -p imcp -s 10.0.0.1 -d 192.168.0.1 --icmp-tpye echo request -j DROP`




