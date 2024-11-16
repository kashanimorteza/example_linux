<!------------------------------------------------------------------- [ Package Manager System (PMS) ] --->
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




