<!------------------------------------------------------------------- [ Runlevel ] --->
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