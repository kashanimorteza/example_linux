<!------------------------------------------------------------------- [ Kernel ] --->
## Kernel


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


