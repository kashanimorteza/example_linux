<!------------------------------------------------------------------- [ Init ] --->
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


