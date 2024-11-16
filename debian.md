

<div>
General :
<a href="#basic">Basic</a> - 
<a href="#tools">Tools</a> - 
<a href="#network">Network</a> - 
<a href="#ssh">SSh</a> - 
</div>
<div>
Software :
<a href="#chrome">Chrome</a> - 
<a href="#xdm">XDM</a> -
<a href="#wine">Wine</a> - 
<a href="#virtualbox">Virtualbox</a> -
<a href="#vmware">Vmware</a>
</div>
<div>
Service :
<a href="#ifenslave">ifenslave</a> - 
<a href="#xrdp">Xrdp</a> - 
<a href="#openvpn">Openvpn</a>
</div>


<!----------------------------------------------------------------------------------[General]-->
<div class="md5"></div>

## General

#### <span class="red">Basic</span>
	sudo timedatectl set-timezone UTC
	Disable ufw Firewall
	Disable iptables Firewall
	Install network tools
	sudo apt update
	sudo apt upgrade

#### <span class="red">Tools</span>

	sudo apt install software-properties-common
	sudo apt install apt-transport-https
	sudo apt install wget
	sudo apt install build-essential 
	sudo apt install ca-certificates
	sudo apt-get install unixodbc-dev

#### <span class="red">Network</span>

	sudo apt install net-tools
	sudo apt install iputils-ping
	sudo apt install openssh-server
	sudo apt install traceroute

<span class="blue">IP forwarding</span> 

	sysctl -p
	cat /proc/sys/net/ipv4/ip_forward
	sysctl -w net.ipv4.ip_forward=1
	sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf



<!-----------------------------------------------------------DNS-->
#### <span class="red">DNS</span>

<span class="blue">Command</span>

	resolvectl status
	restart systemd-resolved.service


<span class="blue">Disable dhcp dns</span>
	vim /etc/netplan/50-cloud-init.yaml
	------------------------------------
	network:
		version: 2
		ethernets:
			enp1s0:
				dhcp4: true
				dhcp4-overrides:
				use-dns: false
				match:
					macaddress: 56:00:04:f1:25:b3
				set-name: enp1s0
	------------------------------------
	sudo netplan apply



<!-----------------------------------------------------------Transfer File-->
#### <span class="red">Transfer File</span>

<span class="blue">From Server</span>

	scp root@108.61.175.212:~/client-configs/files/abd.ovpn ~/linux/vpn/abd.ovpn

<span class="blue">To Server</span>

	scp ~/linux/vpn/abd.ovpn root@108.61.175.212:~/client-configs/files/abd.ovpn



<!-----------------------------------------------------------Software----------------------------------------------------------->
<div class="md1"></div>

## Software

#### <span class="red">Chrome</span>

	wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
	sudo apt install ./google-chrome-stable_current_amd64.deb

#### <span class="red">XDM</span>

	cd ~/Downloads/
	wget https://github.com/subhra74/xdm/releases/download/7.2.11/xdm-setup-7.2.11.tar.xz
	tar -xf xdm-setup-*.tar.xz
	sudo ./install.sh

#### <span class="red">Wine</span>

	Linux
 	-------------------------------------------
	dpkg --add-architecture i386
	mkdir -pm755 /etc/apt/keyrings
	wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key
 	wget https://dl.winehq.org/wine-builds/ubuntu/dists/jammy/winehq-jammy.sources
	cp ./winehq-jammy.sources /etc/apt/sources.list.d/  
 	apt update
	apt install --install-recommends winehq-stable

 	apt install mono-complete
	wget https://dl.winehq.org/wine/wine-mono/9.0.0/wine-mono-9.0.0-x86.msi
 	wine64 uninstaller
  	Press install from the uninstaller GUI and select the downloaded .msi package
  

	Command
 	-------------------------------------------
	winecfg
	wine --version
 
	Install
 	------------------------------------------- 
	wget https://download.mql5.com/cdn/web/stratos.trading.pty/mt4/fxcm4setup.exe
	wine fxcm4setup.exe
 
#### <span class="red">Virtualbox</span>

	sudo apt install virtualbox

	sudo apt-get remove virtualbox-\*
	sudo apt-get purge virtualbox-\*
	sudo apt autoremove

#### <span class="red">Vmware</span>

	sudo apt install gcc build-essential linux-headers-$(uname -r)
	Download VMware-Player From https://www.vmware.com/products/workstation-player.html
	chmod +x VMware-Player-Full-*.bundle
	sudo VMware-Player-Full-*.bundle
	Search VMware-Player And Launch VMware and complete the setup


	
<!-----------------------------------------------------------Service----------------------------------------------------------->
<div class="md1"></div>

## Service

<!-----------------------------------------------------------ifenslave-->
#### <span class="red">Ifenslave</span> 

	sudo apt install ifenslave
	sudo modprobe bonding

	sudo vim /etc/network/interfaces
	-----------------------------------------------
	auto enp0s3
	iface enp0s3 inet manual
		bond-master bond0
		bond-primary enp0s3 enp0s8

	auto enp0s8
	iface enp3s1 inet manual
		bond-master bond0
		bond-primary enp0s3 enp0s8

	auto bond0
	iface bond0 inet static
			address 192.168.0.2
			netmask 255.255.255.0
			dns-nameservers 8.8.8.8 4.2.2.4
			dns-search domain.local
					slaves enp0s3 enp0s8
					bond_mode 0
					bond-miimon 100
					bond_downdelay 200
					bond_updelay 200

	--------------------------------------------------------

	/etc/init.d/networking restart

	cat /proc/net/bonding/bond0

	sudo ifenslave bond0 enp3s0 wlp2s0

	journalctl -f -u NetworkManager

	nmcli dev wifi
	
	sudo ip link delete dev bond0

	---------------------------------------------------

	sudo nmcli device
	sudo nmcli device status
	sudo nmcli connection
	sudo nmcli connection up bond0
	sudo service networking restart

	
	sudo nmcli connection add type bond con-name bond0 ifname bond0 bond.options "mode=6,miimon=100,downdelay=200,updelay =200"
	
	sudo nmcli connection add type ethernet slave-type bond con-name bond0-port1 ifname enp0s3 master bond0
	sudo nmcli connection add type ethernet slave-type bond con-name bond0-port2 ifname enp0s8 master bond0
	--------
	sudo nmcli connection modify "conn1" master bond0
	sudo nmcli connection modify "conn2" master bond0

	sudo nmcli connection modify bond0 ipv4.addresses '192.168.0.1/24'
	sudo nmcli connection modify bond0 ipv4.gateway '192.168.0.2'
	sudo nmcli connection modify bond0 ipv4.dns '8.8.8.8'
	sudo nmcli connection modify bond0 ipv4.dns-search 'domain.local'
	sudo nmcli connection modify bond0 ipv4.method manual

	sudo nmcli connection up bond0
	sudo nmcli connection modify bond0 connection.autoconnect-slaves 1
	sudo nmcli connection up bond0

	--------------------------------------------------------

	auto bond0
			iface bond0 inet static
			address 192.168.0.54
			netmask 255.255.255.0
			network 192.168.0.0
			gateway 192.168.0.1

	auto bond0
	iface bond0 inet static
			address 192.168.0.110
			netmask 255.255.255.0
			gateway 192.168.0.1
			dns-nameservers 8.8.8.8 4.2.2.4
			dns-search domain.local
					slaves enp3s0 wlp2s0
					bond_mode 0
					bond-miimon 100
					bond_downdelay 200
					bond_updelay 200

	--------------------------------------------------------------
	ip route flush cache

	ip link add bond0 type bond
	ip addr add 10.80.0.2/30 dev bond0

	ip link set tap0 master bond0
	ip link set tap1 master bond0

	ip link set bond0 up mtu 1440

	/usr/local/bin/gw bond0


<!-----------------------------------------------------------Xrdp-->
#### <span class="red">Xrdp</span> 

	apt update
	apt upgrade
	apt install xorg dbus-x11 x11-xserver-utils 
	apt install xfce4 xfce4-goodies 
	apt install ubuntu-desktop 
	apt install task-gnome-desktop
	apt install xrdp 
	useradd -m -p $(openssl passwd -1 "Morteza123456") "morteza"
	echo "morteza ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
	systemctl set-default graphical.target


<!-----------------------------------------------------------OpenVpn----------------------------------------------------------->
<div class="md1"></div>

## OpenVpn 

<!-----------------------------------------------------------General-->
#### <span class="red">General</span> 

<span class="blue">Link</span> : https://www.digitalocean.com/community/tutorials/how-to-set-up-an-openvpn-server-on-ubuntu-18-04

<span class="blue">Link</span> : https://docs.digitalocean.com/

<span class="blue">library</span>

	OpenVpn : TLS/SSL VPN
	EasyRSA : is a CLI utility to build and manage a PKI CA With RSA Algorithm

<span class="blue">Tag</span>

	VPN : Virtual Private Network
	SSL : Secure Socket Layer
	TLS : Transfer Layer Security
	RSA : Rivest Shamir Adleman
	CA  : certificate authority
	PKI : public key infrastructure for CA

<span class="blue">Install</span>

	cd
	sudo apt install openvpn

<!-----------------------------------------------------------Create Server-->
#### <span class="red">Create Server</span> 

<!----------Step -1-->
<span class="blue">Step 1 — Variable</span>

	EasyRSA_Version=3.1.0
	proto=tcp
	ip=108.61.175.212
	port=443
	localip=192.168.5.0
	subnet=255.255.255.0
	op_auth=/etc/openvpn/op_auth.sh


<!----------Step 2-->
<span class="blue">Step 2 — Clear</span>

	sudo rm -fr EasyRSA-$EasyRSA_Version
	sudo rm -fr EasyRSA-$EasyRSA_Version.tgz
	sudo rm -fr ~/client-configs
	sudo rm -fr ~/client-configs/keys
	sudo rm -fr $op_auth

<!----------Step 3-->
<span class="blue">Step 3 — Installing OpenVPN and EasyRSA</span>

	wget -P ~/ https://github.com/OpenVPN/easy-rsa/releases/download/v$EasyRSA_Version/EasyRSA-$EasyRSA_Version.tgz
	tar xvf EasyRSA-*
	cd ~/EasyRSA-*/

<!----------Step 4-->
<span class="blue">Step 4 — Configuring the EasyRSA Variables and Building the CA</span>

	-------------------------------------------------------------------------------------------------------------
	RSA Config
	-------------------------------------------------------------------------------------------------------------
	sed -i 's/#set_var EASYRSA_REQ_COUNTRY/set_var EASYRSA_REQ_COUNTRY/' ~/EasyRSA-$EasyRSA_Version/vars.example
	sed -i 's/#set_var EASYRSA_REQ_PROVINCE/set_var EASYRSA_REQ_PROVINCE/' ~/EasyRSA-$EasyRSA_Version/vars.example
	sed -i 's/#set_var EASYRSA_REQ_CITY/set_var EASYRSA_REQ_CITY/' ~/EasyRSA-$EasyRSA_Version/vars.example
	sed -i 's/#set_var EASYRSA_REQ_ORG/set_var EASYRSA_REQ_ORG/' ~/EasyRSA-$EasyRSA_Version/vars.example
	sed -i 's/#set_var EASYRSA_REQ_EMAIL/set_var EASYRSA_REQ_EMAIL/' ~/EasyRSA-$EasyRSA_Version/vars.example
	sed -i 's/#set_var EASYRSA_REQ_OU/set_var EASYRSA_REQ_OU/' ~/EasyRSA-$EasyRSA_Version/vars.example
	

	---------------------------------------
	Initiate the public key infrastructure
	---------------------------------------
	./easyrsa init-pki


	-----------------------------------------------------------
	Make up the public and private sides of an SSl certificate
	-----------------------------------------------------------
	./easyrsa build-ca nopass


	------------------------------------------------------------
	Copy ca.crt To openvpn
	------------------------------------------------------------
	sudo cp ~/EasyRSA-$EasyRSA_Version/pki/ca.crt /etc/openvpn/

<!----------Step 5-->
<span class="blue">Step 5 — Creating the Server Certificate, Key, and Encryption Files</span>

	-------------------------------------------------------------
	Create a private key for the server and a certificate request
	-------------------------------------------------------------
	./easyrsa gen-req server nopass


	----------------------------------------------------------------------
	Copy server.key To openvpn
	-----------------------------------------------------------------------
	sudo cp ~/EasyRSA-$EasyRSA_Version/pki/private/server.key /etc/openvpn/


	--------------------------------
	Sign request
	--------------------------------
	./easyrsa sign-req server server


	-----------------------------------------------------------------------
	Copy request Signed To openvpn
	-----------------------------------------------------------------------
	sudo cp ~/EasyRSA-$EasyRSA_Version/pki/issued/server.crt /etc/openvpn/
	

	------------------------------------
	Create a strong Diffie-Hellman key
	------------------------------------
	./easyrsa gen-dh


	----------------------------------------------------------------------------------------------
	Generate an HMAC signature to strengthen the server’s TLS integrity verification capabilities
	----------------------------------------------------------------------------------------------
	openvpn --genkey secret ta.key


	-------------------------------------------------------------
	Copy File to /etc/openvpn/ directory
	-------------------------------------------------------------
	sudo cp ~/EasyRSA-$EasyRSA_Version/ta.key /etc/openvpn/
	sudo cp ~/EasyRSA-$EasyRSA_Version/pki/dh.pem /etc/openvpn/

<!----------Step 6-->
<span class="blue">Step 6 — Athentication username/password File</span>

	-------------------------
	vim $op_auth
	-------------------------
	#!/bin/bash

	readarray -t lines < $1
	username=${lines[0]}
	password=${lines[1]}



	echo "not ok"
	exit 1
	-------------------------
	chmod +x $op_auth

<!----------Step 7-->
<span class="blue">Step 7 — Configuring the OpenVPN Service</span>

	-----------------------------------------------------------------------------
	Copying a sample OpenVPN configuration file into the configuration directory
	-----------------------------------------------------------------------------
	sudo cp /usr/share/doc/openvpn/examples/sample-config-files/server.conf /etc/openvpn/


	-----------------------------------------------------------------------------
	Change config file /etc/openvpn/server.conf
	-----------------------------------------------------------------------------
	sed -i '245i auth SHA256' /etc/openvpn/server.conf
	sed -i 's/dh dh2048.pem/dh dh.pem/' /etc/openvpn/server.conf
	sed -i 's/;user nobody/user nobody/' /etc/openvpn/server.conf
	sed -i 's/;group nogroup/group nogroup/' /etc/openvpn/server.conf
	sed -i 's/;push "redirect-gateway def1 bypass-dhcp"/push "redirect-gateway def1 bypass-dhcp"/' /etc/openvpn/server.conf
	sed -i 's/;push "dhcp-option DNS 208.67.222.222"/push "dhcp-option DNS 8.8.8.8"/' /etc/openvpn/server.conf
	sed -i 's/;push "dhcp-option DNS 208.67.220.220"/push "dhcp-option DNS 4.2.2.4"/' /etc/openvpn/server.conf
	sed -i "s/;local a.b.c.d/local $ip/" /etc/openvpn/server.conf
	sed -i "s/;proto tcp/proto $proto/" /etc/openvpn/server.conf
	sed -i 's/proto udp/;proto udp/' /etc/openvpn/server.conf
	sed -i "s/server 10.8.0.0 255.255.255.0/server $localip $subnet/" /etc/openvpn/server.conf
	sed -i "s/port 1194/port $port/" /etc/openvpn/server.conf
	sed -i 's/explicit-exit-notify 1/explicit-exit-notify 0/' /etc/openvpn/server.conf
	echo -e "\nscript-security 2" >> /etc/openvpn/server.conf
	echo "auth-user-pass-verify $op_auth via-file" >> /etc/openvpn/server.conf
	echo "username-as-common-name" >> /etc/openvpn/server.conf
	echo "duplicate-cn" >> /etc/openvpn/server.conf
	

<!----------Step 8-->
<span class="blue">Step 8 — Firewall</span>

	sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf
	iptables -t nat -A POSTROUTING -s $localip/24 -o enp1s0 -j MASQUERADE
	iptables -A INPUT -p $proto --dport $port -j ACCEPT
	iptables-save | uniq > /etc/iptables/rules.v4 

<!----------Step 9-->
<span class="blue">Step 9 — Starting and Enabling the OpenVPN Service</span>

	sudo systemctl enable openvpn@server
	sudo systemctl restart openvpn@server
	ping 192.168.5.1 -c 2

<!----------Step 10-->
<span class="blue">Step 10 — Creating the Client Configuration Infrastructure</span>

	-------------------------------------------
	Store client configuration files
	-------------------------------------------
	mkdir -p ~/client-configs/files
	cp /usr/share/doc/openvpn/examples/sample-config-files/client.conf ~/client-configs/base.conf


	------------------------------------------------------------------------
	Change config file ~/client-configs/base.conf
	------------------------------------------------------------------------
	sed -i "s/;proto tcp/proto $proto/" ~/client-configs/base.conf
	sed -i 's/proto udp/;proto udp/' ~/client-configs/base.conf
	sed -i "s/remote my-server-1 1194/remote $ip $port/" ~/client-configs/base.conf
	sed -i 's/;user nobody/user nobody/' ~/client-configs/base.conf
	sed -i 's/;group nogroup/group nogroup/' ~/client-configs/base.conf
	sed -i 's/ca ca.crt/#ca ca.crt/' ~/client-configs/base.conf
	sed -i 's/cert client.crt/#cert client.crt/' ~/client-configs/base.conf
	sed -i 's/key client.key/#key client.key/' ~/client-configs/base.conf
	sed -i 's/tls-auth ta.key 1/#tls-auth ta.key 1/' ~/client-configs/base.conf
	sed -i '117i auth SHA256' ~/client-configs/base.conf
	sed -i '118i key-direction 1' ~/client-configs/base.conf
	sed -i '119i ; script-security 2' ~/client-configs/base.conf
	sed -i '120i ; up /etc/openvpn/update-resolv-conf' ~/client-configs/base.conf
	sed -i '121i ; down /etc/openvpn/update-resolv-conf' ~/client-configs/base.conf
	sed -i '122i ; script-security 2' ~/client-configs/base.conf
	sed -i '123i ; up /etc/openvpn/update-systemd-resolved' ~/client-configs/base.conf
	sed -i '124i ; down /etc/openvpn/update-systemd-resolved' ~/client-configs/base.conf
	sed -i '125i ; down-pre' ~/client-configs/base.conf
	sed -i '126i ; dhcp-option DOMAIN-ROUTE .' ~/client-configs/base.conf
	echo "auth-user-pass" >> ~/client-configs/base.conf


	-------------------------------------------
	Compile your base configuration
	-------------------------------------------
	vim ~/client-configs/make_config.sh
	-------------------------------------------
	#!/bin/bash
	# First argument: Client identifier
	KEY_DIR=~/client-configs/keys
	OUTPUT_DIR=~/client-configs/files
	BASE_CONFIG=~/client-configs/base.conf
	cat ${BASE_CONFIG} \
		<(echo -e '<ca>') \
		${KEY_DIR}/ca.crt \
		<(echo -e '</ca>\n<cert>') \
		${KEY_DIR}/${1}.crt \
		<(echo -e '</cert>\n<key>') \
		${KEY_DIR}/${1}.key \
		<(echo -e '</key>\n<tls-auth>') \
		${KEY_DIR}/ta.key \
		<(echo -e '</tls-auth>') \
		> ${OUTPUT_DIR}/${1}.ovpn
	-------------------------------------------
	chmod 700 ~/client-configs/make_config.sh
	

	-------------------------------------------
	Store the client certificate and key folder
	-------------------------------------------
	mkdir -p ~/client-configs/keys
	chmod -R 700 ~/client-configs


	------------------------------------------------------------------------
	Copy the ca.crt and ta.key files to the client-configs/keys directory
	------------------------------------------------------------------------
	sudo cp /etc/openvpn/ca.crt ~/client-configs/keys/
	cp ~/EasyRSA-$EasyRSA_Version/ta.key ~/client-configs/keys/


<!-----------------------------------------------------------Create User-->
#### <span class="red">Create User</span> 

<span class="blue">Generate request For abd</span>

	cd ~/EasyRSA-$EasyRSA_Version/
	./easyrsa gen-req abd nopass
	cp pki/private/abd.key ~/client-configs/keys/


<span class="blue">Sign request For abd</span>

	./easyrsa sign-req client abd
	cp pki/issued/abd.crt ~/client-configs/keys/


<span class="blue">Create ovpn file For abd</span>

	cd ~/client-configs
	sudo ./make_config.sh abd
	sed -i "s/auth-user-pass/auth-user-pass \\/etc\\/openvpn\\/abd.conf/" ~/client-configs/files/abd.ovpn
	sed -i "`expr $(wc -l < $op_auth) - 2`i if [[ "\""\$username"\"" == "\""abd"\"" ]]; then\n\tif [[ "\""\$password"\"" == "\""123456"\"" ]]; then\n\t\techo "\""ok"\""\n\t\texit 0\n\tfi\nfi\n" $op_auth


<span class="blue">Transfer to local</span>

	scp root@108.61.175.212:~/client-configs/files/abd.ovpn ~/linux/vpn/abd.ovpn
	

<!----------------------------------------------------------- Client -->
#### <span class="red">Client</span>

<span class="blue">Install</span>

	sudo apt install openvpn
	sudo apt install openvpn-systemd-resolved

<span class="blue">Configuring Clients that use systemd-resolved</span>

	sudo vim  /etc/resolve.conf
	-------------------------------------
	nameserver 8.8.8.8
	options tun0

	nameserver 4.2.2.4
	options tun0

<span class="blue">Download  ovpn file</span>

	scp root@108.61.175.212:~/client-configs/files/abd.ovpn ~/linux/vpn/abd.ovpn

<span class="blue">Set User pass</span>

	sudo vim /etc/openvpn/abd.conf
	abd
	123456

<span class="blue">Connect</span>

	sudo openvpn --config ~/linux/vpn/abd.ovpn


<!----------------------------------------------------------- Alias -->
#### <span class="red">Alias</span>

vim ~/.bash_aliases

	alias opc='vim /etc/openvpn/server.conf'
	alias opa='vim /etc/openvpn/op_auth.sh'
	alias opr='sudo systemctl restart openvpn@server'
	alias ops='tail -f /var/log/syslog | grep ovpn-server'
	alias ops1='journalctl -xeu openvpn@server.service'
	alias ops2='sudo tail -f /var/log/openvpn/openvpn.log'
	alias ops3='cat /var/log/openvpn/openvpn-status.log | grep 192.168.5 '

source ~/.bash_aliases





sudo vim /etc/netplan/50-cloud-init.yaml

network:
    ethernets:
        eth0:
            dhcp4: no
            addresses:
              - 192.168.1.6/24
            gateway4: 192.168.1.130
            nameservers:
              addresses: [8.8.8.8, 4.2.2.4]
            optional: true
    version: 2

