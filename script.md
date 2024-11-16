

<!----------------------------------------------------------------------------------[Pages]-->
[Linux](index.md) |
[Debian](debian.md) |
[RedHat](redhat.md) |
[Mikrotik](mikrotik.md) |
[Config](config.md) |
[Script](script.md) |
[VPN](vpn.md) |
[Cryptography](cryptography.md)



<!----------------------------------------------------------------------------------[subject]-->
<a href="#connect-to-server">Connect To Server</a> - 
<a href="#tunnel">Tunnel</a> - 
<a href="#openvpn-connection">OpenVpn Connection</a> - 
<a href="#openvpn-server">OpenVpn Server</a> - 



<!----------------------------------------------------------------------------------[ssh]-->
<div class="md5"></div>

## Connect to server

#### <span class="red">Create Script</span>

vim ~/s

	#!/bin/sh

	srv=$london

	if [ "$srv" = "london" ];
	then
		echo 'Connecting to Server London ...'
		ssh root@108.61.175.212
	fi

	if [ "$srv" = "test" ];
	then
		echo 'Connecting to Server test ...'
		ssh root@95.179.228.159
	fi

chmod +x ~/s

#### <span class="red">Add Shortcut</span>

vim ~/.bash_aliases

	#-------------------------------------------------- [ server ]
	alias sl='~/s london'
	alias st='~/s test'

#### <span class="red">Run command</span>

	morteza@laptop:~$ sl
	morteza@laptop:~$ st







<!----------------------------------------------------------------------------------[Openvpn Connection]-->
<div class="md1"></div>

## OpenVpn Connection

#### <span class="red">Connect</span>

vim ~/ops

	nohup sudo openvpn --config ~/linux/vpn/uk_london.ovpn & exit

chmod +x ~/ops

#### <span class="red">Disconnect</span>

vim ~/opk

	ps -ef | grep "sudo openvpn --config /home/morteza/linux/vpn/uk_london.ovpn" | grep -v grep | sudo awk -F" " 'system("kill  "$2"")'

chmod +x ~/opk

#### <span class="red">Check Connection</span>

vim ~/opc

	#!/bin/bash

	STR=$(ifconfig | grep tun)
	SUB='tun0'
	if [[ "$STR" == *"$SUB"* ]]; then
			vpn="true"
	fi

	if ping -q -c 1 -W 1 192.168.1.1 >/dev/null; then
		if ping -q -c 1 -W 1 8.8.8.8 >/dev/null; then
			if [ "$vpn" = "true" ];then
					echo "VPN Connected"
			else
					echo "VPN NOT Connected"
					sudo openvpn --config uk_london.ovpn
			fi
		else
			sudo killall openvpn
			echo "Adsl disconnected"
		fi
	else
		echo "Modem disconnected"
		sudo killall openvpn
	fi

chmod +x ~/opc


#### <span class="red">Add Schedule</span>

sudo echo "* * * * * ubuntu ~/opc" >>  /etc/crontab

#### <span class="red">Add Shortcut</span>

vim ~/.bash_aliases

	#-------------------------------------------------- [ OpenVpn ]
	alias ops='~/ops'
	alias opc='~/opc'
	alias opk='~/opk'

#### <span class="red">Run command</span>

	morteza@laptop:~$ ops
	morteza@laptop:~$ opc
	morteza@laptop:~$ opk



<!----------------------------------------------------------------------------------[Create Openvpn]-->
<div class="md1"></div>

## OpenVPN Server

<!-----------------------------------------------------------Create Server Script-->
#### <span class="red">Create Server Script</span> 

vim ~/op_cs.sh 

	#!/bin/sh

	echo "-------------------------------- [Step 1 _ Variable] --------------------------------"
	EasyRSA_Version=$1
	proto=$2
	ip=$3
	port=$4
	localip=$5
	subnet=$6
	op_auth=/etc/openvpn/op_auth.sh
	echo "config : $EasyRSA_Version $proto $ip $port $localip $subnet $op_auth"

	echo "-------------------------------- [Step 2 _ Clear] --------------------------------"
	sudo rm -fr EasyRSA-$EasyRSA_Version
	sudo rm -fr EasyRSA-$EasyRSA_Version.tgz
	sudo rm -fr ~/client-configs
	sudo rm -fr ~/client-configs/keys
	sudo rm -fr $op_auth
	
	echo "-------------------------------- [Step 3 _ Installing OpenVPN and EasyRSA] --------------------------------"
	wget -P ~/ https://github.com/OpenVPN/easy-rsa/releases/download/v$EasyRSA_Version/EasyRSA-$EasyRSA_Version.tgz
	tar xvf EasyRSA-*
	cd ~/EasyRSA-*/

	echo "-------------------------------- [Step 4 — Configuring the EasyRSA Variables and Building the CA] --------------------------------"	
	sed -i 's/#set_var EASYRSA_REQ_COUNTRY/set_var EASYRSA_REQ_COUNTRY/' ~/EasyRSA-$EasyRSA_Version/vars.example
	sed -i 's/#set_var EASYRSA_REQ_PROVINCE/set_var EASYRSA_REQ_PROVINCE/' ~/EasyRSA-$EasyRSA_Version/vars.example
	sed -i 's/#set_var EASYRSA_REQ_CITY/set_var EASYRSA_REQ_CITY/' ~/EasyRSA-$EasyRSA_Version/vars.example
	sed -i 's/#set_var EASYRSA_REQ_ORG/set_var EASYRSA_REQ_ORG/' ~/EasyRSA-$EasyRSA_Version/vars.example
	sed -i 's/#set_var EASYRSA_REQ_EMAIL/set_var EASYRSA_REQ_EMAIL/' ~/EasyRSA-$EasyRSA_Version/vars.example
	sed -i 's/#set_var EASYRSA_REQ_OU/set_var EASYRSA_REQ_OU/' ~/EasyRSA-$EasyRSA_Version/vars.example
	./easyrsa init-pki
	./easyrsa build-ca nopass
	sudo cp ~/EasyRSA-$EasyRSA_Version/pki/ca.crt /etc/openvpn/

	echo "-------------------------------- [Step 5 — Creating the Server Certificate, Key, and Encryption Files] --------------------------------"
	./easyrsa gen-req server nopass
	sudo cp ~/EasyRSA-$EasyRSA_Version/pki/private/server.key /etc/openvpn/
	./easyrsa sign-req server server
	sudo cp ~/EasyRSA-$EasyRSA_Version/pki/issued/server.crt /etc/openvpn/
	./easyrsa gen-dh
	openvpn --genkey secret ta.key
	sudo cp ~/EasyRSA-$EasyRSA_Version/ta.key /etc/openvpn/
	sudo cp ~/EasyRSA-$EasyRSA_Version/pki/dh.pem /etc/openvpn/

	echo "-------------------------------- [Step 6 — Athentication username/password File] --------------------------------"

	sudo echo '#!/bin/bash

	readarray -t lines < $1
	username=${lines[0]}
	password=${lines[1]}



	echo "not ok"
	exit 1
	' > $op_auth

	chmod +x $op_auth

	echo "-------------------------------- [Step 7 — Configuring the OpenVPN Service] --------------------------------"
	sudo echo "
	dev tun
	local $ip
	proto $proto
	port $port
	server $localip $subnet
	auth SHA256
	cipher AES-256-CBC
	ca ca.crt
	cert server.crt
	key server.key 
	dh dh.pem
	ifconfig-pool-persist /var/log/openvpn/ipp.txt
	push "\""redirect-gateway def1 bypass-dhcp"\""
	push "\""dhcp-option DNS 8.8.8.8"\""
	push "\""dhcp-option DNS 4.2.2.4"\""
	keepalive 10 120
	tls-auth ta.key 0
	user nobody
	persist-key
	persist-tun
	status /var/log/openvpn/openvpn-status.log
	verb 3
	explicit-exit-notify 0
	script-security 2
	auth-user-pass-verify $op_auth via-file
	username-as-common-name
	duplicate-cn
	" >  /etc/openvpn/server.conf

	echo "-------------------------------- [Step 8 — Firewall] --------------------------------"

	sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf
	iptables -t nat -A POSTROUTING -s $localip/24 -o enp1s0 -j MASQUERADE
	iptables -A INPUT -p $proto --dport $port -j ACCEPT
	iptables-save | uniq > /etc/iptables/rules.v4 

	echo "-------------------------------- [Step 9 — Starting and Enabling the OpenVPN Service] --------------------------------"
	sudo systemctl enable openvpn@server
	sudo systemctl restart openvpn@server

	echo "-------------------------------- [Step 10 — Creating the Client Configuration Infrastructure] --------------------------------"
	sudo mkdir -p ~/client-configs/files
	sudo echo "
	client
	dev tun
	proto $proto
	remote $ip $port
	auth SHA256
	cipher AES-256-CBC
	resolv-retry infinite
	nobind
	user nobody
	persist-key
	persist-tun
	remote-cert-tls server
	key-direction 1
	verb 3
	auth-user-pass
	" >  ~/client-configs/base.conf

	sudo echo '#!/bin/bash

	# First argument: Client identifier

	KEY_DIR=~/client-configs/keys
	OUTPUT_DIR=~/client-configs/files
	BASE_CONFIG=~/client-configs/base.conf

	cat ${BASE_CONFIG} \
		<(echo -e "<ca>") \
		${KEY_DIR}/ca.crt \
		<(echo -e "</ca>\n<cert>") \
		${KEY_DIR}/${1}.crt \
		<(echo -e "</cert>\n<key>") \
		${KEY_DIR}/${1}.key \
		<(echo -e "</key>\n<tls-auth>") \
		${KEY_DIR}/ta.key \
		<(echo -e "</tls-auth>") \
		> ${OUTPUT_DIR}/${1}.ovpn' > ~/client-configs/make_config.sh

	chmod 700 ~/client-configs/make_config.sh

	echo "-------------------------------- [Step 11 — Generating a Client Certificate and Key Pair] --------------------------------"
	mkdir -p ~/client-configs/keys
	chmod -R 700 ~/client-configs
	sudo cp /etc/openvpn/ca.crt ~/client-configs/keys/
	cp ~/EasyRSA-$EasyRSA_Version/ta.key ~/client-configs/keys/	

chmod +x ./op_cs.sh

./op_cs.sh 3.1.0 tcp 108.61.175.212 443 192.168.5.0 255.255.255.0

<!-----------------------------------------------------------Create User Script-->
#### <span class="red">Create User Script</span> 

vim ~/op_cu.sh

	#!/bin/sh

	EasyRSA_Version=$1
	user=$2
	pass=$3
	op_auth=/etc/openvpn/op_auth.sh
	echo "config : $EasyRSA_Version $user $pass $op_auth"

	cd ~/EasyRSA-$EasyRSA_Version/
	./easyrsa gen-req $user nopass
	cp pki/private/$user.key ~/client-configs/keys/
	./easyrsa sign-req client $user
	cp pki/issued/$user.crt ~/client-configs/keys/
	cd ~/client-configs
	sudo ./make_config.sh $user

	sed -i "s/auth-user-pass/auth-user-pass \\/etc\\/openvpn\\/$user.conf/" ~/client-configs/files/$user.ovpn

	sed -i "`expr $(wc -l < $op_auth) - 2`i if [[ "\""\$username"\"" == "\""$user"\"" ]]; then\n\tif [[ "\""\$password"\"" == "\""$pass"\"" ]]; then\n\t\techo "\""ok"\""\n\t\texit 0\n\tfi\nfi\n" $op_auth

chmod +x ./op_cu.sh

./op_cu.sh 3.1.0 abd 123456

<!-----------------------------------------------------------Delete User Script-->
#### <span class="red">Delete User Script</span>

vim ~/op_du.sh 

	#!/bin/sh

	EasyRSA_Version=$1
	user=$2

	rm -fr ~/EasyRSA-$EasyRSA_Version/pki/private/$user.key
	rm -fr ~/EasyRSA-$EasyRSA_Version/pki/issued/$user.crt
	rm -fr ~/client-configs/keys/$user.key
	rm -fr ~/client-configs/keys/$user.crt
	rm -fr ~/client-configs/files/$user.ovpn	

chmod +x ./op_du.sh

./op_du.sh 3.1.0 abd



<!-----------------------------------------------------------Network----------------------------------------------------------->
<div class="md1"></div>

## Create Partition
	#!/bin/bash

	hdd="sdd"

	sudo fdisk /dev/$hdd << EOF
	g
	n


	+25G
	n


	+50M
	w
	EOF
	exit 0
	
	
	
	
<div class="md1"></div>





## Format Partition
	#!/bin/bash

	hdd="sdd"

	sudo mkfs.ext4 -F /dev/"$hdd"1
	sudo mkfs.vfat -F 32 /dev/"$hdd"2




<div class="md1"></div>





## Mount Partition
	#!/bin/bash

	hdd="sdd"

	sudo mkdir /media/"$hdd"1
	sudo mkdir /media/"$hdd"2

	sudo mount -t ext4 /dev/"$hdd"1 /media/"$hdd"1/
	sudo mount /dev/"$hdd"2 /media/"$hdd"2/
	
	
	
	
<div class="md1"></div>




## Copy ISO
	#!/bin/bash

	hdd="sdd"

	sudo cp -r /media/sda4/Users/Morteza/Desktop/Computer/. /media/"$hdd"1

	sudo cp -r /media/"$hdd"1/NewGrub/EFI /media/"$hdd"2

	
	
	
	
<div class="md1"></div>




## Grub Config
	set default="1"

	function load_video {
	  insmod efi_gop
	  insmod efi_uga
	  insmod video_bochs
	  insmod video_cirrus
	  insmod all_video
	}

	load_video
	set gfxpayload=keep
	insmod gzio
	insmod part_gpt
	insmod ext2

	set timeout=60

	search --no-floppy --set=root -l 'Fedora-S-dvd-x86_64-31'



	menuentry "Install --- Centos" {

		set isofile=/linux-centos.iso
		loopback loop3 (hd0,5)$isofile
		linuxefi (loop3)/images/pxeboot/vmlinuz inst.repo=hd:sda5 quiet
		initrdefi (loop3)/images/pxeboot/initrd.img
	}
	menuentry "Install --- Ubuntu" {
		
		set isofile=/linux-ubuntu.iso
		loopback loop4 (hd0,5)$isofile
		linuxefi (loop4)/casper/vmlinuz boot=casper iso-scan/filename=${isofile} quiet splash
		initrdefi (loop4)/casper/initrd
	}
	menuentry "Install --- Ubuntu Xfce" {
		
		set isofile=/linux-ubuntu-xfce.iso
		loopback loop5 (hd0,5)$isofile
		linuxefi (loop5)/casper/vmlinuz boot=casper iso-scan/filename=${isofile} quiet splash
		initrdefi (loop5)/casper/initrd
	}




<div class="md1"></div>




## openvpn

	#!/bin/bash
	
	sudo openvpn --config /home/morteza/Downloads/vpnbook/vpnbook-us2-udp25000.ovpn --auth-user-pass /home/morteza/Downloads/vpnbook/login.conf








<div class="md0"></div>

## Create Service

sudo vim /etc/systemd/system/forex-downloaddata.service

	[Unit]
	Description=forex download data
	[Service]
	User=morteza
	WorkingDirectory=/home/morteza/forex-download-data
	ExecStart=/home/morteza/forex-download-data/linux-service
	SuccessExitStatus=143
	TimeoutStopSec=10
	Restart=on-failure
	RestartSec=60
	[Install]
	WantedBy=multi-user.target

sudo vim /home/morteza/forex-download-data/linux-service

	#!/bin/sh

	python3.8 main.py

sudo chmod 755 /home/morteza/forex-download-data/linux-service

Start Service

	sudo systemctl daemon-reload
	
	sudo systemctl enable forex-downloaddata
	sudo systemctl disable forex-downloaddata
	
	sudo systemctl is-enabled forex-downloaddata
	sudo systemctl is-active forex-downloaddata

	sudo systemctl start forex-downloaddata
	sudo systemctl stop forex-downloaddata
	sudo systemctl restart forex-downloaddata
	sudo systemctl status forex-downloaddata

Check Service Log 

	sudo journalctl --unit=forex-downloaddata
	sudo journalctl -f -n 10 -u forex-downloaddata
	sudo journalctl -f -u forex-downloaddata



## Remode desktop

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





#### <span class="blue">Connection</span>

	ssh root@192.168.1.1







tun2socks
-------------------------------------------------------------------------------------------

source
--------------------------------------------------------
https://github.com/xjasonlyu/tun2socks

install
--------------------------------------------------------
git clone git@github.com:xjasonlyu/tun2socks.git
cd tun2socks
make tun2socks
sudo cp ./build/tun2socks /usr/local/bin


config
--------------------------------------------------------
sudo ip route del default
sudo ip route add 108.61.175.212 via 192.168.1.1 dev wlp2s0

ping 108.61.175.212
ssh -fCqND 127.0.0.1:8082 root@108.61.175.212

sudo ip tuntap add mode tun dev tun0
sudo ip addr add 198.18.0.1/15 dev tun0
sudo ip link set dev tun0 up

sudo ip route add default via 198.18.0.1 dev tun0 metric 1
sudo ip route add default via 192.168.1.1 dev wlp2s0 metric 10

sudo tun2socks -device tun0 -proxy socks5://127.0.0.1:8082 -interface wlp2s0