<!------------------------------------------------------------------- [ Library ] --->
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



