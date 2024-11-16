<!----------------------------------------------------------------------------------[Desktop]-->
## Desktop

#### Linux
    Download ventory | https://github.com/ventoy/Ventoy/releases
    Extract          | ventoy-1.0.77-linux.tar.gz
    Run              | ./VentoyGUI.x86_64
    Download linux   | https://linuxmint.com/edition.php?id=292
    Install Linux    | Copy linux image to ventory flash and Install linux

#### GPG
    gpg --import abd_public_key.asc
    gpg --import abd_private_key.asc
    gpg --list-keys
    gpg --edit-key <key>
    trust | 5 | quit

#### Note
    download note-main.zip
    extract note-main.zip
    cd ~/note-main
    sudo ./pull

#### Setting
    Appearance     | change theme
    KeyBoard       | add language
    Date Format    | DateTime: %b:%m / %A:%e / %H:%M:%S     Date: %b:%m | %A:%e     Time: %H:%M:%S
    Driver Manager | update graphic driver
    System Report  | Install multimedia codec
    Power Manager  | Disable timing

#### Config
    sudo timedatectl set-timezone UTC
    mkdir app
    mkdir ~/.ssh
    echo laptop > /etc/hostname
    echo "morteza ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

#### Install
    apt update
    apt upgrade
    apt install vim git xdotool dnscrypt-proxy
    install chrome vscode xdm telegram Remmina

#### Iptables
    systemctl disable ufw
    systemctl stop ufw
    apt-get install iptables-persistent
    iptables -F 
    iptables -X
    iptables -P OUTPUT ACCEPT
    iptables -P FORWARD ACCEPT
    iptables -P INPUT DROP    
    iptables -A INPUT -i lo -j ACCEPT
    iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    iptables -A OUTPUT -o lo -j ACCEPT
    iptables -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    iptables -A INPUT -p icmp -j ACCEPT
    iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    iptables -A INPUT -p tcp --dport 22022 -j ACCEPT
    iptables -A INPUT -p tcp --dport 33033 -j ACCEPT
    iptables -A INPUT -p tcp --dport 44044 -j ACCEPT
    iptables -A INPUT -p tcp --dport 80 -j ACCEPT
    iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
    iptables-save | uniq > /etc/iptables/rules.v4
    (crontab -l ; echo "@reboot systemctl restart iptables") | crontab -

#### Git
    git config --global user.email "kashani.morteza@gmail.com"
    git config --global user.name "morteza"
    git config --global core.editor "vim"

#### Dnscrypt-proxy
    vim /etc/dnscrypt-proxy/dnscrypt-proxy.toml

    listen_addresses = []
    server_names = ['free.shecan.ir']
    [query_log]
    file = '/var/log/dnscrypt-proxy/query.log'
    [nx_log]
    file = '/var/log/dnscrypt-proxy/nx.log'
    [static]
    [static.'free.shecan.ir']
    stamp = 'sdns://AgUAAAAAAAAAAAAOZnJlZS5zaGVjYW4uaXIKL2Rucy1xdWVyeQ'

    systemctl enable dnscrypt-proxy
    systemctl restart dnscrypt-proxy


<!----------------------------------------------------------------------------------[Backup]-->
## OS Backup

#### Backup
    sudo dd if=/dev/sda of=/data/image.img bs=4M

#### Restor
    sudo dd if=/data/image.img of=/dev/sda bs=4M