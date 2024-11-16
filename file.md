<!------------------------------------------------------------------- [ Runlevel ] --->
## Runlevel

<!---------------------------------------Folder system-->
#### <span class="red">Folder system</span>
<table>
<thead><tr><th align="center" bgcolor="D1ECCF">Directory</th><th align="center" bgcolor="D1ECCF">Description</th></tr></thead>
<tbody>
<tr><td align="center">bin</td><td align="center">Essential command binaries</td></tr>
<tr><td align="center">boot</td><td align="center">Static files of the boot loader</td></tr>
<tr><td align="center">dev</td><td align="center">Device files</td></tr>
<tr><td align="center">etc</td><td align="center">Host-specific system configuration</td></tr>
<tr><td align="center">home</td><td align="center">Home directory of the users</td></tr>
<tr><td align="center">lib</td><td align="center">Essential shared libraries and kernel modules</td></tr>
<tr><td align="center">media</td><td align="center">Mount point for removable media</td></tr>
<tr><td align="center">mnt</td><td align="center">Mount point for mounting a filesystem temporarily</td></tr>
<tr><td align="center">opt</td><td align="center">Add-on application software packages</td></tr>
<tr><td align="center">root</td><td align="center">Home directory of the root user</td></tr>
<tr><td align="center">sbin</td><td align="center">Essential system binaries</td></tr>
<tr><td align="center">srv</td><td align="center">Data for services provided by this system</td></tr>
<tr><td align="center">tmp</td><td align="center">Temporary files, sometimes purged on each boot</td></tr>
<tr><td align="center">usr</td><td align="center">Secondary hierarchy</td></tr>
<tr><td align="center">var</td><td align="center">Variable data (logs, ...)</td></tr>
</tbody>
</table>

<!---------------------------------------Command-->
#### <span class="red">Commaand</span>
| Command | Explain |
| ------ | ------ |
| ldd   | Show program library dependency |
| ldconfig  | Cash name and path of libreary  |
| df -h  | list of partition and mounted on  |
| lsblk -p  | list of partition and mounted on  |
| mount/umount  | add hard to file sytem  |
| fdisk  | partition bandi  |
| ------ | ------ |
| fdisk sda   | aaa |
| parted   | Ude for make partition |
| locate   | Find Directory or file |
| which   | Show path of program |

#### <span class="red">Part</span>

    stdin | stdout | stderr

#### <span class="red">View</span>

    cat | bzcat | xzcat | zcat | gzcat | less | od

#### <span class="red">Split</span>

    split | head | tail | cut 

#### <span class="red">Modify</span>

    nl | sort | uniq | paste | tr | sed

#### <span class="red">stats</span>

    wc | sha256sum

#### <span class="red">Management</span>

cp | find | mkdir | mv | ls | rm | rmdir | touch | tar | cpio | dd | file | gzip | gunzip | bzip2 | bunzip2 | xz | unxz | file globbing

Wildcards :&emsp;*&emsp; | &emsp;?&emsp;| &emsp;[ABC]&emsp;| &emsp;[a-k]&emsp; | &emsp;[0-9a-z]&emsp; | &emsp;[!x]

<table border="0" align="center" valign="top"><tbody><tr>
    <!-- td 1 -->
    <td valign="top">
        <table><tbody>        
            <tr><td align="center">touch</td><td>Create file <br> change time of the file</td></tr>
            <tr><td align="center">file</td><td>check file type</td></tr>
            <tr><td align="center">dd</td><td>convert and copy data</td></tr>
            <tr><td align="center">find</td><td>find file</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
        </tbody></table>
    </td>
    <!-- td 2 -->
    <td valign="top">
        <table><tbody>        
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
        </tbody></table>
    </td>
    <!-- td 3 -->
    <td valign="top">
        <table><tbody>        
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
            <tr><td align="center">a</td><td>q</td></tr>
        </tbody></table>
    </td>
</tr></tbody></table>

#### <span class="red">Compression</span>
    gzip & gunzip | bzip2 & bunzip2 | xz & unxz |

#### <span class="red">Archiving</span>
    tar | cpio
    tar -cfzv all.tar.gz *
    tar -zxvf all.tar.gz

#### <span class="red">streams | pipes | redirects</span>
<span class="blue">Command : </span> tree | xargs <br>
<span class="blue">Streams : </span> stdin | stdout | stderr <br>
<span class="blue">Example : </span>

    ls x* a*
    ls x* a* 1>out 2>err
    ls x* a* &>out_err 
    ls x* a* 1>out_err 2>&1
    ls x* a* 1>out 2>/dev/null

    cat << zzzz
    this is 1
    this is 2
    this is 3
    zzzz

    pipe
    -------------------------
    ls -1 | wc -l
    ls | tee fileA.txt
    xargs
    -------------------------
    ls | xargs echo
    echo "morteza" | xargs -I DATA echo this person DATA is fun



