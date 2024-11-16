

<!----------------------------------------------------------------------------------[Pages]-->
[Linux](index.md) |
[Debian](debian.md) |
[RedHat](redhat.md) |
[Mikrotik](mikrotik.md) |
[Config](config.md) |
[Script](script.md) |
[VPN](vpn.md) |
[Cryptography](cryptography.md)



<!----------------------------------------------------------------------------------[Subject]-->
<a href="#general">General</a> -
<a href="#ssh">SSH</a> -
<a href="#sshuttle">sshuttle</a> -
<a href="#tun2socks">tun2socks</a> -
<a href="#v2ray">v2ray</a> -



<!----------------------------------------------------------------------------------[General]-->
<div class="md5"></div>

## General

#### <span class="red">Source</span>
    
    Protocols : SSH Tunnel | PPTP | L2TP | OpenVpn | v2ray | Trojan GFW | BadVpn

    Protocols : TCP | UDP | Websocket | mKCP | QUIC

    Protocols : Socks | Shadowsocks | Vmess

#### <span class="red">Config</span>

    timedatectl set-timezone UTC

    cat /proc/sys/net/ipv4/ip_forward
    sysctl -w net.ipv4.ip_forward=1
    sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf

#### <span class="red">Install requirement</span>

    apt update
    apt upgrade    
    apt install net-tools 
    apt install make
    apt install git
    apt install golang-go
    apt install sshuttle
    apt install proxychains

#### <span class="red">Config iptables</span>

    apt remove ufw
    apt purge ufw
    apt install iptables-persistent
    
    iptables -F 
    iptables -X
    iptables -P OUTPUT ACCEPT
    iptables -P FORWARD ACCEPT
    iptables -P INPUT ACCEPT    
    iptables -A INPUT -i lo -j ACCEPT
    iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    iptables -A OUTPUT -o lo -j ACCEPT
    iptables -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    iptables -A INPUT -p icmp -j ACCEPT
    iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    iptables -A INPUT -p tcp --dport 22022 -j ACCEPT
    iptables -A INPUT -p tcp --dport 443 -j ACCEPT
    iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
    iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
    
    iptables-save | uniq > /etc/iptables/rules.v4
    systemctl enable iptables
    systemctl start iptables
    systemctl daemon-reload

#### <span class="red">Aliases</span>

    #-------------------------------------------------- [ Tunnel ]
    #------------- [ General ]
    alias ts='~/tunnel ssh rt root 198.244.232.101 22022 morteza 192.168.1.110 192.168.1.1 8081 wlp2s0 silent'
    alias tl='~/tl'
    alias tk='~/tk'
    #------------- [ SSh Tunnel]
    alias vst1="~/tunnel ssh tnl root 198.244.232.101 22022 morteza 192.168.1.110 192.168.1.1 8081 wlp2s0 silent"
    alias vsg1="~/tunnel ssh get root 198.244.232.101 22022 morteza 192.168.1.110 192.168.1.1 8081 wlp2s0 silent"
    alias vss1="~/tunnel ssh rt root 198.244.232.101 22022 morteza 192.168.1.110 192.168.1.1 8081 wlp2s0 silent"
    alias vst2="~/tunnel ssh tnl root 95.179.194.40 22022 morteza 192.168.1.110 192.168.1.1 8081 wlp2s0 silent"
    alias vsg2="~/tunnel ssh get root 95.179.194.40 22022 morteza 192.168.1.110 192.168.1.1 8081 wlp2s0 silent"
    alias vss2="~/tunnel ssh rt root 95.179.194.40 22022 morteza 192.168.1.110 192.168.1.1 8081 wlp2s0 silent"
    #------------- [ V2ray Tunnel]
    alias vvc="sudo vim ~/v2ray/config.json"
    alias vvt1="sudo cp -f ~/v2ray/web-ws-vmess.config ~/v2ray/config.json && sudo ~/tunnel v2ray tnl root 198.244.232.101 22022 morteza 192.168.1.110 192.168.1.1 8082 wlp2s0 silent"
    alias vvg1="sudo cp -f ~/v2ray/web-ws-vmess.config ~/v2ray/config.json && sudo ~/tunnel v2ray get root 198.244.232.101 22022 morteza 192.168.1.110 192.168.1.1 8082 wlp2s0 silent"
    alias vvt2="sudo cp -f ~/v2ray/vpn-ws-vmess.config ~/v2ray/config.json && sudo ~/tunnel v2ray tnl root 95.179.194.40 22 morteza 192.168.1.110 192.168.1.1 8082 wlp2s0 silent"
    alias vvg2="sudo cp -f ~/v2ray/vpn-ws-vmess.config ~/v2ray/config.json && sudo ~/tunnel v2ray get root 95.179.194.40 22 morteza 192.168.1.110 192.168.1.1 8082 wlp2s0 silent"
    #------------- [ Tunnel status]
    alias tt='ps -ef | grep tun2socks'

    #------------- [ Raspberry ]
    alias sr='~/linux/s raspberry'
    alias srtss='ssh root@192.168.1.6 "~/runnel ssh"'
    alias srtvs='ssh root@192.168.1.6 "~/runnel v2ray"'
    alias srtvc='ssh root@192.168.1.6 "cat ~/v2ray/config.json"'
    alias srtvc1='ssh root@192.168.1.6 "cp -f ~/v2ray/web-ws-vmess.config ~/v2ray/config.json && ~/tunnel v2ray"'
    alias srtvc2='ssh root@192.168.1.6 "cp -f ~/v2ray/vpn-ws-vmess.config ~/v2ray/config.json && ~/tunnel v2ray"'

#### <span class="red">Tunnel</span>

vim /root/tunnel

    #!/bin/bash

    echo "---------------------------------------------------------Config..."
    proto=${1}
    mode=${2}
    server_user=${3}
    server_ip=${4}
    server_port=${5}
    local_user=${6}
    local_ip=${7}
    local_gateway=${8}
    local_port=${9}
    local_interface=${10}
    debug=${11}

    if [ $local_user = root ];
    then
            location=/root
    else
            location=/home/$local_user
    fi

    echo "---------------------------------------------------------Log..."
    echo "Proto           : $proto"
    echo "Mode            : $mode"
    echo "Server User     : $server_user"
    echo "Server Ip       : $server_ip"
    echo "Server Port     : $server_port"
    echo "Local User      : $local_user"
    echo "Local Ip        : $local_ip"
    echo "Local Gateway   : $local_gateway"
    echo "Local Port      : $local_port"
    echo "Local Interface : $local_interface"
    echo "Location        : $location"


    echo "---------------------------------------------------------Iptables..."
    systemctl restart iptables
    #iptables -A INPUT -p tcp --dport $local_port -j ACCEPT
    #iptables -A INPUT -p udp --dport $local_port -j ACCEPT


    echo "---------------------------------------------------------Clera..."
    $location/tk


    echo "---------------------------------------------------------ssh..."
    if [ $proto = ssh ];
    then
            if [ $mode = tnl ];
            then
                    ssh -fCqND  $local_ip:$local_port $server_user@$server_ip -p $server_port &
            elif [ $mode = get ];
            then
                    sshuttle -r $server_user@$server_ip:$server_port 0.0.0.0/0 --dns &
            else
                    echo "----------Add tun0..."
                    ip tuntap add mode tun dev tun0
                    ip addr add 10.0.0.1/24 dev tun0
                    ip link set dev tun0 up
                    echo "----------Routing..."
                    ip route del default
                    ip route add $server_ip via $local_gateway dev $local_interface
                    ip route add default via 10.0.0.1 dev tun0 metric 1
                    ip route add default via $local_gateway dev $local_interface metric 10
                    #sudo $location/route_add_iran
                    echo "----------Tunneling..."
                    ssh -fCqND  $local_ip:$local_port $server_user@$server_ip -p $server_port &
                    echo "----------tun2socks..."
                    $location/tun2socks/build/tun2socks -loglevel $debug -device tun0 -proxy socks5://$local_ip:$local_port -interface $local_interface &
            fi
    fi

    echo "---------------------------------------------------------v2ray..."
    if [ $proto = v2ray ];
    then
            if [ $mode = tnl ];
            then
            echo "----------Tunneling..."
                    $location/v2ray/v2ray run -config=$location/v2ray/config.json &
            elif [ $mode = get ];
            then

                    echo "----------Add tun0..."
                    ip tuntap add mode tun dev tun0
                    ip addr add 10.0.0.1/24 dev tun0
                    ip link set dev tun0 up
                    echo "----------Routing..."
                    ip route del default
                    ip route add $server_ip via $local_gateway dev $local_interface
                    ip route add default via 10.0.0.1 dev tun0 metric 1
                    ip route add default via $local_gateway dev $local_interface metric 10
                    #sudo $location/route_add_iran
            echo "----------Tunneling..."
            $location/v2ray/v2ray run -config=$location/v2ray/config.json &
                    echo "----------tun2socks..."
                    $location/tun2socks/build/tun2socks -loglevel $debug -device tun0 -proxy socks5://$local_ip:$local_port -interface $local_interface &
            fi
    fi

chmod +x /root/tunnel


#### <span class="red">Service</span>

vim  /etc/systemd/system/tunnel.service

    [Unit]
    Description=Route all trafic to ssh tunnel

    [Service]
    User=root
    ExecStart=/root/tunnel

    [Install]
    WantedBy=multi-user.target



    [Unit]
    Description=sshuttle service
    After=network.target
    [Service]
    User=sshuttle
    Restart=always
    Type=forking
    WorkingDirectory=/etc/sshuttle
    ExecStart=/etc/sshuttle/sshuttle.py start
    ExecStop=/etc/sshuttle/sshuttle.py stop
    [Install]
    WantedBy=multi-user.target

systemctl daemon-reload



<!----------------------------------------------------------------------------------[SSH]-->
<div class="md1"></div>

## SSh

#### <span class="red">Create user without bash</span>

    useradd -m -s /usr/sbin/nologin morteza


#### <span class="red">Start</span>

vim ~/ts

	#!/bin/bash
	ssh -fCqND 192.168.1.6:8082 root@45.77.57.39

chmod +x ~/ts

#### <span class="red">List</span>

vim ~/tl

    #!/bin/bash

    echo "---------------------List---------------------------sshuttle Tunnel List"
    ps -ef | grep "sshuttle -r" | grep -v grep
    echo "---------------------List---------------------------SSH Tunnel List"
    ps -ef | grep "ssh -fCqND" | grep -v grep
    echo "---------------------List---------------------------V2ray Tunnel List"
    ps -ef | grep "v2ray" | grep -v grep
    echo "---------------------List---------------------------Tun2socks Tunnel List"
    ps -ef | grep "tun2socks" | grep -v grep

chmod +x ~/tl

#### <span class="red">Kill</span>

vim ~/tk

    #!/bin/bash

    echo "---------------------Kill---------------------------Kill sshuttle Tunnel List"
    ps -ef | grep "sshuttle -r"  | grep -v grep
    for OUTPUT1 in $(ps -ef | grep "sshuttle -r" | grep -v grep | awk -F" " 'system("echo  "$2"")')
    do
            kill $OUTPUT1
    done

    echo "---------------------Kill---------------------------Kill SSH Tunnel List"
    ps -ef | grep "ssh -fCqND"  | grep -v grep
    for OUTPUT2 in $(ps -ef | grep "ssh -fCqND" | grep -v grep | awk -F" " 'system("echo  "$2"")')
    do
            kill $OUTPUT2
    done

    echo "---------------------Kill---------------------------Kill V2ray Tunnel List"
    ps -ef | grep "v2ray/v2ray" | grep -v grep
    for OUTPUT3 in $(ps -ef | grep "v2ray/v2ray" | grep -v grep | awk -F" " 'system("echo  "$2"")')
    do
            kill $OUTPUT3
    done

    echo "---------------------Kill---------------------------Kill Tun2socks"
    ps -ef | grep "tun2socks"  | grep -v grep
    for OUTPUT4 in $(ps -ef | grep "tun2socks"  | grep -v grep | awk -F" " 'system("echo  "$2"")')
    do
            kill $OUTPUT4
    done

chmod +x ~/tk

#### <span class="red">Check</span>

vim ~/tch

    #!/bin/bash

    STR=$(ps -ef | grep "ssh -fCqND 192.168.1.6:8081 root@45.32.181.149 -p 22022"  | grep -v grep | awk -F" " 'system("echo  True")')
    SUB='True'
    if [[ "$STR" != *"$SUB"* ]]; then
            systemctl restart tunnel_ssh
    fi

chmod +x ~/tch

vim /etc/crontab

    *  *    * * *   root    /root/tch



<!----------------------------------------------------------------------------------[sshuttle]-->
<div class="md1"></div>

## sshuttle

    sshuttle -r root@198.244.232.101:22022 0.0.0.0/0 -vv --dns



<!----------------------------------------------------------------------------------[tun2socks]-->
<div class="md1"></div>

## tun2socks
    
#### <span class="red">Source</span>

    https://github.com/xjasonlyu/tun2socks

#### <span class="red">Intall</span>
    
    cd /root/
    git clone git@github.com:xjasonlyu/tun2socks.git
    cd tun2socks
    make tun2socks
    
<!----------------------------------------------------------------------------------[v2ray]-->
<div class="md1"></div>

## v2ray

<!---------------------------------------Source-->
#### <span class="red">Source</span>

v2ray : 
<a href="https://v2ray.com/en" target="_blank">v2ray.com</a> | 
<a href="https://github.com/v2ray" target="_blank">github.com/v2ray</a>

v2fly : 
<a href="https://www.v2fly.org/" target="_blank">v2fly.org</a> | 
<a href="https://github.com/v2fly" target="_blank">github.com/v2fly</a>

233blog :
<a href="https://233blog.com/" target="_blank">233blog</a>

vaxilu :
<a href="https://github.com/vaxilu/x-ui/" target="_blank">github.com/vaxilu</a>

privacymelon : 
<a href="https://privacymelon.com/v2ray-setup-guide/" target="_blank">v2ray</a> | 
<a href="https://privacymelon.com/how-to-setup-v2ray-ws-tls-cdn/" target="_blank">v2ray-ws-tls-cdn</a> | 
<a href="https://privacymelon.com/how-to-install-vless-xtls-xray-core/" target="_blank">vless-xtls-xray-cor</a>

Other:
<a href="https://toutyrater.github.io/" target="_blank">toutyrater.github.io</a> - 
<a href="http://233blog.com/" target="_blank">233blog.com</a>
    

<!---------------------------------------Install Core-->
#### <span class="red">Install</span>

<span class="blue">v2fly</span>

Install

    bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)

Remove :

    bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh) --remove

Config:

    vim /usr/local/etc/v2ray/config.json

Log:

    tail -f  /var/log/v2ray/access.log
    tail -f /var/log/v2ray/error.log

<span class="blue">233blog</span>

Install

    bash <(curl -L -s https://git.io/v2ray.sh)

Config 


Command

    general config menu   : v2ray
    show configuration    : v2ray > 1
    change port 9999      : v2ray > 2 > 1 > 9999
    change protocol to ws : v2ray > 2 > 2 > 20 > 10000 > 20000
    get config for client : v2ray qr > open link and scan qrCode

<span class="blue">vaxilu</span>

Install

    bash <(curl -L -s https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)

    Install parameters : 
    --------------------------
    y
    admin
    123456
    8090

    Access to panel :
    --------------------------
    link : http://192.168.1.6:8090
    User : admin
    Pass : 123456

Config

    vim /usr/local/x-ui/bin/config.json
    vim /usr/bin/x-ui

Command

    general config menu   : x-ui

<span class="blue">With Accontinyf</span>

Install

    bash <(curl -Ls https://raw.githubusercontent.com/hossinasaadi/x-ui/master/install.sh)






<!---------------------------------------Client-->
#### <span class="red">Client</span>

<span class="blue">Linux</span>

v2ray core

    install v2ray-core 
    add client config to config file
    start service 
    set proxy to 192.168.1.6

v2ray binary

    wget https://github.com/v2fly/v2ray-core/releases/download/v5.1.0/v2ray-linux-64.zip
    unzip v2ray-linux-64.zip -d ./v2ray/
    cd ./v2ray
    vim config.json  #put your config into this file
    ./v2ray run -config=config.json
    set proxy to 192.168.1.6


v2rayA (Web GUI) : <a href="https://v2raya.org/en/" target="_blank">v2raya.org</a> - <a href="https://github.com/v2rayA" target="_blank">github.com/v2rayA</a>

    curl -Ls https://mirrors.v2raya.org/go.sh | bash
    wget -qO - https://apt.v2raya.org/key/public-key.asc | tee /etc/apt/trusted.gpg.d/v2raya.asc
    echo "deb https://apt.v2raya.org/ v2raya main" | tee /etc/apt/sources.list.d/v2raya.list
    apt update
    apt install v2raya
    v2raya --reset-password



<span class="blue">Android</span>

    OneClick | v2RayNG | Kitsunebi | BifrostV | V2Ray | Clash for Android

<span class="blue">IOS</span>

    OneClick | ShadowRocket | Kitsunebi | Quantumult | i2Ray | Pepi | 91VPN | Pharos Pr

<span class="blue">Windows</span>

    V2RayW | V2RayN | V2RayS | Clash



<!---------------------------------------Config Example-->
#### <span class="red">Config Example</span>

<span class="blue">Server</span>

    {
    "log": null,
    "routing": {
        "rules": [
        {
            "inboundTag": [
            "api"
            ],
            "outboundTag": "api",
            "type": "field"
        },
        {
            "ip": [
            "geoip:private"
            ],
            "outboundTag": "blocked",
            "type": "field"
        },
        {
            "outboundTag": "blocked",
            "protocol": [
            "bittorrent"
            ],
            "type": "field"
        }
        ]
    },
    "dns": null,
    "inbounds": [
        {
        "listen": "192.168.1.6",
        "port": 9999,
        "protocol": "dokodemo-door",
        "settings": {
            "address": "192.168.1.6"
        },
        "streamSettings": null,
        "tag": "api",
        "sniffing": null
        },
        {
        "listen": null,
        "port": 10000,
        "protocol": "vmess",
        "settings": {
            "clients": [
            {
                "id": "3255441iayrusdfpod-g[fgf3f[][fda[-487fg7-f9[d]7[5-bd9909dddda8e2015",
                "alterId": 0
            }
            ],
            "disableInsecureEncryption": false
        },
        "streamSettings": {
            "network": "ws",
            "security": "none",
            "wsSettings": {
            "path": "/",
            "headers": {}
            }
        },
        "tag": "inbound-9999",
        "sniffing": {
            "enabled": true,
            "destOverride": [
            "http",
            "tls"
            ]
        }
        }
    ],
    "outbounds": [
        {
        "protocol": "freedom",
        "settings": {}
        },
        {
        "protocol": "blackhole",
        "settings": {},
        "tag": "blocked"
        }
    ],
    "transport": null,
    "policy": {
        "system": {
        "statsInboundDownlink": true,
        "statsInboundUplink": true
        }
    },
    "api": {
        "services": [
        "HandlerService",
        "LoggerService",
        "StatsService"
        ],
        "tag": "api"
    },
    "stats": {},
    "reverse": null,
    "fakeDns": null
    }



<span class="blue">Client</span>

    {
    "dns": {
        "hosts": {
        "domain:googleapis.cn": "googleapis.com"
        },
        "servers": [
        "1.1.1.1"
        ]
    },
    "inbounds": [
        {
        "listen": "192.168.1.6",
        "port": 10808,
        "protocol": "socks",
        "settings": {
            "auth": "noauth",
            "udp": true,
            "userLevel": 8
        },
        "sniffing": {
            "destOverride": [
            "http",
            "tls"
            ],
            "enabled": true
        },
        "tag": "socks"
        },
        {
        "listen": "192.168.1.6",
        "port": 10809,
        "protocol": "http",
        "settings": {
            "userLevel": 8
        },
        "tag": "http"
        }
    ],
    "log": {
        "loglevel": "warning"
    },
    "outbounds": [
        {
        "mux": {
            "concurrency": 8,
            "enabled": false
        },
        "protocol": "vmess",
        "settings": {
            "vnext": [
            {
                "address": "78.254.154.12",
                "port": 9999,
                "users": [
                {
                    "alterId": 0,
                    "encryption": "",
                    "flow": "",
                    "id": "5wer22rr-4be0-1122554-ab7f-ft45877b1b7",
                    "level": 8,
                    "security": "auto"
                }
                ]
            }
            ]
        },
        "streamSettings": {
            "network": "ws",
            "security": "",
            "wsSettings": {
            "headers": {
                "Host": ""
            },
            "path": ""
            }
        },
        "tag": "proxy"
        },
        {
        "protocol": "freedom",
        "settings": {},
        "tag": "direct"
        },
        {
        "protocol": "blackhole",
        "settings": {
            "response": {
            "type": "http"
            }
        },
        "tag": "block"
        }
    ],
    "routing": {
        "domainMatcher": "mph",
        "domainStrategy": "IPIfNonMatch",
        "rules": [
        {
            "ip": [
            "1.1.1.1"
            ],
            "outboundTag": "proxy",
            "port": "53",
            "type": "field"
        }
        ]
    }
    }


<!----------------------------------------------------------------------------------[SSR]-->
<div class="md1"></div>

## SSR

#### <span class="red">Document</span>

    Source  : https://github.com/ShadowsocksR-Live
    Youtube : https://www.youtube.com/watch?v=pSZWNUhXeVw


#### <span class="red">Install</span>

    vim /etc/sysctl.conf
    ------------------------------------------
    net.core.default_qdisc=fq
    net.ipv4.tcp_congestion_control=bbr

    wget --no-check-certificate https://raw.githubusercontent.com/ShadowsocksR-Live/shadowsocksr-native/master/install/ssrn-install.sh
    chmod +x ssrn-install.sh
    ./ssrn-install.sh 2>&1 | tee ssr-n.log

#### <span class="red">Client</span>

    Android
    ---------------------------
    https://github.com/shadowsocksrr/shadowsocksr-android/releases/download/3.5.4/shadowsocksr-android-3.5.4.apk
    
    IOS
    ---------------------------

    Windows
    ---------------------------
    https://github.com/ShadowsocksR-Live/ssrWin/releases/download/0.8.6/ssr-win-x64.zip

    Linux
    ---------------------------


<!----------------------------------------------------------------------------------[BadVpn]-->
<div class="md1"></div>

## BadVpn

    Ambroz Bizjak 
    ambrop7@gmail.com

    https://code.google.com/archive/p/badvpn/
    https://github.com/ambrop72/badvpn







<!------------------------------------------------------------------- [ V2ray ] --->
<br><br>

## V2ray

<!---------------------------------------Resource-->
#### <span class="red">Resource</span>

Web : 
<a href="https://www.v2ray.com/en/index.html" target="_blank">Project V</a> - 
<a href="https://xtls.github.io/en/" target="_blank">Project X</a> - 

Github :
<a href="https://github.com/v2ray" target="_blank">v2ray</a> - 
<a href="https://github.com/v2fly" target="_blank">v2fly</a> - 
<a href="https://github.com/XTLS" target="_blank">XTLS</a> - 

Panel :
<a href="https://github.com/hiddify" target="_blank">hiddify</a> - 
<a href="https://github.com/Gozargah" target="_blank">gozargah</a> - 

<!---------------------------------------Xray-->
#### <span class="red">Xray</span>


<span class="blue">Alias</span>

    alias xf="cd /usr/local/etc/xray/"
    alias xc="vim /usr/local/etc/xray/config.json"
    alias xr="systemctl restart xray"
    alias xs="systemctl status xray"

<span class="blue">Install</span>

    Source
    ---------------------------------------------------------
    https://github.com/XTLS/Xray-install 
    
    Command
    ---------------------------------------------------------
	bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install

    File and Folder
    ---------------------------------------------------------
    /usr/local/bin/xray
    /usr/local/share/xray/geoip.dat
    /usr/local/share/xray/geosite.dat
    /usr/local/etc/xray/config.json
    /var/log/xray/access.log
    /var/log/xray/error.log
    /etc/systemd/system/xray.service
    /etc/systemd/system/xray@.service

<!---------------------------------------Hiddify-->



<!---------------------------------------Gozargah-->
#### <span class="red">Gozargah</span>

	git clone https://github.com/Gozargah/Marzban.git
	cd Marzban
	python3.8 -m venv .myenv3.8
	./.myenv3.8/bin/python3.8 -m pip install --upgrade pip
	source .myenv3.8/bin/activate	
	wget -qO- https://bootstrap.pypa.io/get-pip.py | python3 -
	python3 -m pip install -r requirements.txt


<!---------------------------------------Requirement-->
#### <span class="red">Requirement</span>

	add-apt-repository ppa:deadsnakes/ppa
	apt update -y
	apt install python3.8 -y
	apt install python3-pip -y 
	apt install python3.8-venv



    xray run -confdir /usr/local/etc/xray/ -test

for BASE in 00_log 01_api 02_dns 03_routing 04_policy 05_inbounds 06_outbounds 07_transport 08_stats 09_reverse 10_fakedns; do echo '{}' > "/usr/local/etc/xray/$BASE.json"; done


certbot certonly --standalone -d testtls2.mkcf.online --agree-tos -m mkvpn1001@gmail.com -n 


/etc/letsencrypt/live/testtls1.mkcf.online/fullchain.pem
/etc/letsencrypt/live/testtls1.mkcf.online/privkey.pem





&& sudo mv /etc/letsencrypt/live/testtls1.mkcf.online/fullchain.pem /opt/mkpanel/certificates/testtls1.mkcf.online.crt && sudo mv /etc/letsencrypt/live/testtls1.mkcf.online/privkey.pem /opt/mkpanel/certificates/testtls1.mkcf.online.key




ssh-keygen -t rsa -b 1024 -f /root/.ssh/test2 -N ""
