<!------------------------------------------------------------------- [ Boot ] --->
## Boot

## Boot Manager : Systemd-boot
| a | b |
| ------ | ------ |
| libudev | Standard libreary for using of udev |

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




