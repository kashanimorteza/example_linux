<!------------------------------------------------------------------- [ Kernel ] --->
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





