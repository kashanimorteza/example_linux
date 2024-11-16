<a href="#combine-internet-connection">Combine Internet Connection</a> - 
<a href="#openvpn-client">OpenVpn Client</a>



<!-----------------------------------------------------------Combine Internet Connection----------------------------------------------------------->
<div class="md5"></div>

## Combine Internet Connection

#### <span class="red">Install</span>

	Download "CD Image" from Mikrotik
	Create Virtual box : linux | other linux 64 bit
	Default login  : admin | no password
	install wine and install WinBox
	wine /home/abd/Downloads/winbox64.exe

#### <span class="red">Interface : Change name</span>

	/
	/interface
	set ether1 name=ISP1
	set ether2 name=ISP2
	set ether3 name=ISP3
	set ether4 name=ISP4
    set ether5 name=Local

#### <span class="red">Interface : Add List</span>

	/
	/interface
	list add name=internet
	list member add interface=ISP1 list=internet
	list member add interface=ISP2 list=internet
	list member add interface=ISP3 list=internet
	list member add interface=ISP4 list=internet

#### <span class="red">IP : Set IP Addresses</span> 

	/
	/ip address
	add address=192.168.1.2/24 network=192.168.1.0 broadcast=192.168.1.255 interface=ISP1
	add address=192.168.2.2/24 network=192.168.2.0 broadcast=192.168.2.255 interface=ISP2
	add address=192.168.3.2/24 network=192.168.3.0 broadcast=192.168.3.255 interface=ISP3
	add address=192.168.4.2/24 network=192.168.4.0 broadcast=192.168.4.255 interface=ISP4
	add address=192.168.0.2/24 network=192.168.0.0 broadcast=192.168.0.255 interface=Local	

#### <span class="red">Route : Add Default Route</span> 

	/
	/ip route
	add dst-address=0.0.0.0/0 gateway=192.168.1.1 distance=1 check-gateway=ping
	add dst-address=0.0.0.0/0 gateway=192.168.2.1 distance=2 check-gateway=ping
	add dst-address=0.0.0.0/0 gateway=192.168.3.1 distance=3 check-gateway=ping
	add dst-address=0.0.0.0/0 gateway=192.168.4.1 distance=4 check-gateway=ping

#### <span class="red">Firewall : Mangle : Nat Local Network</span> 

	/	
	/ip firewall nat
	add chain=srcnat src-address=192.168.0.0/24 out-interface-list=internet action=masquerade

#### <span class="red">Firewall : Mangle : Mark packets from Internet to Local</span> 

	/	
	/ip firewall mangle
	add chain=prerouting in-interface=ISP1 connection-mark=no-mark action=mark-connection new-connection-mark=ISP1
	add chain=prerouting in-interface=ISP2 connection-mark=no-mark action=mark-connection new-connection-mark=ISP2
	add chain=prerouting in-interface=ISP3 connection-mark=no-mark action=mark-connection new-connection-mark=ISP3
	add chain=prerouting in-interface=ISP4 connection-mark=no-mark action=mark-connection new-connection-mark=ISP4

#### <span class="red">Firewall : Mangle : Mark packets from Local to Internet</span> 

	/	
	/ip firewall mangle
	add chain=prerouting in-interface=Local connection-mark=no-mark dst-address-type=!local per-connection-classifier=both-addresses-and-ports:4/0 action=mark-connection new-connection-mark=ISP1
	add chain=prerouting in-interface=Local connection-mark=no-mark dst-address-type=!local per-connection-classifier=both-addresses-and-ports:4/1 action=mark-connection new-connection-mark=ISP2
	add chain=prerouting in-interface=Local connection-mark=no-mark dst-address-type=!local per-connection-classifier=both-addresses-and-ports:4/2 action=mark-connection new-connection-mark=ISP3
	add chain=prerouting in-interface=Local connection-mark=no-mark dst-address-type=!local per-connection-classifier=both-addresses-and-ports:4/3 action=mark-connection new-connection-mark=ISP4

#### <span class="red">Firewall : Mangle : Add PCC Route</span> 

	/	
	/ip firewall mangle
	add chain=prerouting in-interface=Local connection-mark=ISP1 action=mark-routing new-routing-mark=ISP1
	add chain=prerouting in-interface=Local connection-mark=ISP2 action=mark-routing new-routing-mark=ISP2
	add chain=prerouting in-interface=Local connection-mark=ISP3 action=mark-routing new-routing-mark=ISP3
	add chain=prerouting in-interface=Local connection-mark=ISP4 action=mark-routing new-routing-mark=ISP4
	add chain=output connection-mark=ISP1 action=mark-routing new-routing-mark=ISP1
	add chain=output connection-mark=ISP2 action=mark-routing new-routing-mark=ISP2
	add chain=output connection-mark=ISP3 action=mark-routing new-routing-mark=ISP3
	add chain=output connection-mark=ISP4 action=mark-routing new-routing-mark=ISP4

#### <span class="red">IP : Route : Add PCC Route</span> 

	/
	/ip route
	add dst-address=0.0.0.0/0 gateway=192.168.1.1 routing-mark=ISP1
	add dst-address=0.0.0.0/0 gateway=192.168.2.1 routing-mark=ISP2
	add dst-address=0.0.0.0/0 gateway=192.168.3.1 routing-mark=ISP3
	add dst-address=0.0.0.0/0 gateway=192.168.4.1 routing-mark=ISP4

#### <span class="red">DNS</span>

	/ip dns set allow-remote-requests=yes cache-max-ttl=1w cache-size=5000KiB max-udp-packet-size=512 servers=8.8.8.8



<!-----------------------------------------------------------OpenVpn Client----------------------------------------------------------->
<div class="md1"></div>

## OpenVpn Client

#### <span class="red">Install</span>

	Download Mikrotik VmWare File Cracked version 7.1.1
	Install VmWare Workstation player 
	Import Mikrotik VmWare File to VmWare Workstation player
	Default login  : admin | admin

#### <span class="red">File : Upload OpenVpn Client File</span> 

	file > Upload

#### <span class="red">Certificated : Import OpenVpn Client File</span> 

	system > certificated > import

#### <span class="red">IP : Set IP Addresses</span> 

	/
	/ip address
	add address=192.168.1.200/24 network=192.168.1.0 broadcast=192.168.1.255 interface=ether1

#### <span class="red">Route : Add Default Route</span> 

	/
	/ip route
	add distance=1 dst-address=0.0.0.0/0 gateway=192.168.1.1 

#### <span class="red">Interface : Add OpenVpn Client</span> 

	/	
	/interface ovpn-client
	add name=vpnbook-out connect-to=198.7.62.204 port=443 mode=ip user=vpnbook password=z93cvfv auth=sha1 cipher=aes128

#### <span class="red">Firewall : Nat</span> 

	/	
	/ip firewall nat
	add chain=srcnat out-interface=vpnbook-out action=masquerade	

#### <span class="red">Firewall : Filter</span> 

	/
	/ip firewall filter
	add chain=output out-interface=vpnbook-out action=accept 
	add chain=forward out-interface=vpnbook-out action=accept
	add chain=input src-address=192.168.1.0/24 in-interface=vpnbook-out action=accept
	add chain=input protocol=tcp dst-port=80 action=accept