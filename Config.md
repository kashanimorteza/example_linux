<div class="md3">
<a href="#config-file">Config file</a> - 
<a href="#boot">Boot</a> - 
<a href="#connection">Connection</a> -
<a href="#device">Device</a> -
<a href="#user">User</a> - 
<a href="#network">Network</a> - 
<a href="#service">Service</a>
</div>

<!----------------------------------------------------------------------------------[SSH]-->
<div class="md5"></div>

## SSH

#### <span class="red">Connect to server with private key</span>

<span class="blue">Create key</span>

	ssh-keygen -t rsa -b 1024
	ssh root@108.61.175.212 mkdir -p .ssh
	cat .ssh/id_rsa.pub | ssh root@108.61.175.212 'cat >> .ssh/authorized_keys'

<span class="blue">Add key to config</span>

vim ~/.ssh/config
	
    Host 108.61.175.212
        PreferredAuthentications publickey
        IdentityFile ~/.ssh/id_rsa.key



<!-----------------------------------------------------------General----------------------------------------------------------->
<div class="md1"></div>

## General

	sudo timedatectl set-timezone UTC


<!-----------------------------------------------------------Config File-->
#### <span class="red">Config File</span>

<table><tbody>
<tr><td colspan="2" align="center" bgcolor="D1ECCF">Config Files</td></tr>
<tr><td rowspan="1">Libreary path</td><td>/etc/ld.so.conf</td></tr>
<tr><td rowspan="1">Libreary name and phth of cash</td><td>/etc/ld.so.cache</td></tr>
<tr><td rowspan="1">List Of Packages</td><td>/etc/apt/sources.list</td></tr>
</tbody></table>


<!-----------------------------------------------------------SSH-->




<!-----------------------------------------------------------Boot----------------------------------------------------------->
<div class="md1"></div>

## Boot

<!---------------------------------------Add Menu to grub-->
#### <span class="red">Add Menu to grub</span>
	Add these lines to filr /etc/grub.d/40_custom :
	---------------------------------------------------
	menuentry "Install Linux Ubuntu-18.04.2" {
	set isofile="/Linux-Ubuntu-18.04.2-desktop-amd64.iso"
	loopback loop (hd1,2)$isofile
	linuxefi (loop)/casper/vmlinuz boot=casper iso-scan/filename=${isofile} quiet splash
	initrdefi (loop)/casper/initrd
	}

	Run this command : update-grub

<!---------------------------------------Reinstall BootLoader-->
#### <span class="red">Reinstall BootLoader</span>	
	sudo mkdir /mnt/ubuntu <br>
	sudo mount /dev/sda1 /mnt/ubuntu <br>
	sudo grub-install --boot-directory=/mnt/ubuntu/boot /dev/sda <br>








<!-----------------------------------------------------------Device----------------------------------------------------------->
<div class="md1"></div>

## Device

<!---------------------------------------Disable Touchpad-->
#### <span class="red">Disable Touchpad</span>
	echo 'xinput --disable 15' >> $HOME/.profile




<!-----------------------------------------------------------User----------------------------------------------------------->
<div class="md1"></div>

## User

<!---------------------------------------Enable root user-->
#### <span class="red">Enable root user</span>
    sudo passwd root
    usermod -U root
    su root

<!---------------------------------------Disable sudo pass-->
#### <span class="red">Disable sudo pass</span>
	
	sudo vim /etc/sudoers
	------------------------------
	#includedir /etc/sudoers.d
	ALL     ALL = (ALL) NOPASSWD: ALL



<!-----------------------------------------------------------Network----------------------------------------------------------->
<div class="md1"></div>

## Network

<!---------------------------------------Set Static Ip-->
#### <span class="red">Set Static Ip</span>

<span class="blue">Way 1</span>

	sudo vi /etc/network/interfaces
	-----------------------------------------
	auto enp3s0
	iface enp3s0 inet static
	address 192.168.1.2
	netmask 255.255.255.0
	network 192.168.1.0
	gateway 192.168.1.1
	dns-nameservers 8.8.8.8 4.2.2.4
	dns-search domain.local

	auto enp3s0:0
	iface enp3s0:0 inet static
	address 192.168.2.2
	netmask 255.255.255.0
	network 192.168.2.0
	gateway 192.168.2.1
	dns-nameservers 8.8.8.8 4.2.2.4
	dns-search domain.local


<span class="blue">Way 2</span>

	sudo vim /etc/netplan/1-network-manager-all.yaml
	-------------------------------------------------
	# Let NetworkManager manage all devices on this system
	network:
	version: 2
	renderer: NetworkManager
	ethernets:
		enp3s0:
		dhcp4: no
		addresses: [192.168.1.110/24, ]
		gateway4: 192.168.1.1
		nameservers:
		addresses: [8.8.8.8, 4.2.2.4]

	sudo netplan apply
	ip addr show dev enp3s0

<!---------------------------------------Virtual interface-->
#### <span class="red">Virtual interface</span>ifconfig
	sudo lsmod | grep dummy
	sudo modprobe dummy

	sudo ip link add enp3s1 type dummy
	ip link show enp3s1
	sudo ifconfig enp3s1 hw ether C8:D7:4A:4E:47:50
	sudo ip addr add 192.168.2.110/24 brd + dev enp3s1 label enp3s1
	sudo ip link set dev enp3s1 up
	ip a

	sudo ip addr del 192.168.1.100/24 brd + dev eth0 label eth0:0
	sudo ip link delete eth0 type dummy
	sudo rmmod dummy

	auto enp3s0
	iface enp3s0 inet static
			address 192.168.1.11
			netmask 255.255.255.0
			gateway 192.168.1.1
			dns-nameservers 8.8.8.8 4.2.2.4
			dns-search domain.local


