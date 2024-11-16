<!------------------------------------------------------------------- [ Security ] --->
## Security

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