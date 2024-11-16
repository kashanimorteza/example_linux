<!----------------------------------------------------------------------------------[Diagram]-->
<div align="left"><img src="https://github.com/kashanimorteza/linux/blob/main/diagram/linux.jpeg"></div>

<!----------------------------------------------------------------------------------[Subject]-->
<a href="#basic">Basic</a> - 
<a href="#link">Link</a> - 
<a href="#note">Note</a>

<a href="#boot">Boot</a> - 
<a href="#kernel">Kernel</a> - 
<a href="#init">Init</a> - 
<a href="#device-manager--udevd">udevd</a> - 
<a href="#event-logging--journald">journald</a> -
<a href="#user-manager--logind">logind</a> -
<a href="#network-manager--networkd">networkd</a> -
<a href="#time-manager--timedated">timedated</a> -
<a href="#boot-manager--systemd-boot">Systemd-boot</a> -
<a href="#security--iptables">iptables</a>

<a href="#disk">Disk</a> -
<a href="#ram">Ram</a> -
<a href="#file">File</a>

<a href="#runlevel">Runlevel</a> -
<a href="#shell">Shell</a> -
<a href="#variable">Variable</a> - 
<a href="#process">Process</a>

<a href="#library">Library</a> - 
<a href="#package-manager-system-pms">PMS</a> -
<a href="#virtualization">Virtualization</a> -
<a href="#graphic">Graphic</a> 



<!-----------------------------------------------------------Basic----------------------------------------------------------->
<div class="md3"></div>

## Basic

<!---------------------------------------Resource-->
#### <span class="red">Resource</span>
<table border="0" align="center" valign="top"><tbody><tr>
    <!-- td 1 -->
    <td valign="top">
        <table><tbody>
            <tr><td align="center" bgcolor="D1ECCF">Link</td><td align="center" bgcolor="D1ECCF">Description</td></tr>        
            <tr><td align="center"><a href="http://www.kernel.org/" target="_blank">kernel.org</a></td><td>Linux Kernel</td></tr>
            <tr><td align="center"><a href="http://www.gnu.org/" target="_blank">gnu</a></td><td>Linux Kernel</td></tr>
            <tr><td align="center"><a href="http://www.linux.com/" target="_blank">linux</a></td><td>Linux Kernel</td></tr>
            <tr><td align="center"><a href="http://Opensource.com" target="_blank">Opensource</a></td><td>Linux Kernel</td></tr>
            <tr><td align="center"><a href="http://x.org " target="_blank">x</a></td><td>Linux Kernel</td></tr>
            <tr><td align="center"><a href="http://kde.org " target="_blank">kde</a></td><td>Linux Kernel</td></tr>
            <tr><td align="center"><a href="http://gnome.org " target="_blank">gnome</a></td><td>Linux Kernel</td></tr>
        </tbody></table>
    </td>
    <!-- td 2 -->
    <td valign="top">
        <table><tbody>
            <tr><td align="center" bgcolor="D1ECCF">Link</td><td align="center" bgcolor="D1ECCF">Description</td></tr>
            <tr><td align="center"><a href="http://www.distrowatch.com/" target="_blank">distrowatch</a></td><td>Linux Kernel</td></tr>
            <tr><td align="center"><a href=" http://Linuxalt.com" target="_blank">Linuxalt</a></td><td>Linux Kernel</td></tr>
            <tr><td align="center"><a href="http://putty.org" target="_blank">putty</a></td><td>Linux Kernel</td></tr>
            <tr><td align="center"><a href="http://openwrt.org" target="_blank">openwrt</a></td><td>Linux Kernel</td></tr>
            <tr><td align="center"><a href="https://alpinelinux.org/downloads/" target="_blank">alpinelinux</a></td><td>Linux Kernel</td></tr>
        </tbody></table>
    </td>
    <!-- td 3 -->
    <td valign="top">
        <table><tbody>
            <tr><td align="center" bgcolor="D1ECCF">Link</td><td align="center" bgcolor="D1ECCF">Description</td></tr>
            <tr><td align="center"><a href="https://linux1st.com/archives.html" target="_blank">linux1st.com</a></td><td> Jadi linux book </td></tr>
        </tbody></table>
    </td>
</tr></tbody></table>


<!---------------------------------------Concept-->
#### <span class="red">Concept</span>
    GNU limux OS = Linux kernel + GNU Software
    Hardware | Firmware | Software
    PCI | USB | GPIO | 

<!---------------------------------------History-->
#### <span class="red">History</span>
    Multics - Unix - Plan 9 - MINIX - BSD

<!---------------------------------------Character-->
#### <span class="red">Character</span>
    Linus Torvalds - Richard Stallman

<!---------------------------------------Organization-->
#### <span class="red">Organization</span>
    GNU - FSF  -  OSI  -  CC  -  RFC

<!---------------------------------------Standard-->
#### <span class="red">Standard</span>
    Posix | Ventory

<!---------------------------------------Licence & Software Types-->
#### <span class="red">Licence & Software Types</span>
    Commercial  -  Shareware  -  Freeware  -  Open Source
    GPL

<!---------------------------------------Evidence-->
#### <span class="red">Evidence</span>
<div><span class="blue">Certification</span> : <span>LPI | LPIC-1 | LPIC-2 | LPIC-3</span></div>
<div><span class="blue">Wetsite</span> : <span>
<a href="http://Lpi.org" target="_blank">Lpi</a> - <a href="http://lpimarketplace.com" target="_blank">lpimarketplace</a> - <a href="http://Gratisexam.com" target="_blank">Gratisexam</a> - <a href="http://ibm.com/developerworks/library/l-lpic1-map/" target="_blank">ibm</a>
</span></div>



<!-----------------------------------------------------------Boot----------------------------------------------------------->
<div class="md1"></div>

## Boot

<!---------------------------------------General-->
#### <span class="red">General</span> 
<table><tbody>
<tr><td align="center" bgcolor="D1ECCF">Subject</td><td align="center" bgcolor="D1ECCF">Description</td></tr>
<tr><td align="center">Boot Steps</td><td>IC PC Register | POST | Bios/UEFI | /GPT | BootLoader | Kernel | Init</td></tr>
<tr><td align="center">Firmware</td><td>Bios | UEFI</td></tr>
<tr><td align="center">Boot Loader </td><td> Grub </td></tr>
</tbody></table>

<!---------------------------------------UEFI-->
#### <span class="red">UEFI</span> 

    Check     : [ -d /sys/firmware/efi ] && echo UEFI || echo BIOS
    Partition : /boot/efi
    File      : /sys/efi

<!---------------------------------------Grub-->
#### <span class="red">Grub</span> 
<table><tbody>
<tr><td >Work</td><td>Kernel | initrmfs</td></tr>
<tr><td>Config</td><td>/boot/grub/grub.cfg | /etc/defaults/grub | /etc/grub.d/</td></tr>
</tbody></table> 
grub-mkconfig > /boot/grub/grub.cfg

<!---------------------------------------Log-->
#### <span class="red">Log</span>
Kernel ring buffer : کرنل تو پروسه بوت شدن لاگ هاشو اینجا مینویسه تا یادش نره چون هنوز درایور دیسک لود نشده 

dmesg

cat /var/log/dmesg

cat /var/log/boot.log

journalctl -b



<!-----------------------------------------------------------Kernel----------------------------------------------------------->
<div class="md1"></div>

## Kernel
<table><tbody>
<tr>
<td >Layer 3</td>
<td >System Call Interfaces (SCI)</td>
<td>stat, splice, dup, ...</td>
</tr>
</tbody></table>
<table><tbody>
<tr>
<td >Layer 2</td>
<td >Process Scheduling</td>
<td >IPCSub</td>
<td >Memory Management</td>
<td >VirtualFiles</td>
<td >Network</td>
</tr>
</tbody></table>
<table><tbody>
<tr>
<td rowspan="2">Layer 1</td>
<td >Other Subsystems: </td>
<td >ALSA, DRI, evdev, LVM, Device mapper, Linux Network Scheduler, Netfilter</td>
</tr>
<tr>
<td >Security Modules</td>
<td > SELinux, TOMOYO, AppArmor, Smack</td>
</tr>
</tbody></table>
<table><tbody>
<tr>
<td >/etc/fstab</td>
<td>kernel linux read this file at the first</td>
</tr>
</tbody></table>


| Command | Explain |
| ------ | ------ |
| lsmod   | All module that load with kernel |
| rmmod  |   |
| modprobe   |  |
| runlevel   | Show systrm runlevel at the moment |
| telinit   | Move to other runlevel |
| systemctl   | aaa |
| wc   | Count line and character rpm -qa | wc -l |
| grep   | Filter |
| systemctl get-default   | Filter |
| systemd-analyze   | - |


<!-----------------------------------------------------------Init----------------------------------------------------------->
<div class="md1"></div>

## Init

<!---------------------------------------System-->
#### <span class="red">System</span>

    SysVinit | systemd | upstart

<!---------------------------------------Find-->
#### <span class="red">Find</span>

    which init

    readlink -f /usr/sbin/init

    ls -ltrh /usr/sbin/init

    ps -p 1

    pstree

<!---------------------------------------systemd-->
#### <span class="red">Systemd</span>

<table><tbody>
<tr><td >Developer</td><td>Redhat</td></tr>
<tr><td >Wetsite</td><td><a href="https://www.freedesktop.org/wiki/" target="_blank">www.freedesktop.org</a></td></tr>
<tr><td >Github</td><td><a href="https://github.com/systemd" target="_blank">www.github.com/systemd</a></td></tr>
<tr><td >Wiki</td><td><a href="https://www.freedesktop.org/wiki/Software/systemd/" target="_blank">www.freedesktop.org/wiki/Software/systemd/</a></td></tr>
<tr><td >Local configuration</td><td>/etc/systemd/system</td></tr>
<tr><td >Runtime units</td><td>/run/systemd/system</td></tr>
<tr><td >Units of installed packages</td><td>/usr/lib/systemd/system</td></tr>
</tbody></table>

<!---------------------------------------Libraries-->
#### <span class="red">Libraries</span>

    dbus-1 | libpam | libcam | libcryptsetup | tcpwrapper | libaudit | libnotify

<!---------------------------------------Unit-->
#### <span class="red">Unit</span>

<span class="blue">Priority</span>

    /etc/systemd/system/ | /run/systemd/system/ | /usr/lib/systemd/system

<span class="blue">Type</span>

    service | socket | device | mount | automount | swap | target | path | timer | snapshot | slice | scope

<!---------------------------------------Target-->
#### <span class="red">Target</span>

    bootmode | basic | shutdown | reboot | multiuser | graphical | user session

<!---------------------------------------Utilites-->
#### <span class="red">Utilites</span>

    systemctl | journalctl | notify | analyze | cgls | cgtop | loginctl | nspawn

<!---------------------------------------GUI Interface-->
#### <span class="red">GUI Interface</span>

    systemd-ui | systemd-kcm


<!---------------------------------------Command-->
#### <span class="red">Command</span>

    systemctl | systemd-analyze

    systemctl get-default
    systemctl list-units
    systemctl list-units --type=service
    systemctl list-units --type=service | grep ssh

    systemctl is-system-running
    systemctl --failed
    systemctl is-active sshd
    systemctl enable sshd
    systemctl disable sshd
    systemctl status sshd
    systemctl start sshd
    systemctl stop sshd
    systemctl restart sshd
    systemctl reload sshd
    systemctl daemon-reload sshd


| Command | Explain |
| ------ | ------ |
| top   | Show all process |
| pstree   | Show all process as tree |
| ps aux   | Show all process |
| kill -9 33407   | kill process with PID 33407 |
| pkill -KILL fire* | kill all process that starts wirh fire |


<!-----------------------------------------------------------udevd----------------------------------------------------------->
<div class="md1"></div>

## Device Manager : udevd

<!---------------------------------------General-->
#### <span class="red">General</span>

| Component | Libreary | Explain |
| ------ | ------ | ------ |
| udevd | libudev | Standard libreary for using of udev |

<!---------------------------------------sysfs-->
#### <span class="red">sysfs</span> 
<div class="" align="right">
<div class="md4">شبه فایل سیستم در مموری کرنل</div>
<div class="md4"> ls /sys/</div>
<div class="md4"></div>
</div>

<!---------------------------------------udevd-->
<div class="md1"></div>

#### <span class="red">udevd</span> 
<div class="" align="right" dir="rtl">
<div class="md4">یه لایه بالاتر از sysfs است و در واقع یک Device Manager است </div>
<div class="md4"> به ما یک user space device میدهد که با آن میتوانیم با سخت افزار صحبت کنیم یعنی چیز بخونیم و چیز بنویسیم</div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
</div>

<!---------------------------------------dbus-->
<div class="md1"></div>

#### <span class="red">dbus</span> 
<div class="" align="right" dir="rtl">
<div class="md4">برنامه ها میتونن از طریق این سرویس بر روی باس برای هم پیغام بفرستند</div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
</div>

<!---------------------------------------proc-->
#### <span class="red">proc</span> 
<div class="" align="right">
<div class="md4"> شبه فایل سیستم در مموری کرنل که برای پروسس ها استفاده می شود</div>
<div class="md4"> ls /proc/</div>
<div class="md4"></div>
</div>

<!---------------------------------------Command-->
#### <span class="red">Command</span> 

| Command | Explain |
| ------ | ------ |
| lsusb   | Show Devices that connected to usb port |
| lspci  | Show Devices that connected to pci port  |
| lsblk  | Show Devices that connected to Block  |
| lshal   | Show Device who be HAL |
| lshw  | Show all Hardware |
| lspcmcia   | Show all mcia card |
| blkid  | Show block id like HDD  |



<!-----------------------------------------------------------journald----------------------------------------------------------->
<div class="md1"></div>

## Event logging : journald

<!---------------------------------------General-->
#### <span class="red">General</span>
<div class="" align="right" dir="rtl">
<div class="md4">مدیریت لاگ systemd</div>
<div class="md4"></div>
</div>

<!---------------------------------------Command-->
#### <span class="red">Command</span>

    journalctl
    journalctl --no-pager
    journalctl -n 10 
    journalctl -S -1d 
    journalctl -xe 
    journalctl -u ntp 
    journalctl _PID=1234


<table>
<thead><tr>
<th align="center" bgcolor="D1ECCF">Command</th>
<th align="center" bgcolor="D1ECCF">Example</th>
<th align="center" bgcolor="D1ECCF">Explain</th>
</tr></thead>
<tbody>
<tr><td align="center">dmesg</td><td align="center">dmesg</td><td align="center">Show all log</td></tr>
</tbody>
</table>



<!-----------------------------------------------------------User Manager----------------------------------------------------------->
<div class="md1"></div>

## User Manager : logind
| a | b |
| ------ | ------ |
| b | a |

who -T

<!-----------------------------------------------------------Network Manager----------------------------------------------------------->
<div class="md1"></div>

## Network Manager : networkd

| Command | Explain |
| ------ | ------ |
| nmcli d   | Show all network card |
| nmtui   | Graphic GUI for config network |
| ip link   | Show network card with some information |
| ip addr   | Show network card with some information with ipaddress |
| ip -s link   | Shoe detail of informaion about network card |



<!-----------------------------------------------------------Temp Manager----------------------------------------------------------->
<div class="md1"></div>

## Temp Manager : tmpfiles
| a | b |
| ------ | ------ |
| b | a |



<!-----------------------------------------------------------Time Manager----------------------------------------------------------->
<div class="md1"></div>

## Time Manager : timedated
| a | b |
| ------ | ------ |
| b | a |







<!-----------------------------------------------------------Boot Manager ----------------------------------------------------------->
<div class="md1"></div>

## Boot Manager : Systemd-boot
| a | b |
| ------ | ------ |
| libudev | Standard libreary for using of udev |



<!-----------------------------------------------------------Security----------------------------------------------------------->
<div class="md1"></div>

## Security : iptables

<!---------------------------------------General-->
#### <span class="red">General</span>

<span class="blue">Config</span>

    sudo apt-get install iptables-persistent

    iptables-save | uniq > /etc/iptables/rules.v4 

    vim /etc/iptables/rules.v4

<span class="blue">Show</span>

    iptables -L
    iptables -L -v
    iptables -L --line-numbers
    iptables -L INPUT
    iptables -S

<span class="blue">Delete</span>
    
    iptables -F 
    iptables -X

    iptables -F INPUT
    iptables -F OUTPUT
    iptables -F FORWARD

    iptables -D INPUT -p tcp --dport 3389 -j DROP

    iptables -D INPUT 2

<span class="blue">Reset</span>

    iptables -P OUTPUT ACCEPT
    iptables -P FORWARD ACCEPT
    iptables -P INPUT ACCEPT    
    iptables -A INPUT -i lo -j ACCEPT
    iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    iptables -A OUTPUT -o lo -j ACCEPT
    iptables -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    iptables -A INPUT -p icmp -j ACCEPT
    iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    iptables -A INPUT -p tcp --dport 80 -j ACCEPT
    iptables -A INPUT -p tcp --dport 443 -j ACCEPT
    iptables -A INPUT -p tcp --dport 3389 -j ACCEPT
    
<span class="blue">Nat</span>

    iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o tun0 -j MASQUERADE


<!-----------------------------------------------------------Disk----------------------------------------------------------->
<div class="md1"></div>

## Disk

<!---------------------------------------Concept-->
#### <span class="red">Concept</span>

<div><span class="blue">Partition Table</span> : <span>MBR | GPT</span></div>
<div><span class="blue">Partition Type</span> : <span>Primary | Extended(Logical) | LVM | Swap</span></div>

<!---------------------------------------Command-->
#### <span class="red">Commaand</span>
<table>
<thead><tr>
<th align="center" bgcolor="D1ECCF">Command</th>
<th align="center" bgcolor="D1ECCF">Example</th>
<th align="center" bgcolor="D1ECCF">Explain</th>
</tr></thead>
<tbody>
<tr><td align="center">lsblk</td><td align="center">lsblk -p</td><td align="center">list of partition and mounted on</td></tr>
<tr><td align="center">fdisk</td><td align="center">fdisk /dev/nvme0n1</td><td align="center">Create Partition</td></tr>
<tr><td align="center">parted</td><td align="center">parted /dev/nvme0n1 p</td><td align="center">Create Partition</td></tr>
<tr><td align="center">gparted</td><td align="center">gparted</td><td align="center">Create Partition</td></tr>
<tr><td align="center">mount</td><td align="center">mount | grep /dev/nvme0n1</td><td align="center"></td></tr>
</tbody>
</table>



<!-----------------------------------------------------------Ram----------------------------------------------------------->
<div class="md1"></div>

## Ram

<!---------------------------------------Swap-->
#### <span class="red">Swap</span>

<div><span class="blue">Type</span> : <span>Partition | File | zram</span></div>



<!---------------------------------------Command-->
#### <span class="red">Command</span>
<table>
<thead><tr>
<th align="center" bgcolor="D1ECCF">Command</th>
<th align="center" bgcolor="D1ECCF">Example</th>
<th align="center" bgcolor="D1ECCF">Explain</th>
</tr></thead>
<tbody>
<tr><td align="center">free</td><td align="center">free -h</td><td align="center">Ram Data</td></tr>
<tr><td align="center">swapon</td><td align="center">swapon</td><td align="center">Show swap location</td></tr>
</tbody>
</table>



<!-----------------------------------------------------------File----------------------------------------------------------->
<div class="md1"></div>

## File

<!---------------------------------------Folder system-->
#### <span class="red">Folder system</span>
<table>
<thead><tr><th align="center" bgcolor="D1ECCF">Directory</th><th align="center" bgcolor="D1ECCF">Description</th></tr></thead>
<tbody>
<tr><td align="center">bin</td><td align="center">Essential command binaries</td></tr>
<tr><td align="center">boot</td><td align="center">Static files of the boot loader</td></tr>
<tr><td align="center">dev</td><td align="center">Device files</td></tr>
<tr><td align="center">etc</td><td align="center">Host-specific system configuration</td></tr>
<tr><td align="center">home</td><td align="center">Home directory of the users</td></tr>
<tr><td align="center">lib</td><td align="center">Essential shared libraries and kernel modules</td></tr>
<tr><td align="center">media</td><td align="center">Mount point for removable media</td></tr>
<tr><td align="center">mnt</td><td align="center">Mount point for mounting a filesystem temporarily</td></tr>
<tr><td align="center">opt</td><td align="center">Add-on application software packages</td></tr>
<tr><td align="center">root</td><td align="center">Home directory of the root user</td></tr>
<tr><td align="center">sbin</td><td align="center">Essential system binaries</td></tr>
<tr><td align="center">srv</td><td align="center">Data for services provided by this system</td></tr>
<tr><td align="center">tmp</td><td align="center">Temporary files, sometimes purged on each boot</td></tr>
<tr><td align="center">usr</td><td align="center">Secondary hierarchy</td></tr>
<tr><td align="center">var</td><td align="center">Variable data (logs, ...)</td></tr>
</tbody>
</table>

<!---------------------------------------Command-->
#### <span class="red">Commaand</span>
| Command | Explain |
| ------ | ------ |
| ldd   | Show program library dependency |
| ldconfig  | Cash name and path of libreary  |
| df -h  | list of partition and mounted on  |
| lsblk -p  | list of partition and mounted on  |
| mount/umount  | add hard to file sytem  |
| fdisk  | partition bandi  |
| ------ | ------ |
| fdisk sda   | aaa |
| parted   | Ude for make partition |
| locate   | Find Directory or file |
| which   | Show path of program |

#### <span class="red">Part</span>

    stdin | stdout | stderr

#### <span class="red">View</span>

    cat | bzcat | xzcat | zcat | gzcat | less | od

#### <span class="red">Split</span>

    split | head | tail | cut 

#### <span class="red">Modify</span>

    nl | sort | uniq | paste | tr | sed

#### <span class="red">stats</span>

    wc | sha256sum

#### <span class="red">Management</span>

cp | find | mkdir | mv | ls | rm | rmdir | touch | tar | cpio | dd | file | gzip | gunzip | bzip2 | bunzip2 | xz | unxz | file globbing

Wildcards :&emsp;*&emsp; | &emsp;?&emsp;| &emsp;[ABC]&emsp;| &emsp;[a-k]&emsp; | &emsp;[0-9a-z]&emsp; | &emsp;[!x]

<table border="0" align="center" valign="top"><tbody><tr>
    <!-- td 1 -->
    <td valign="top">
        <table><tbody>        
            <tr><td align="center">touch</td><td>Create file <br> change time of the file</td></tr>
            <tr><td align="center">file</td><td>check file type</td></tr>
            <tr><td align="center">dd</td><td>convert and copy data</td></tr>
            <tr><td align="center">find</td><td>find file</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
        </tbody></table>
    </td>
    <!-- td 2 -->
    <td valign="top">
        <table><tbody>        
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
        </tbody></table>
    </td>
    <!-- td 3 -->
    <td valign="top">
        <table><tbody>        
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
        </tbody></table>
    </td>
</tr></tbody></table>

#### <span class="red">Compression</span>
    gzip & gunzip | bzip2 & bunzip2 | xz & unxz |

#### <span class="red">Archiving</span>
    tar | cpio
    tar -cfzv all.tar.gz *
    tar -zxvf all.tar.gz

#### <span class="red">streams | pipes | redirects</span>
<span class="blue">Command : </span> tree | xargs <br>
<span class="blue">Streams : </span> stdin | stdout | stderr <br>
<span class="blue">Example : </span>

    ls x* a*
    ls x* a* 1>out 2>err
    ls x* a* &>out_err 
    ls x* a* 1>out_err 2>&1
    ls x* a* 1>out 2>/dev/null

    cat << zzzz
    this is 1
    this is 2
    this is 3
    zzzz

    pipe
    -------------------------
    ls -1 | wc -l
    ls | tee fileA.txt
    xargs
    -------------------------
    ls | xargs echo
    echo "morteza" | xargs -I DATA echo this person DATA is fun


<!-----------------------------------------------------------Runlevel----------------------------------------------------------->
<div class="md1"></div>

## Runlevel

<!---------------------------------------Command-->
#### <span class="red">Commaand</span>

    systemctl list-units --type=target
    systemctl cat multi-user.target

    systemctl isolate rescue
    systemctl isolate emergency
    systemctl isolate reboot
    systemctl isolate halt
    systemctl isolate poweroff

    runlevel
    shutdown -r 1 we are restarting...
    shutdown -c

<a href="https://www.liquidweb.com/kb/linux-runlevels-explained/" target="_blank">runlevels</a> - 
<a href="http://www.tldp.org/LDP/sag/html/run" target="_blank">opetldp.orgnwrt</a> -

<div class="" align="left" dir="rtl">
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
</div>



<!-----------------------------------------------------------Shell----------------------------------------------------------->
<div class="md1"></div>

## Shell

#### <span class="red">Type</span>
    
    Bash | dash | zsh | ksh | csh

#### <span class="red">General</span>
    
    echo $SHELL

    ls -ltrh /bin/sh

    type cd
    type ls
    type ping

#### <span class="red">Command</span>

    cd | type | break | exec | pwd | set | export | history | 
    
    man | uname | ls | env | 

#### <span class="red">Characters</span>

    * | $ | \n | \t | 

#### <span class="red">Example</span>

    cd
    cd ~ 
    cd $HOME
    cd ..
    cd ~/Downloads
    echo $HOME
    echo \$HOME
    echo -e \\
    echo -e \\n
    touch x\ y
    which vim
    whereis vim 
    whatis vim 

    CTRL + R : Search history
    CTRL + O : Run search result
    !!       :  run last coomand
    !ping    : last command that is ping
    !30      : run command 30 from history

<!-----------------------------------------------------------Variable----------------------------------------------------------->
<div class="md1"></div>

## Variable

#### <span class="red">Command</span>

    PATH | PS1 | HOME | 

#### <span class="red">Command</span>

    env

#### <span class="red">Example</span>

    name='morteza'
    export name='morteza'

<!-----------------------------------------------------------[Process]----------------------------------------------------------->
<div class="md1"></div>

## Process

#### <span class="red">aaaa</span>

    inside the shell
    -------------------------------------------------
    jobs     :  show all process on curent terminal 
    jobs -l  :  show all process with od 
    CTRL + Z : kill process
    CTRL + Z : Stop processs
    fg %1    : start process 1 front grand
    bg %2    : start process 2 on back ground
    &        : run proceess on backgrouns
    nohup    : run process without patent process
    kill     : send signal to prcess
    killall  : kill all process with name 
    pkill    : kill all process that name inseide process


    pas      : shoe all process
    top
    htop 
    free : show mwmory free
    uptime 
    watch  : run command every 2 seccond

    screen 
    ----------------------------------
    یه شل مجازی میسازه
    Ctrl + a > miad to halati ke dastor bedi behesh
    d > az on screen miyad birun
    | > spilit paghe
    c > create ne shell
    screen -ls > list screen haro neshon mide
    screen -r 2234 > mire dakhele on screen ke id sho zdi
    
    tmux 
    ----------------------------------
    یه شل مجازی میسازه
    Ctrl + b > miad to halati ke dastor bedi behesh
    d > az on screen miyad birun
    % > spilit paghe amoudi
    " > split ofoghi
    c > ye safhe dige baz mikone 
    Ctrl+b > adade on safhe > mire dakhele on safhe 
    bad az Ctrl+B ba felesh ha be safahate dige mire
    tmux ls > list screen haro neshon mide
    tmux att -t 0 > mire dakhele on screen ke id sho zdi

<!-----------------------------------------------------------Package Manager System (PMS)----------------------------------------------------------->
<div class="md1"></div>

## Package Manager System (PMS)
    
#### <span class="red">Command</span>
<span class="blue">Debian</span> : dpkg | apt

<span class="blue">Redhat</span> : RPM | yum | dnf

#### <span class="red">Repository</span>
<span class="blue">Debian</span>

    /etc/apt/sources.list
    /var/cache/apt

<span class="blue">RedHat</span> 

    /etc/yum.conf
    /etc/yum.repos.d/


#### <span class="red">Example</span>
<span class="blue">Debian</span> 

    dpkg -I aaaa.deb
    dpkg -l
    dpkg -L code
    dpkg -S /usr/share/code/resources.pak
    sudo dpkg-reconfigure tzdata

    sudo apt show vim
    sudo apt clean all
    sudo apt update
    sudo apt list --upgradable
    sudo apt upgrade
    sudo apt dist-upgrade
    sudo apt install -f
    sudo apt install vim
    sudo apt remove vim
    sudo apt autoremove
    sudo apt install -s vlc
    sudo apt install --download-only vlc
    sudo apt download vlc
    sudo apt-cache search vim 
    
<span class="blue">RedHat</span> 





<!-----------------------------------------------------------Library----------------------------------------------------------->
<div class="md1"></div>

## Library

<!---------------------------------------C Standard Library-->
#### <span class="red">C Standard Library</span>
    glibc | uClibc | bionic

<!---------------------------------------Other Libraries-->
#### <span class="red">Other Libraries</span>
    GTK+, Qt, EFL,SDL, SFML, FLTK, GNUstep



<!---------------------------------------Configuration File-->
#### <span class="red">Configuration File</span>
    /etc/ld.so.conf
    /etc/ld.so.conf.d/


<!---------------------------------------Command-->
#### <span class="red">Command</span>
<table>
<thead><tr>
<th align="center" bgcolor="D1ECCF">Directory</th>
<th align="center" bgcolor="D1ECCF">Example</th>
<th align="center" bgcolor="D1ECCF">Description</th>
</tr></thead>
<tbody>
<tr><td align="center">ldd</td><td align="center">ldd /usr/bin/ls <br> ldd /usr/sbin/ldconfig</td><td align="center">یه برنامه از چه کتابخانه هایی استفاده میکند</td></tr>
<tr><td align="center">ldconfig</td><td align="center">sudo ldconfig -v</td><td align="center">آدرس های کتابخانه ها را کش می کند که سریع بشه پیدا کرد</td></tr>
<tr><td align="center">file</td><td align="center">file /usr/bin/ls</td><td align="center">میگه اون فایل چی هست</td></tr>
<tr><td align="center">readelf</td><td align="center">readelf -Wl /usr/bin/ls</td><td align="center">نشون میده داخل یه فایل اجرایی لینوکس چه خبره</td></tr>
<tr><td align="center">ld-linux</td><td align="center">/usr/lib/ld-linux.so.2 /usr/bin/ls</td>
<td align="center">
کتابخانه های مورد نیاز برنامه رو به برنامه وصل میکنه و اجرا میکنه
<br>
<span align="left" dir="rtl">
وقتی به یه برنامه مجوز Execution میدی در واقع میگی برو با ld-linux اجراش کن پس اگه مجوز نداشتی با این اجرا کن برنامه رو 
</span>
</td></tr>
</tbody>
</table>



<!------------------------------------------------------------------- [ Virtualization ] --->
<div class="md1"></div>

## Virtualization

#### <span class="red">Hardware support</span>
    Intel : lscpu | grep vmx
    AMD   : lscpu | grep svm
    
    lscpu | grep hypervisor

#### <span class="red">Type</span>

    Type 1 : KVM | Xen | Hyper-V
    Type 2 : virtualbox | vmware

#### <span class="red">Config</span>
    cat /etc/machine-id
    cat /var/lib/dbus/machine-id
    dbus-uuidgen --ensure

#### <span class="red">Container</span>
    Doucker

<!------------------------------------------------------------------- [ Graphic ] --->
<div class="md1"></div>

## Graphic
<table>
<thead>
<tr>
<th align="center" bgcolor="D1ECCF">Subject</th>
<th align="center" bgcolor="D1ECCF">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">User interface types</td>
<td align="center">CLI - GUI - NUI - VUI</td>
</tr>
<tr>
<td align="center">Windowing system</td>
<td align="center">X Window System(X11)</td>
</tr>
<tr>
<td align="center">Display manager</td>
<td align="center">GDM, KDM</td>
</tr>
<tr>
<td align="center">Desktop environment</td>
<td align="center">Gnome, KDE - Xfce - Unity</td>
</tr>
</tbody>
</table>


<!------------------------------------------------------------------- [ Link ] --->
<div class="md1"></div>

## Link

<div class="" align="left" dir="rtl">

<div class="md4">
<a href="https://unix.stackexchange.com/questions/620323/iptables-route-for-returning-incoming-traffic-back-out-of-originating-interfac" target="_blank">iptables-route</a> - 
<a href="https://superuser.com/questions/1242284/use-iptables-nat-to-redirect-gateway-for-lan-pcs" target="_blank">iptables-nat</a> - 
<a href="aaaa" target="_blank">aaaa</a> - 
<a href="aaaa" target="_blank">aaaa</a> - 
<a href="aaaa" target="_blank">aaaa</a> - 
<a href="aaaa" target="_blank">aaaa</a> - 
<a href="aaaa" target="_blank">aaaa</a> - 
</div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
</div>


<!------------------------------------------------------------------- [ Note ] --->
<div class="md1"></div>

## Note

<div class="" align="left" dir="rtl">
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
</div>


