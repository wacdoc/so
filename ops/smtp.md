# Dhis server-ka SMTP ee kuu gaar ah

## gogoldhig

SMTP waxa ay si toos ah uga iibsan kartaa adeegyada bixiyayaasha daruuraha, sida:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali Cloud email riix](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Waxaad sidoo kale dhisi kartaa server-kaaga boostada - diris aan xadidneyn, guud ahaan kharash yar.

Hoosta, waxaan ku muujineynaa talaabo talaabo sida loo dhiso server-kayaga boostada.

## Xulashada adeegaha

Seerfarka SMTP ee iskii u martigeliyay wuxuu u baahan yahay IP-ga guud oo leh dekedaha 25, 456, iyo 587 furan.

Daruuraha guud ee sida caadiga ah loo isticmaalo ayaa si caadi ah u xannibay dekedahan, waxaana suuragal ah in la furo iyadoo la soo saarayo amar shaqo, laakiin waa dhibaato aad u weyn.

Waxaan kugula talinayaa inaad ka iibsatid martigeliyaha leh dekedahan furan oo taageera samaynta magacyada domainka.

Halkan, waxaan ku talinayaa [Contabo](https://contabo.com) .

Contabo waa bixiye martigelinaya oo fadhigiisu yahay Munich, Jarmalka, oo la aasaasay 2003 oo leh qiime aad u tartan badan.

Haddii aad u doorato Euro sida lacagta wax lagu gato, qiimuhu wuu ka jaban doonaa (Server leh 8GB xusuusta iyo 4 CPUs ayaa ku kacaya qiyaastii 529 yuan sanadkii, khidmadda rakibida bilowga ah waa bilaash hal sano).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Markaad dalbanayso, hadalku `prefer AMD` , iyo server-ka AMD CPU wuxuu yeelan doonaa waxqabad wanaagsan.

Kuwa soo socda, waxaan u soo qaadan doonaa Contabo's VPS tusaale ahaan si aan u muujiyo sida loo dhiso server-kaaga.

## Qaabeynta nidaamka Ubuntu

Nidaamka hawlgalka halkan waa Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Haddii server-ka ssh uu muujiyo `Welcome to TinyCore 13!` (sida ku cad shaxanka hoose), waxay ka dhigan tahay in nidaamka aan weli la rakibin. Fadlan ka saar ssh oo sug dhowr daqiiqo si aad mar kale u gasho.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Marka `Welcome to Ubuntu 22.04.1 LTS` , bilaabista waa dhammaatay, waxaadna sii wadi kartaa tillaabooyinka soo socda.

### [Ikhtiyaar ah] Bilow deegaanka horumarinta

Talaabadani waa ikhtiyaari.

Si ay ugu habboonaato, waxaan dhigay rakibaadda iyo habaynta nidaamka software ubuntu [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Ku socodsii amarkan soo socda si aad hal guji ugu rakibto.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Isticmaalayaasha Shiinaha, fadlan isticmaal amarka soo socda beddelka, luqadda, aagga waqtiga, iwm. ayaa si toos ah loo dejin doonaa.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo wuxuu awood u siinayaa IPV6

Daar IPV6 si SMTP ay sidoo kale u soo dirto iimayl cinwaannada IPV6.

wax ka beddel `/etc/sysctl.conf`

Wax ka beddel ama ku dar khadadkan soo socda

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Lasoco [tababbarka contabo: Ku darista isku xidhka IPv6 seerkaaga](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Tafatir `/etc/netplan/01-netcfg.yaml` , ku dar dhowr sadar sida ku cad shaxanka hoose (Contabo VPS file design default ayaa horay u lahaa khadadkan, kaliya ku qancin iyaga).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Kadibna `netplan apply` si qaabaynta wax laga beddelay uu dhaqan galo.

Ka dib qaabaynta lagu guulaysto, waxaad isticmaali kartaa `curl 6.ipw.cn` si aad u aragto ciwaanka ipv6 ee shabakadaada dibadda.

## Xir habka kaydinta qaabeynta

```
git clone https://github.com/wactax/ops.soft.git
```

## U samee shahaado SSL oo bilaash ah magacaaga bogga

Diritaanka boostada waxay u baahan tahay shahaado SSL sirta iyo saxiixa.

Waxaan isticmaalnaa [acme.sh](https://github.com/acmesh-official/acme.sh) si aan u soo saarno shahaadooyin.

acme.sh waa qalab saxeexa shahaado toos ah oo furan,

Geli bakhaarka qaabaynta ops.soft, orod `./ssl.sh` , iyo galka `conf` ayaa lagu abuuri doonaa **hagaha sare** .

Ka hel adeeg bixiyahaaga DNS [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , wax ka beddel `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Kadibna orod `./ssl.sh 123.com` si aad u soo saarto shahaadooyinka `123.com` iyo `*.123.com` ee magacaaga domainka.

Socodka kowaad wuxuu si toos ah u rakibi doonaa [acme.sh](https://github.com/acmesh-official/acme.sh) wuxuuna ku dari doonaa hawl qorshaysan oo dib u cusboonaysiin toos ah. Waxaad arki kartaa `crontab -l` , waxaa jira xariiq sidan oo kale ah.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Waddada shahaadada la soo saaray waa wax la mid ah `/mnt/www/.acme.sh/123.com_ecc。`

Cusbooneysiinta shahaadada waxay wici doontaa qoraalka `conf/reload/123.com.sh` , wax ka beddel qoraalkan, waxaad ku dari kartaa amarrada sida `nginx -s reload` si aad u cusbooneysiiso kaydka shahaadada ee codsiyada la xiriira.

## Ku dhis serverka SMTP oo leh chasquid

[chasquid](https://github.com/albertito/chasquid) waa adeeg SMTP il furan oo ku qoran luqadda Go.

Beddelka barnaamijyada boostada qadiimiga ah sida Postfix iyo Sendmail, chasquid waa ka sahlan yahay waana fududahay in la isticmaalo, sidoo kale way u fududahay horumarinta sare.

Run `./chasquid/init.sh 123.com` si toos ah ayaa loogu rakibi doonaa hal gujin (ku beddel 123.com magacaaga soo dirida).

## Habee Saxiixa iimaylka DKIM

DKIM waxa loo isticmaalaa in lagu soo diro saxeexyada iimaylka si looga hortago in xarfaha loola dhaqmo sidii spam.

Ka dib markii amarku si guul leh u socdo, waxaa laguu sheegi doonaa inaad dejiso diiwaanka DKIM (sida hoos ku cad).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Kaliya ku dar diiwaanka TXT DNS-kaaga (sida hoos ku cad).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Eeg heerka adeegga & diiwaannada

 `systemctl status chasquid` Eeg heerka adeega

Xaaladda hawlgalka caadiga ah waa sida ka muuqata sawirka hoose

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` ama `journalctl -xeu chasquid` ayaa arki kara diiwaanka qaladka.

## Dib u habeynta magaca domain

Magaca domainka rogaal celiska ah waa inuu ogolaado ciwaanka IP-ga in lagu xalliyo magaca domainka ee u dhigma.

Dejinta magac domain oo kale waxay ka hortagi kartaa iimaylada in loo aqoonsado spam.

Marka boostada la helo, server-ka helaya wuxuu samayn doonaa falanqaynta magaca domainka ee ciwaanka IP-ga ee serfarka soo diraya si loo xaqiijiyo in serfarka soo diraya leeyahay magac domain oo kale oo ansax ah.

Haddii server-ka soo diraya aanu lahayn magac domain oo kale ah ama haddii magaca domainka ee ka duwan aanu u dhigmin ciwaanka IP-ga ee serfarka soo diraya, server-ka helaya waxa uu u aqoonsan karaa iimaylka inuu yahay spam ama uu diido.

Booqo [https://my.contabo.com/rdns](https://my.contabo.com/rdns) oo habee sida hoos ka muuqata

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Ka dib markii aad dejiso magaca domainka, xasuuso inaad dejiso xallinta hore ee magaca domain ipv4 iyo ipv6 server-ka.

## Wax ka beddel magaca martida loo yahay ee chasquid.conf

Wax ka beddel `conf/chasquid/chasquid.conf` una beddelo qiimaha magaca domainka ee beddelka ah.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Kadibna orod `systemctl restart chasquid` si aad dib ugu bilowdo adeega.

## Ku soo celi conf ilaa git repository

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Tusaale ahaan, waxaan dib ugu soo celiyaa galka conf habka github u gaar ah sida soo socota

Marka hore samee bakhaar gaar ah

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Geli hagaha conf oo u gudbi bakhaarka

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Ku dar soodiraha

orod

```
chasquid-util user-add i@wac.tax
```

Ku dari kara soo diri

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Xaqiiji in erayga sirta ah si sax ah loo dejiyay

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Ka dib marka lagu daro isticmaalaha, `chasquid/domains/wac.tax/users` waa la cusboonaysiin doonaa, xasuuso inaad u gudbiso bakhaarka.

## DNS ku dar diiwaanka SPF

SPF (Siyaasadda Soo-dirida) waa tignoolajiyada xaqiijinta iimaylka ee loo isticmaalo ka hortagga khiyaanada iimaylka.

Waxay xaqiijisaa aqoonsiga soo-diraha iyadoo la hubinayo in cinwaanka IP-ga soo-diraha uu la mid yahay diiwaannada DNS ee magaca domain-ka ee uu sheeganayo inuu yahay, isagoo ka hortagaya khayaanada inay diraan emaillo been abuur ah.

Ku darida diiwaannada SPF waxay ka hortagi kartaa iimaylada in loo aqoonsado spam sida ugu badan ee suurtogalka ah.

Haddii server-ka magacaaga domain uusan taageerin nooca SPF, kaliya ku dar diiwaanka nooca TXT.

Tusaale ahaan, SPF ee `wac.tax` waa sida soo socota

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF ee `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Ogsoonow in aan `include:_spf.google.com` halkan, tani waa sababta oo ah waxaan u habeyn doonaa `i@wac.tax` sidii ciwaanka soo dirida ee sanduuqa boostada Google mar dambe.

## Qaabeynta DNS ee DMARC

DMRC waa soo gaabinta ( Xaqiijinta Fariinta Domain-based, Reporting & Conformance).

Waxaa loo isticmaalaa in lagu qabto SPF bounces (laga yaabee inay sababto khaladaadka qaabeynta, ama qof kale ayaa iska dhigaya inaad dirto spam).

Ku dar diiwaanka TXT `_dmarc` ,

Nuxurku waa sida soo socota

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Halbeeg kasta macnaha uu leeyahay waa sidan soo socota

### p (Siyaasada)

Waxay tuseysaa sida loo maareeyo iimaylada ku guul darreystay xaqiijinta SPF (Siyaasadda Soo-diraha) ama DKIM (DomainKeys Identified Mail). Halbeegga p waxa loo dejin karaa mid ka mid ah saddexda qiime:

* Midna: Wax tallaabo ah lagama qaadin, kaliya natiijada xaqiijinta ayaa dib loogu celinayaa soo-diraha iyada oo loo marayo habka warbixinta iimaylka.
* Karantiil: Geli boostada aan xaqiijin xaqiijinta gal gal spam, laakiin si toos ah uma diidi doonto boostada.
* diid: Si toos ah u diid iimayllada ku guul daraystay xaqiijinta.

### fo (Ikhtiyaarada Fashilka)

Wuxuu qeexayaa cadadka macluumaadka lagu soo celiyay habka warbixinta. Waxaa lagu dejin karaa mid ka mid ah qiyamyada soo socda:

* 0: Ka warbixi natiijooyinka ansaxinta dhammaan fariimaha
* 1: Ka warbixi kaliya fariimaha ku guuldareysta xaqiijinta
* d: Kaliya ka warbixi guul darrooyinka xaqiijinta magaca domain
* s: kaliya ka warbixi guuldarrooyinka xaqiijinta SPF
* l: Keliya ka warbixi guuldarrooyinka xaqiijinta DKIM

### ruca & ruf

* rua (Ka warbixinta URI ee warbixinnada wadarta): Ciwaanka iimaylka ee helitaanka warbixinada la isku daray
* ruf (Ka warbixinta URI ee warbixinnada Forensic): ciwaanka iimaylka si aad u hesho warbixino faahfaahsan

## Ku dar diiwaanka MX si aad ugu gudbiso iimaylada Google Mail

Sababtoo ah maan helin sanduuq boosto shirkadeed oo bilaash ah oo taageera ciwaannada caalamiga ah (Catch-All, waxay heli karaan iimayl kasta oo loo soo diro magaca domainka, iyada oo aan la xaddidin horgalayaasha), waxaan isticmaalay chasquid si aan ugu gudbiyo dhammaan iimaylada sanduuqa boostada Gmail.

**Haddii aad leedahay sanduuqa boostada ee ganacsi ee adiga kuu gaar ah, fadlan ha beddelin MX oo ka bood tallaabadan.**

Wax ka beddel `conf/chasquid/domains/wac.tax/aliases` , deji sanduuqa boostada gudbinta

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` waxay muujinaysaa dhammaan iimaylada, `i` waa horgalaha cinwaanka iimaylka ee isticmaalaha soo diraya ee kor lagu sameeyay. Si loo gudbiyo boostada, isticmaale kastaa wuxuu u baahan yahay inuu ku daro khad.

Kadibna ku dar diiwaanka MX (waxaan si toos ah u tilmaamayaa ciwaanka magaca domainka rogaal celiska ah halkan, sida ku cad xariiqda koowaad ee shaxanka hoose).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Marka qaabaynta la dhammeeyo, waxaad isticmaali kartaa ciwaanno kale oo iimayl si aad iimayllada ugu dirto `i@wac.tax` iyo `any123@wac.tax` si aad u aragto haddii aad ku heli karto iimaylo gudaha Gmail ah.

Haddii kale, hubi log chasquid ( `grep chasquid /var/log/syslog` ).

## U dir emayl i@wac.tax oo wata Google Mail

Ka dib markii Google Mail uu helay boostada, waxaan si dabiici ah u rajaynayay inaan ku jawaabo `i@wac.tax` halkii i.wac.tax@gmail.com.

Booqo [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) oo dhagsii "Ku dar ciwaan kale"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Kadibna, geli lambarka xaqiijinta ee uu helay iimaylka loo soo gudbiyay.

Ugu dambeyntii, waxaa loo dejin karaa sidii ciwaanka soo diraha ee caadiga ah (oo ay la socoto ikhtiyaarka ah in lagu jawaabo isla cinwaanka).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Sidan, waxaanu ku dhamaynay samaynta server-ka SMTP isla markaana aanu isticmaalno Google Mail si aanu u dirno una helno emails.

## Soo dir iimayl tijaabo ah si aad u hubiso in qaabayntu guulaystay

Geli `ops/chasquid`

Orod `direnv allow` in lagu rakibo waxyaalaha ku tiirsanaanta (direnv waxa lagu rakibay hanaan bilow-fureedkii hore oo jillaab ayaa lagu daray qolofka)

dabadeed orod

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Macnaha halbeegyadu waa sida soo socota

* user: SMTP username
* gudbi: SMTP password
* ku: qaata

Waxaad soo diri kartaa iimaylka tijaabada

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Waxaa lagu talinayaa in la isticmaalo Gmail si aad u hesho iimaylo tijaabo ah si loo hubiyo in qaabaynta lagu guulaystay.

### Sirta caadiga ah ee TLS

Sida shaxanka hoose ku cad, waxa jira qufulkan yar, taas oo macnaheedu yahay in shahaadada SSL si guul leh loo hawlgeliyay.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Dabadeed dhagsii "Show Email Original"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Sida ku cad shaxanka hoose, Gmail bogga boostada asalka ah wuxuu soo bandhigayaa DKIM, taas oo macnaheedu yahay in qaabeynta DKIM lagu guuleystay.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Fiiri qaybta la helay ee ciwaanka iimaylka asalka ah, oo waxaad arki kartaa in ciwaanka soo diray yahay IPV6, taas oo macnaheedu yahay in IPV6 sidoo kale loo habeeyey si guul leh.
