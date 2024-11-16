<div class="md3"> 
<a href="#hash">Hash</a> -
<a href="#cryptography">Cryptography</a>
</div>


<!-----------------------------------------------------------Hash----------------------------------------------------------->
## Hash

![](diagram/hash.jpeg)


<!---------------------------------------Resource-->
#### <span class="red">Resource</span>
General : hash break website

<!---------------------------------------Concept-->
#### <span class="red">Concept</span>
<div class="" align="right" dir="rtl"><div class="md3">
<div class="md4">
<span>یک تابع که یک ورودی بگیرد و همیشه یک خرجی ثابت بابت این ورودی بدهد</span>
<span>چون خروجی‌ ثابت است و ورودی بی‌ نهایت، پس ۱۰۰ درصد ورودی‌های مختلف با خروجی یکسان خواهیم داشت، اما خروجی‌ اینقدر بزرگ که این مساله اصلا مهم نیست</span>
</div>
<div class="md4">salt</div>
</div></div>

<!---------------------------------------Properties-->
#### <span class="red">Properties</span>
Free input size

Specific output length

Efficiency computed

Collision resistance : نتونن ورودی رو جوری تغییر بدن که به هش مورد نظرشون برسن

Hiding : نباید از هش به دیتا برسم

Puzzle friendliness : خیلی سریع تولید نشه

<!---------------------------------------Libreary-->
#### <span class="red">Libreary</span>
sha256

<!---------------------------------------Command-->
#### <span class="red">Command</span>
<table ><tbody>
<tr><td colspan="2" align="center" bgcolor="D1ECCF">General</td></tr>
<tr>
<td  align="center">Power</td>
<td align="center">echo '2^256' | bc</td>
</tr>
</tbody></table>

<table ><tbody>
<tr><td colspan="2" align="center" bgcolor="D1ECCF">Ascii</td></tr>
<tr>
<td  align="center">Convert character to ascii</td>
<td align="center">echo "a" | od -An -t dC | awk '{print $1}'</td>
</tr>
<tr>
<td  align="center">Convert ascii to character</td>
<td align="center">echo 97 | awk '{printf("%c",$1)}'</td>
</tr>
</tbody></table>

<table ><tbody>
<tr><td colspan="2" align="center" bgcolor="D1ECCF">Binary</td></tr>
<tr>
<td  align="center">Convert number to binary</td>
<td align="center">echo "obase=2; 97" | bc</td>
</tr>
<tr>
<td  align="center">Convert binary to number</td>
<td align="center">echo "$((2#1100001))"</td>
</tr>
<tr>
<td  align="center">View file as Binary</td>
<td align="center">xxd -b a.txt</td>
</tr>
</tbody></table>

<table ><tbody>
<tr><td colspan="2" align="center" bgcolor="D1ECCF">Hash</td></tr>
<tr>
<td  align="center">Generate hash from character </td>
<td align="center">echo a | sha256sum</td>
</tr>
<tr>
<td  align="center">Generate hash from file</td>
<td align="center">sha256sum a.txt</td>
</tr>
</tbody></table>

<!---------------------------------------Script-->
#### <span class="red">Script</span>

    import hashlib

    for i in range(1,1000000):

        data='my name is jadi and my 123456 is my student number. ' + str(i)
        m = hashlib.sha256()
        m.update(data.encode('utf-8'))
        hash = m.hexdigest()

        if hash[-4:] == "1111" :
            print('found it ',i, data)
            break



<!-----------------------------------------------------------Cryptography----------------------------------------------------------->
<div class="md1"></div>

## Cryptography

![](diagram/cryptography.jpeg)

<!---------------------------------------Resource-->
#### <span class="red">Resource</span>
General : 
<a href="https://en.wikipedia.org/wiki/Pretty_Good_Privacy" target="_blank">PGP</a> - 
<a href="https://www.openpgp.org/" target="_blank">OpenPGP</a> - 
<a href="https://gnupg.org/" target="_blank">GnuPG</a>
<br> Tutorial :
<a href="https://www.devdungeon.com/content/gpg-tutorial" target="_blank">devdungeon</a> - 
<a href="https://stylesuxx.github.io/steganography/" target="_blank">steganography</a>
<br> Tools :
<a href="http://wot.deedbot.org/" target="_blank">deedbot</a>

Adaptor signature

<!---------------------------------------Concept-->
#### <span class="red">Concept</span>
<div class="" align="right" dir="rtl">
<div >در این سیستم ما ۲ تا کلید داریم، یکی‌ برای رمزنگاری اطلاعات(Public Key) و یکی‌ برای رمزگشایی اطلاعات (Private Key)</div>
<div>فرض کنید ۵ نفر می‌خواهد برای ما به صورت رمزشده اطلاعاتی‌ بفرستند، باید چی‌ کار کنیم ؟</div>
<div>ما (Public Key) را در اختیار همهٔ آنها  قرار میدهیم و آنها با (Public Key) اطلاعاتی‌ را رمزنگاری می‌‌کنند، اطلاعات رمز شده را فقط کسی‌ میتواند رمزگشایی کند که (Private Key) را در اختیار داشته باشد و اون شخص کسی‌ نیست جز خود ما </div>
<div>حالا از کجا بفهمیم که هر پیغام برای چه کسی‌ است ؟</div>
</div>
<div class="md3"></div>
<div class="" align="right" dir="rtl">
<div>
حالا اگر هر کسی‌ بتونه پیغام خودش رو امضا کنه و ما بتونیم امضای هر کسی‌ رو برسی‌ کنیم، میتونیم بفهمیم هر پیغام برای چه کسی‌ هست
پس با استفاده از یک فانکشن که Private_key و Data رو به عنوان ورودی میگیره و یک امضا برای اون دیتا درست می‌کنه، می‌تونیم دیتای خود را امضا کنیم و امضا رو در اختیار دیگران قرار می دهیم تا بررسی کنن اطلاعاتی که بدستشون میرسه از طرف ما هست یا نه
</div>
<div><span>اینجوری امضا می کنیم : </span><span>MySign = Sign(private_key, data)</span></div>
<div><span>اینجوری امضا رو چک می کنیم : </span><span>ValidateSign = Validate(public_key, MySign, data )</span></div>
</div>
<div class="md3"></div>
<div class="" align="right" dir="rtl">
Private Key / Public Key / Revoke Key / Encrypt / Decrypt / Sign / Revoke | Seed phrase
<div class="md4"></div>
</div>


<div align="left" dir="ltr"><span class="blue">Web of trust</span></div>
<div align="right" dir="rtl">
<div class="md4">برای اینکه مطمئن بشیم کلید عمومی که داریم برای شخص مورد نظرمون هست یا نه</div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
<div class="md4"></div>
</div>



<!---------------------------------------Method-->
#### <span class="red">Method</span>
<div align="left" dir="ltr"><span class="blue">Symmetric</span></div>
<div align="right" dir="rtl">در این روش برای رمز کردن اطلاعات و همچنین باز کردن اطلاعات از یک کلید استفاده می‌‌شود</div>
<div align="left" dir="ltr"><span class="blue">Asymmetric</span></div>
<div align="right" dir="rtl">در این روش از یک کلید برای رمز کردن اطلاعات و از یک کلید دیگر برای باز کردن اطلاعات استفاده می‌‌شود</div>
<div align="right" dir="rtl"><span>secp256k1</span> : <span> رمزنگاری منحنی بیضوی</span></div>


<!---------------------------------------Algorithm-->
#### <span class="red">Algorithm</span>
Triple DES

RSA

AES

ECDSA

<!---------------------------------------Libreary-->
#### <span class="red">Libreary</span>
PGP

OpenPGP

GnuPG 

BIP38

<!---------------------------------------Command-->
#### <span class="red">Command</span>
<table ><tbody>
<tr><td colspan="2" align="center" bgcolor="D1ECCF">General</td></tr>
<tr>
<td  align="center">Generate</td>
<td align="center">gpg --full-generate-key</td>
</tr>
<tr>
<td  align="center">List</td>
<td align="center">gpg --list-keys <br> gpg --list-secret-keys</td>
</tr>
<tr>
<td  align="center">Delete</td>
<td align="center">gpg --delete-secret-key morteza <br> gpg --delete-key morteza</td>
</tr>
<tr>
<td  align="center">Import</td>
<td align="center">gpg --import public_key <br> gpg --import private_key <br> gpg --edit-key 79241793755C3E54 <br> trust <br> 5</td>
</tr>
<tr>
<td  align="center">Export</td>
<td align="center">
gpg --export morteza > public_key <br> gpg --export --armor morteza > public_key.asc 
<br><br>
gpg --export-secret-keys morteza > private_key <br> gpg --export-secret-keys --armor morteza > private_key.asc
</td>
</tr>
<tr>
<td  align="center">Encrypted <br> Decrypted</td>
<td align="center">
gpg --out file.encrypted --recipient morteza --encrypt file.original 
<br>
gpg --out file.decrypted --decrypt file.encrypted
</td>
</tr>
<tr>
<td  align="center">Signature</td>
<td align="center">
gpg --local-user morteza --detach-sign --sign --armor --output file.sign file.original 
<br>
gpg --verify file.sign file.original
</td>
</tr>
<tr>
<td  align="center">Revoke</td>
<td align="center">gpg --out file.revoke --gen-revoke morteza</td>
</tr>
<tr>
<td  align="center">Get fingerprint of Publick key</td>
<td align="center">gpg --show-keys ThomasV.asc <br></td>
</tr>

<tr>
<td  align="center">Verify Data With Signature</td>
<td align="center">gpg --import public_key<br>gpg --verify signature data<br></td>
</tr>

</tbody></table>

<!---------------------------------------Script-->
#### <span class="red">Script</span>

https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-1804

    ssh-keygen -t rsa -b 2048
    ssh root@185.177.23.137 mkdir -p .ssh
    cat .ssh/id_rsa.pub | ssh root@185.177.23.137 'cat >> .ssh/authorized_keys'
