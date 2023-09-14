# network_pipe
SOURCE: https://www.tecmint.com/create-network-bridge-in-rhel-centos-8/
# To create a bridge network in almalinux8.7
 
 #To list the active network connections on the test system,
 $nmcli conn show --active
 
 #create a network bridge interface using the following nmcli command, where conn or con stands for connection,
 and the connection name is br0 and the interface name is also br0.
 $nmcli conn add type bridge con-name br0 ifname br0
 
 #Add the Ethernet interface (eno2) as a portable device to the bridge (br0) connection as shown.
 
 $nmcli conn add type ethernet slave-type bridge con-name bridge-br0 ifname eno2 master br0
  
 
 #To set a static IP address, run the following commands to set IPv4 address, network mask, default gateway, 
 and DNS server of the br0 connection (set the values according to your environment).
 $nmcli conn modify br0 ipv4.addresses '192.168.10.100/24'
 
 #Next, bring up or activate the bridge connection, you can use the connection name or UUID as shown.
  $nmcli conn up br0
OR
  $nmcli conn up dc525094-a502-4100-b079-c34b5db8c4f9
 
 #Then deactivate or bring down the Ethernet or Wired connection.
 $nmcli conn down eno2
 
 
 #Now when you try to list the active network connections on the system, the bridge connection should display on the list.
 
 $nmcli conn show  --active
 
 #Next, use the following bridge command to display the current bridge port configuration and flags.
  $bridge link show
  
##########Once bridge mode setup ####################

###### Add brdige interface br0 to container ######

#clone pipework script from github

$https://github.com/ditissgithub/network_pipe.git

$chmod +x pipework

#add extra network interface

$ ./pipework.sh br0 <container id> 192.168.10.110/24
