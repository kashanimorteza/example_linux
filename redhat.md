

<div class="md3"></div>
<a href="#Basic">Basic</a> - 
<a href="#Tools">Tools</a> - 
<a href="#Programming">Programming</a> - 
<a href="#Software">Software</a>

<div class="md1"></div>

## <span class="red">Ubuntu</span>

#### <span class="blue">Basic</span>
	sudo apt update
	sudo apt upgrade

#### <span class="blue">Tools</span>

	sudo apt install software-properties-common
	sudo apt install apt-transport-https
	sudo apt install wget
	sudo apt install ca-certificates
	sudo apt-get install unixodbc-dev

#### <span class="blue">Network</span>

	sudo apt install net-tools
	sudo apt install iputils-ping

#### <span class="blue">Server</span>

SSH

	sudo apt install openssh-server

#### <span class="blue">Software</span>

Chrome

	cd ~/Downloads
	wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
	sudo apt install ./google-chrome-stable_current_amd64.deb





<div class="md0"></div>

## Centos

#### Basic

	dnf update
	dnf upgrade

	dnf clean all
	rm -fr /var/cache/dnf
	dnf -y upgrade
	dnf -y update

#### EPEL

	dnf -y install epel-release
	yum config-manager --set-enabled PowerTools

	dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

#### Network

	dnf install net-tools

#### ntfs
	dnf -y install ntfs-3g	
	
	wget https://tuxera.com/opensource/ntfs-3g_ntfsprogs-2017.3.23.tgz
	tar -zxvf ntfs-3g_ntfsprogs-2017.3.23.tgz
	cd ntfs-3g_ntfsprogs-2017.3.23
	./configure --prefix=/usr/local --disable-static
	make
	make install

	mkdir /media/sda1
	mount -t ntfs-3g /dev/sd11 /media/sda1
	umount /media/sda1

	vim /etc/fstab
	/dev/sda1 /media/sda1 ntfs-3g defaults 0 0

#### Software

Chrome

	curl -SLo chrome.rpm https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
	dnf localinstall chrome.rpm









<div class="md0"></div>

## Software

#### Telegram
	Download from telegram.com

	dnf config-manager --add-repo ppa:atareao/telegram
	dnf update 
	dnf install telegram

#### Xdman
	curl -SLo xdm.xz https://github.com/subhra74/xdm/releases/download/7.2.10/xdm-setup-7.2.10.tar.xz
	tar -xvf xdm.xz
	./install.sh
	
#### Openvpn
	dnf install openvpn

	git clone https://github.com/Nyr/openvpn-install.git
	cd ./openvpn-install
	chmod +x ./openvpn-install.sh
	./openvpn-install.sh

	sudo openvpn --config /home/morteza/Downloads/vpnbook/vpnbook-us2-udp25000.ovpn --auth-user-pass login.conf
	

	
#### f.lux
	sudo add-apt-repository ppa:nathan-renniewaldock/flux
	sudo apt-get update
	sudo apt-get install fluxgui
	sudo apt-get install fluxgui
	51.48N, 0.29W
	
#### Redshift
	sudo apt-get install libxcb1-dev libxcb-randr0-dev libx11-dev
	sudo apt-get install redshift redshift-gtk
	
#### putty
	sudo apt-get install putty

#### Grub Customizer
	sudo add-apt-repository ppa:danielrichter2007/grub-customizer
	sudo apt-get update
	sudo apt-get install grub-customizer
	

	
#### unetbootin
	sudo add-apt-repository ppa:gezakovacs/ppa 
	sudo apt-get update 
	sudo apt-get install unetbootin





#### Atom	
	curl -SLo atom.rpm https://atom.io/download/rpm
	dnf localinstall atom.rpm
	
	
#### VS Code
	---[ubuntu]
	Way 1:
	wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
	sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
	sudo apt update
	sudo apt install code

	Way 2:
	cd ~/Downloads
	wget https://az764295.vo.msecnd.net/stable/a0479759d6e9ea56afa657e454193f72aef85bd0/code_1.48.2-1598353430_amd64.deb	
	sudo apt install ./code_1.48.2-1598353430_amd64.deb
	







<!-----------------------------------------------------------Service----------------------------------------------------------->
<div class="md1"></div>

## Service

<!---------------------------------------Mikrotik-->
#### <span class="red">Mikrotik</span> 

	Download "CD Image" from Mikrotik
	Create Virtual box : linux | other linux 64 bit
	Default login  : admin | no password
	install wine and install WinBox
	




<!---------------------------------------ifenslave-->
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
                    
<!---------------------------------------Xrdp-->
#### <span class="red">Xrdp</span> 

	sudo apt update
	sudo apt upgrade
	sudo apt install xubuntu-desktop
	sudo apt install gnome-session
	sudo apt install xrdp
	sudo adduser morteza
	sudo adduser morteza xrdp 
	sudo ufw allow from 0.0.0.0/24 to any port 3389
	sudo ufw allow 3389
	sudo ufw reload

	sudo systemctl status xrdp
	sudo systemctl restart xrdp
	sudo ufw status

<!---------------------------------------OpenVpn-->
#### <span class="red">OpenVpn</span> 

<!----------General-->
<span class="blue">General</span>

<span class="green">Link</span> : https://www.digitalocean.com/community/tutorials/how-to-set-up-an-openvpn-server-on-ubuntu-18-04

<span class="green">Link</span> : https://docs.digitalocean.com/

<span class="green">library</span>

	OpenVpn : TLS/SSL VPN
	EasyRSA : is a CLI utility to build and manage a PKI CA With RSA Algorithm

<span class="green">Tag</span>

	VPN : Virtual Private Network
	SSL : Secure Socket Layer
	TLS : Transfer Layer Security
	RSA : Rivest Shamir Adleman
	CA  : certificate authority
	PKI : public key infrastructure for CA

<!----------Step 1-->
<span class="blue">Step 1 — Installing OpenVPN and EasyRSA</span>

	cd ~
	sudo apt update
	sudo apt install openvpn
	wget -P ~/ https://github.com/OpenVPN/easy-rsa/releases/download/v3.0.8/EasyRSA-3.0.8.tgz
	tar xvf EasyRSA-3.0.8.tgz
	cd ~/EasyRSA-3.0.8/

<!----------Step 2-->
<span class="blue">Step 2 — Configuring the EasyRSA Variables and Building the CA</span>

	RSA Config
	-----------------------------------------
	cp ~/EasyRSA-3.0.8/vars.example ~/EasyRSA-3.0.8/vars
	sed -i 's/#set_var EASYRSA_REQ_COUNTRY/set_var EASYRSA_REQ_COUNTRY/' ~/EasyRSA-3.0.8/vars
	sed -i 's/#set_var EASYRSA_REQ_PROVINCE/set_var EASYRSA_REQ_PROVINCE/' ~/EasyRSA-3.0.8/vars
	sed -i 's/#set_var EASYRSA_REQ_CITY/set_var EASYRSA_REQ_CITY/' ~/EasyRSA-3.0.8/vars
	sed -i 's/#set_var EASYRSA_REQ_ORG/set_var EASYRSA_REQ_ORG/' ~/EasyRSA-3.0.8/vars
	sed -i 's/#set_var EASYRSA_REQ_EMAIL/set_var EASYRSA_REQ_EMAIL/' ~/EasyRSA-3.0.8/vars
	sed -i 's/#set_var EASYRSA_REQ_OU/set_var EASYRSA_REQ_OU/' ~/EasyRSA-3.0.8/vars

	Initiate the public key infrastructure
	---------------------------------------
	./easyrsa init-pki

	Make up the public and private sides of an SSl certificate
	-----------------------------------------------------------
	./easyrsa build-ca nopass

	Copy ca.crt To openvpn
	------------------------------------------------------------
	sudo cp ~/EasyRSA-3.0.8/pki/ca.crt /etc/openvpn/

<!----------Step 3-->
<span class="blue">Step 3 — Creating the Server Certificate, Key, and Encryption Files</span>

	Create a private key for the server and a certificate request
	-------------------------------------------------------------
	./easyrsa gen-req server nopass

	Copy server.key To openvpn
	-------------------------------------------------------------
	sudo cp ~/EasyRSA-3.0.8/pki/private/server.key /etc/openvpn/

	Sign request
	---------------------------------------
	./easyrsa sign-req server server

	Copy request Signed To openvpn
	-------------------------------------------------------------
	sudo cp ~/EasyRSA-3.0.8/pki/issued/server.crt /etc/openvpn/
	
	Create a strong Diffie-Hellman key
	----------------------------------
	./easyrsa gen-dh

	Generate an HMAC signature to strengthen the server’s TLS integrity verification capabilities
	----------------------------------------------------------------------------------------------
	openvpn --genkey --secret ta.key

	Copy File to /etc/openvpn/ directory
	-------------------------------------
	sudo cp ~/EasyRSA-3.0.8/ta.key /etc/openvpn/
	sudo cp ~/EasyRSA-3.0.8/pki/dh.pem /etc/openvpn/

<!----------Step 4-->
<span class="blue">Step 4 — Generating a Client Certificate and Key Pair</span>

	Store the client certificate and key folder
	-------------------------------------------
	mkdir -p ~/client-configs/keys
	chmod -R 700 ~/client-configs

	Generate client1 request
	-------------------------------------------
	cd ~/EasyRSA-3.0.8/
	./easyrsa gen-req client1 nopass
	cp pki/private/client1.key ~/client-configs/keys/

	Sign request client1
	---------------------------------------
	./easyrsa sign-req client client1
	cp pki/issued/client1.crt ~/client-configs/keys/

	Copy the ca.crt and ta.key files to the client-configs/keys directory
	------------------------------------------------------------------------
	sudo cp /etc/openvpn/ca.crt ~/client-configs/keys/
	cp ~/EasyRSA-3.0.8/ta.key ~/client-configs/keys/

<!----------Step 5-->
<span class="blue">Step 5 — Configuring the OpenVPN Service</span>

	Copying a sample OpenVPN configuration file into the configuration directory
	-----------------------------------------------------------------------------
	sudo cp /usr/share/doc/openvpn/examples/sample-config-files/server.conf.gz /etc/openvpn/
	sudo gzip -d /etc/openvpn/server.conf.gz

	vim /etc/openvpn/server.conf
	----------------------------
	sed -i '245i auth SHA256' /etc/openvpn/server.conf
	sed -i 's/dh dh2048.pem/dh dh.pem/' /etc/openvpn/server.conf
	sed -i 's/;user nobody/user nobody/' /etc/openvpn/server.conf
	sed -i 's/;group nogroup/group nogroup/' /etc/openvpn/server.conf
	sed -i 's/;push "redirect-gateway def1 bypass-dhcp"/push "redirect-gateway def1 bypass-dhcp"/' /etc/openvpn/server.conf
	sed -i 's/;push "dhcp-option DNS 208.67.222.222"/push "dhcp-option DNS 208.67.222.222"/' /etc/openvpn/server.conf
	sed -i 's/;push "dhcp-option DNS 208.67.220.220"/push "dhcp-option DNS 208.67.220.220"/' /etc/openvpn/server.conf
	sed -i 's/;proto tcp/proto tcp/' /etc/openvpn/server.conf
	sed -i 's/proto udp/;proto udp/' /etc/openvpn/server.conf
	sed -i 's/server 10.8.0.0 255.255.255.0/server 192.168.0.0 255.255.255.0/' /etc/openvpn/server.conf
	sed -i 's/port 1194/port 443/' /etc/openvpn/server.conf
	sed -i 's/explicit-exit-notify 1/explicit-exit-notify 0/' /etc/openvpn/server.conf

<!----------Step 6-->
<span class="blue">Step 6 — Adjusting the Server Networking Configuration</span>

	Ip Forward
	--------------------
	sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf

	Config UFW
	-------------------------------
	sed -i '10i # START OPENVPN RULES\n# NAT table rules\n*nat\n:POSTROUTING ACCEPT [0:0]\n# Allow traffic from OpenVPN client to enp1s0 (change to the interface you discovered)\n-A POSTROUTING -s 192.168.0.0/24 -o enp1s0 -j MASQUERADE\nCOMMIT\n# END OPENVPN RULE' /etc/ufw/before.rules

	Allow forwarded packets by default as well
	-------------------------------------------
	sed -i 's/DEFAULT_FORWARD_POLICY="DROP"/DEFAULT_FORWARD_POLICY="ACCEPT"/' /etc/default/ufw

	Allow traffic to OpenVPN
	-------------------------------------------
	sudo ufw allow 443/tcp
	sudo ufw allow OpenSSH

	Restart UFW
	-------------------------------------------
	sudo ufw disable
	sudo ufw enable

<!----------Step 7-->
<span class="blue">Step 7 — Starting and Enabling the OpenVPN Service</span>

	Start the OpenVPN server
	-------------------------------------------
	sudo systemctl enable openvpn@server
	sudo systemctl start openvpn@server
	sudo systemctl status openvpn@server
	ping 192.168.0.1 -c 3

<!----------Step 8-->
<span class="blue">Step 8 — Creating the Client Configuration Infrastructure</span>

	Store client configuration files
	-------------------------------------------
	mkdir -p ~/client-configs/files
	cp /usr/share/doc/openvpn/examples/sample-config-files/client.conf ~/client-configs/base.conf
	sed -i 's/;proto tcp/proto tcp/' ~/client-configs/base.conf
	sed -i 's/proto udp/;proto udp/' ~/client-configs/base.conf
	sed -i 's/remote my-server-1 1194/remote 104.238.170.252 443/' ~/client-configs/base.conf
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

	Compile your base configuration
	--------------------------------
	vim ~/client-configs/make_config.sh

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

	chmod 700 ~/client-configs/make_config.sh

<!----------Step 9-->
<span class="blue">Step 9 — Generating Client Configurations</span>

	cd ~/client-configs
	sudo ./make_config.sh client1
	ls ~/client-configs/files

	Transfer ~/client-configs/files/client1.ovpn to local

<!----------Step 10-->
<span class="blue">Step 10 — Installing the Client Configuration</span>

	sudo apt update
	sudo apt install openvpn

	Configuring Clients that use systemd-resolved
	----------------------------------------------
	cat /etc/resolv.conf
	sudo apt install openvpn-systemd-resolved

	configure the client 
	----------------------
	vim ~/client1.ovpn

	script-security 2
	up /etc/openvpn/update-systemd-resolved
	down /etc/openvpn/update-systemd-resolved
	down-pre
	dhcp-option DOMAIN-ROUTE .

	sudo openvpn --config client1.ovpn	

<!----------Step 11-->
<span class="blue">Step 11 — Create user</span>

	cd ~/EasyRSA-3.0.8/
	op=morteza
	./easyrsa gen-req $op nopass
	cp ./pki/private/$op.key ~/client-configs/keys/
	./easyrsa sign-req client $op
	cp ./pki/issued/$op.crt ~/client-configs/keys/
	sudo ~/client-configs/make_config.sh $op
	ls ~/client-configs/files
	cat ~/client-configs/files/$op.ovpn 