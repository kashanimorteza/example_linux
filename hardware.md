<!------------------------------------------------------------------- [ Hardware ] --->
## Hardware

## Disk

<!---------------------------------------Concept-->
#### <span class="red">Concept</span>

<div><span class="blue">Partition Table</span> : <span>MBR | GPT</span></div>
<div><span class="blue">Partition Type</span> : <span>Primary | Extended(Logical) | LVM | Swap</span></div>

<!---------------------------------------Command-->
#### <span class="red">Commaand</span>
<table>
<thead><tr>
<th align="center" bgcolor="D1ECCF">Command</th>
<th align="center" bgcolor="D1ECCF">Example</th>
<th align="center" bgcolor="D1ECCF">Explain</th>
</tr></thead>
<tbody>
<tr><td align="center">lsblk</td><td align="center">lsblk -p</td><td align="center">list of partition and mounted on</td></tr>
<tr><td align="center">fdisk</td><td align="center">fdisk /dev/nvme0n1</td><td align="center">Create Partition</td></tr>
<tr><td align="center">parted</td><td align="center">parted /dev/nvme0n1 p</td><td align="center">Create Partition</td></tr>
<tr><td align="center">gparted</td><td align="center">gparted</td><td align="center">Create Partition</td></tr>
<tr><td align="center">mount</td><td align="center">mount | grep /dev/nvme0n1</td><td align="center"></td></tr>
</tbody>
</table>

## Ram

<!---------------------------------------Swap-->
#### <span class="red">Swap</span>

<div><span class="blue">Type</span> : <span>Partition | File | zram</span></div>



<!---------------------------------------Command-->
#### <span class="red">Command</span>
<table>
<thead><tr>
<th align="center" bgcolor="D1ECCF">Command</th>
<th align="center" bgcolor="D1ECCF">Example</th>
<th align="center" bgcolor="D1ECCF">Explain</th>
</tr></thead>
<tbody>
<tr><td align="center">free</td><td align="center">free -h</td><td align="center">Ram Data</td></tr>
<tr><td align="center">swapon</td><td align="center">swapon</td><td align="center">Show swap location</td></tr>
</tbody>
</table>

