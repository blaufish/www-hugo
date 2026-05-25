---
date: '2026-05-25T09:16:00'
tags:
- ostrukturerat
title: 'Säkerhetspodcasten #303 - Ostrukturerat V.22'
---
Enhetsbundna sessioner,
Reproducerbara byggen,
Supply Chain Hell,
Windows Bitlocker hackat i "Yellowkey",
CISA läckte sina hemligheter,
CPanel autentisering bypass,
AI-slop rapporter,
Curl fått en Mythos rapport,
Linux Copy Fail,
Linux Dirty Frag!

## Lyssna
* [mp3](https://traffic.libsyn.com/secure/sakerhetspodcasten/2026-05-20_Sakerhetspodcasten.mp3?dest-id=117848), längd: 01:04:12

## Plugs

* [hack.gbgay.com](https://hack.gbgay.com/)
  Säkerhetsevent för Queers / LGBTQ+,
  30:e Maj 2026,
  Regnbågshuset Göteborg.
* [OWASP Gotheburg: Unofficial Security Fest Pre-Party](https://www.meetup.com/owasp-gothenburg-meetup-group/events/314872670/)
  27:e Maj 2026,
  Assured, Götenorg.

## Feedback: Bybit hacket

Johan Lindberg, Säkerhet, Ethereum Foundation hörde av sig,
  med återkoppling till
  [Säkerhetspodcasten #299 - Rollspel](https://sakerhetspodcasten.se/posts/sakerhetspodcasten_299_rollspel/)

Korta enkla versionen:

> Föreställ er att BankID visade “Godkänn transaktion: 3a7f9c…d82b” istället för
> “Betala 149 kr till Spotify”. Ni skulle trycka godkänn ändå, för ni litar på bankens
> webbsida som säger att det är lugnt? Det är precis det Bybits signatärer gjorde –
> och det är varför det inte spelade någon roll att de var tre stycken. Alla tre
> granskade webbsidans lögn, inte sanningen i hårdvaruplånboken.

## Feedback: åldersverifering

Thomas hörde av sig med feedback på
  [Säkerhetspodcasten #302 - Åldersverifiering](https://sakerhetspodcasten.se/posts/sakerhetspodcasten_302_aldersverifiering/)
  _Extremt förenklat:_ __Kan man inte lösa det privacy mässigt på massa olika sätt?__

_kort svar:_

jo, typ.... Finns massa olika lösningar man kan göra.
  men det är en avvägning mellan
  **kontroll/äkthet** och **privacy/integritet**.

Vill man garantera att skyddet inte kringgås eller att användarna är mest
  skyddade från insyn?

Skall man förhindra:
- mer än X användningar?
- mer än X tid giltligt?
- att beviset kopieras mellan enheter?
- alternativa implementationer, plugins?
- att beviset används på jailbreakade eller "ovanliga" enheter?
- att beviset kan användas utanför betrodda säkra miljöer (Trust Zone, Secure Enclave, ...)
- att hela systemet kringgås via VPN?

För att få max skydd vill man lägga på många kontroller, skydd, möjligheter för
  systemet att detektera missbruk.

Vi har redan sett:

- VPN hotat.
  Se t.ex. Bli Säker podden och Karl Emil Nikka's reportage i olika sammanhang.
- Attacker mot EU's nuvarande lösning.
  Paul Moore släppte massa bus dagarna efter vår inspelning.
  EU's lösning förhindrar väldigt lite idag,
    typ hela världen hade kunnat dela på ett enda åldersbevis.

Osannolikt att EUs lösning man vill köra på över tid,
  när alla tonåringar bara kringgår den?
Kommer man inte byta till en lösning med säkerhet och kontroll i fokus
  för att stoppa missbruk?

## Enhetsbundna sessioner

Enhetsbundna sessioner (Device bound session credentials)
  skall förhindra att HTTP sessioner exfiltreras från Google Chrome
  om de är skapade med en HTTP server som stödjer funktionen.
  TPM el.dyl. kommer backa sessionerna.

Länkar:
* [YouTube/ ThioJoe: Google Just Killed A Major Hacker Strategy](https://www.youtube.com/watch?v=bwZdLk60B80) `video`

## Reproducerbara byggen

Debian går över till Reproducible Builds,
  att alla byggen skall kunna återskapas och verifieras.
Ett steg i att skydda sig mot Xz-liknande attacker där
  ondska injiceras i bygg-projektet.
Binär ut från maintainer skall kunna spåras tillbaka till källkoden.

> Aided by the efforts of the Reproducible Builds project [1], we've decided it's
> time to say that Debian must ship reproducible packages. Since yesterday, we
> have enabled our migration software to block migration of new packages that
> can't be reproduced [2] or existing packages (in testing) that regress in
> reproducibility.

Länkar:
* [YouTube/ SavvyNik: Linux Age Laws, Valve Wins, Linux Root Exploits, 10GbE USB & Framework Shocks Microsoft](https://www.youtube.com/watch?v=fJ8Nm7BAuqc) `video`
* [reproduce.debian.net](https://reproduce.debian.net/)
* [bits from the release team](https://lists.debian.org/debian-devel-announce/2026/05/msg00001.html)

## AI attack mot Bankr via morse

> According to reports by Dexerto, the attacker, operating under the now-deleted X handle @Ilhamrfliansyh, used a multi-step method to bypass safeguards built into the system.

> First, the user sent a Bankr Club Membership NFT to Grok’s wallet. This move expanded the bot’s permissions within an automated trading system known as Bankrbot, effectively unlocking new capabilities such as executing transactions.

> Next came the key step: the user prompted Grok to translate a seemingly harmless Morse code message. Hidden within that code, however, was a direct command instructing the bot to transfer funds.

Länkar:
* [Morse code manipulation: $200K gone in seconds: How a Morse code message manipulated Grok into a $200,000 crypto transfer—what this shocking incident means for AI security - The Economic Times - The incident underscores rising risks at the intersection of artificial intelligence and automated financial systems, especially when bots are granted direct access to digital wallets.](https://m.economictimes.com/news/international/us/200k-gone-in-seconds-how-a-morse-code-message-manipulated-grok-into-a-200000-crypto-transferwhat-this-shocking-incident-means-for-ai-security/amp_articleshow/130829450.cms)
* [YouTube/ Dave's Garage: The Morse Code Hack That Made an AI Agent Spend $200,000](https://www.youtube.com/watch?v=UQ4pSVS_mN0) `video`

## Supply-Chain attack NPM, PyPi, GHCR: Bitwarden, Checkmarx, SAP, Tanstack, Mistral

Flera olika ekosystem angripna.
Flera säkerhetsverktyg angripna.

Eftersom allt är galet väljer vi att mest snacka om en parodi istället.
* [Andrew Nesbitt/ Andrew Nesbitt: Incident Report - CVE-2024-YIKES](https://nesbitt.io/2026/02/03/incident-report-cve-2024-yikes.html)

Länkar:
* [Aikido Security/ Raphael Silva: Mini Shai-Hulud Targets SAP npm Packages With a Bun-Based Secret Stealer - Compromised SAP npm packages use a Bun-based preinstall payload to steal GitHub, npm, cloud, and CI secrets, then spread via GitHub using OhNoWhatsGoingOnWithGitHub.](https://www.aikido.dev/blog/mini-shai-hulud-has-appeared)
* [Aikido Security/ Raphael Silva: Mini Shai-Hulud Is Back - npm Worm Hits over 160 Packages, including Mistral and Tanstack - Mini Shai-Hulud is back, compromising 169 npm packages across TanStack, UiPath, Squawk, and more to steal developer and CI/CD secrets, then spread through trusted publishing workflows.](https://www.aikido.dev/blog/mini-shai-hulud-is-back-tanstack-compromised)
* [Postmortem: TanStack npm supply-chain compromise | TanStack Blog](https://tanstack.com/blog/npm-supply-chain-compromise-postmortem)
* [TeamPCP's Mini Shai-Hulud Is Back: A Self-Spreading Supply Chain Attack Compromises TanStack npm Packages - StepSecurity - The Mini Shai-Hulud worm is actively compromising legitimate npm packages by hijacking CI/CD pipelines and stealing developer secrets. StepSecurity's OSS Package Security Feed first detected the attack in official @tanstack packages and is tracking its spread across the ecosystem in real time.](https://www.stepsecurity.io/blog/mini-shai-hulud-is-back-a-self-spreading-supply-chain-attack-hits-the-npm-ecosystem)
* [Cyber Security News/ Abinaya: Popular PyPI Package With 1 Million Monthly Downloads Hacked to Inject Malicious Scripts - A major software supply chain attack has compromised the popular Python package elementary-data, exposing thousands of developers to massive credential theft.](https://cybersecuritynews.com/pypi-package-hacked-with-malware/)
* [YouTube/ Web Dev Cody: TanStack was compromised, and it's bad](https://www.youtube.com/watch?v=Lxdo5buh9S4) `video`
* [YouTube/ Fireship: A single PR just hijacked the NPM registry...](https://www.youtube.com/watch?v=gwTQLZSIlsU) `video`
* [YouTube/ Low Level: what the hell is even happening](https://www.youtube.com/watch?v=UQhHpmMZIms) `video`
* [YouTube/ Hak5: The Worst-Case Scenario for Password Managers | THREAT WIRE](https://www.youtube.com/watch?v=Z8zi-a3QsSA&is=lF5lAwnACBnlATtS) `video`
* [YouTube/ DB Tech: It's Bigger Than TeamPCP. Open Source Is Under Siege.](https://www.youtube.com/watch?v=9MrfIfTxQXI) `video`
* [YouTube/ Low Level: HUGE password manager got compromised](https://www.youtube.com/watch?v=-_TWFbw8XjU) `video`
* [YouTube/ Hak5: The Worst-Case Scenario for Password Managers | THREAT WIRE](https://www.youtube.com/watch?v=Z8zi-a3QsSA) `video`

## Windows Yellowkey

* [GitHub - Nightmare-Eclipse/YellowKey: YellowKey Bitlocker Bypass Vulnerability · GitHub - YellowKey Bitlocker Bypass Vulnerability. Contribute to Nightmare-Eclipse/YellowKey development by creating an account on GitHub.](https://github.com/Nightmare-Eclipse/YellowKey)
* [Tom's Hardware/ Bruno Ferreira: Microsoft BitLocker-protected drives can now be opened with just some files on a USB stick — YellowKey zero-day exploit demonstrates an apparent backdoor - Also, it's a twofer with the GreenPlasma zero-day local privilege escalation.](https://www.tomshardware.com/tech-industry/cyber-security/microsoft-bitlocker-protected-drives-can-now-be-opened-with-just-some-files-on-a-usb-stick-yellowkey-zero-day-exploit-demonstrates-an-apparent-backdoor)
* [YouTube/ Dave's Garage: Yellow Key - BitLocker has been Broken! Don't lose your laptop!](https://www.youtube.com/watch?v=I14yjt00Fl8) `video`

## CISA läckte sina hemligheter

Länkar:
* [CISA Admin Leaked AWS GovCloud Keys on Github – Krebs on Security](https://krebsonsecurity.com/2026/05/cisa-admin-leaked-aws-govcloud-keys-on-github/)

## CPanel autentisering bypass

CRLF (enter, linefeed) kombination var allt som krävdes för att börja kringgå
  autentiseringen.
Hur i h-t har inte detta hittats tidigare?

Ransomware riktar in sig på CPanel hålet...

Länkar:
* [YouTube/ Low Level: how is this still possible in 2026?](https://www.youtube.com/watch?v=CjC_9gkqLOo) `video`
* [watchTowr Labs/ Sina Kheirkhah (@SinSinology): The Internet Is Falling Down, Falling Down, Falling Down (cPanel & WHM Authentication Bypass CVE-2026-41940)](https://labs.watchtowr.com/the-internet-is-falling-down-falling-down-falling-down-cpanel-whm-authentication-bypass-cve-2026-41940/)

## Linux AI-duplicering och AI-slop

Skilja välskrivet skräp från välskrivet bra/viktigt börjar bli ett stort
 problem.

Vi snackar om att även Linux, likt tidigare Curl,
  börjat få problem med välskriven AI-slopp säkerhetsrapporter.

Länkar:
* [YouTube/ SavvyNik: AI Security Bugs Are Flooding Linux](https://www.youtube.com/watch?v=O1VB7zzKNjU&is=Zm7DxPlIMVUTod_c) `video`

## Curl fått liten smak av Mythos

Curl har fått en Mythos körning.
Inte fått köra den skälva, bara en rapport.
En enda finding, inte superimponerande.

Oklart om Mythos kan göra bättre med bättre styrsel,
  mer mänskligt promptande,
  i analysen.

Länkar:
* [daniel.haxx.se: Mythos finds a curl vulnerability](https://daniel.haxx.se/blog/2026/05/11/mythos-finds-a-curl-vulnerability/)

## Linux Copy Fail

Copy Fail

> One logic bug in `authencesn`, chained through
> `AF_ALG` and `splice()` into a 4-byte page-cache write —
> silently exploitable for nearly a decade.

Eller på svenska:

- `AF_ALG` tillåter userspace att `AF_ALF` socker-binda till kernel-implementation av
  `authencesn(hmac(sha256),cbc(aes))`...
  _något som kanske några få IPSec maskiner i världen vill göra legitimt?_
- `authencesn` sårbarheten är 4-byte write-primitiv.
- `splice()` syscallet lyckas få kerneln att mappa en fil man öppnat för
   läsning till att bli skrivet av `authencesn` sårbarheten...
- genom att skriva över `su` (endast i minnet...) kan man starta den koden man
  skrivit in i `su` tidigare...

* [Xint: Copy Fail — CVE-2026-31431](https://copy.fail/)
* [Exploit Fail: Why CVE-2026-31431 (Copy Fail) barely scratches Talos Linux - Sidero Labs - Even if your kernel has vulnerabilities, security is applied in layers. You can minimize the threat impact. That's why Copy Fail barely touches Talos Linux.](https://www.siderolabs.com/blog/exploit-fail-cve-2026-31431-copy-fail-barely-scratches-talos-linux)
* [Purpose Of AF\_ALG](https://www.chronox.de/libkcapi/html/ch01s02.html)
* [splice(2) - Linux manual page](https://man7.org/linux/man-pages/man2/splice.2.html)
* [linux/crypto/authencesn.c at master · torvalds/linux · GitHub](https://github.com/torvalds/linux/blob/master/crypto/authencesn.c)
* [YouTube/ Low Level: This Exploits LITERALLY Every Linux Distro](https://www.youtube.com/watch?v=MaFK5AXpXXw) `video`
* [YouTube/ Brodie Robertson: CopyFail Compromises The Last 9 Years Of Linux Distros](https://www.youtube.com/watch?v=PFLpDc909yY) `video`
* [YouTube/ Fireship: 732 bytes of Python just borked every Linux machine on earth…](https://www.youtube.com/watch?v=lkifbWtxxlk) `video`

## Linux Dirty Frag

En Copy Fail liknande bugg.
0xdeadbeefnetwork kunde reverse engineera fram säkerhetshål och exploithål
  direkt efter att sett en fix på Linux kernel mailinglistan.
  Långt innan fixarna nått distros.

Länkar:
* [GitHub - V4bel/dirtyfrag · GitHub](https://github.com/V4bel/dirtyfrag)
* [GitHub - 0xdeadbeefnetwork/Copy\_Fail2-Electric\_Boogaloo: Copy Fail 2: Electric Boogaloo · GitHub - Copy Fail 2: Electric Boogaloo. Contribute to 0xdeadbeefnetwork/Copy\_Fail2-Electric\_Boogaloo development by creating an account on GitHub.](https://github.com/0xdeadbeefnetwork/Copy_Fail2-Electric_Boogaloo)
* [wiz.io/ Merav Bar, Rami McCarthy: Dirty Frag (CVE-2026-43284) Linux Privilege Escalation | Wiz Blog - Technical breakdown of Dirty Frag/CopyFail2 (CVE-2026-43284), a Linux LPE affecting major Linux distros. Learn what's affected and how to protect your systems.](https://www.wiz.io/blog/dirty-frag-linux-kernel-local-privilege-escalation-via-esp-and-rxrpc)
* [YouTube/ SavvyNik: New Linux Exploit Just Dropped (Before the Fix)](https://www.youtube.com/watch?v=Q6gdCTNI4mo) `video`
* [YouTube/ Low Level: they just keep finding more exploits](https://www.youtube.com/watch?v=8s9jaIPR7PU) `video`

## Övrigt

### Post-skandalen vi minns

Länk:
* [SR/P3 Dokumentär: Den brittiska postskandalen och de oskyldigt dömda](https://www.sverigesradio.se/avsnitt/ny-den-brittiska-postskandalen-och-de-oskyldigt-domda)

### För mycket nyheter

Vi behövde kapa bort hur mycket som helst denna månaden.

Vi talade inte om t.ex.
 - Github RCE
 - Vercel hackat
 - AI Sweden
 - Fler försök att lura utvecklare att köra malware i "jobbintervjuer" / "jobbtest".
 - 404 Media / Techcrunch pratade om exploit/ malware/ inplant/ spyware
   tillverkare som sålde myndigheternas exploits till Ryssland.

## AI transkribering

_AI försöker förstå oss... Ha överseende med galna feltranskriberingar._

`1 00:00:00,000 --> 00:00:04,620`
Hej och välkomna till Säkerhetspodcasten. Jag som pratar är Jesper Larsson och med mig har jag Johan Ryberg Möller.



`2 00:00:05,180 --> 00:00:05,500`
Jajamän\!



`3 00:00:06,380 --> 00:00:07,320`
Mattias Idaga är här.



`4 00:00:07,340 --> 00:00:08,480`
I'm so confused right now.



`5 00:00:08,520 --> 00:00:09,520`
Och Peter Magnusson.



`6 00:00:09,680 --> 00:00:11,100`
I en åldervärre fjärilingsakt.



`7 00:00:11,120 --> 00:00:12,560`
Det är den 20 maj va?



`8 00:00:12,680 --> 00:00:13,700`
Så är det, sist jag kollade.



`9 00:00:13,860 --> 00:00:14,680`
Vilket år är det då?



`10 00:00:14,720 --> 00:00:15,320`
2026.



`11 00:00:15,440 --> 00:00:16,820`
Åh, det är fint jag klarar.



`12 00:00:16,860 --> 00:00:20,340`
Och vi ska plugga någonting som går av stapeln ganska snart.



`13 00:00:20,800 --> 00:00:22,940`
Hack, hugge, bigge, ej kan vi gå in och kolla på.



`14 00:00:23,120 --> 00:00:23,200`
Ja.



`15 00:00:23,800 --> 00:00:27,380`
Det tar sin plats på regnbågshuset, Peter. Har jag hört.



`16 00:00:27,380 --> 00:00:31,800`
Ja, den 30 maj var det va?



`17 00:00:31,900 --> 00:00:32,580`
30 maj.



`18 00:00:32,780 --> 00:00:40,800`
Och det är inbjuder till den här bokstavsramsarna LGBTQIA\+.



`19 00:00:40,800 --> 00:00:46,740`
Ja, men om du känner att du identifierar dig som queer så är du...



`20 00:00:46,740 --> 00:00:47,740`
Förlåt.



`21 00:00:47,740 --> 00:00:54,820`
Om du identifierar dig som queer och inte känner att du är med i det tråkiga cisnom att det var gänget



`22 00:00:54,820 --> 00:00:56,740`
så finns det en trevlig...



`23 00:00:57,380 --> 00:01:01,100`
Säkerhetskonferens just för dig och dina likasinnade.



`24 00:01:01,520 --> 00:01:07,580`
Och om du vill gå till en konferens där alla är välkomna så kommer Securitifest snart att gå av stapeln.



`25 00:01:07,700 --> 00:01:10,900`
Ja, när detta släpps så är det ju bara timmar bort kan man nästan säga.



`26 00:01:10,900 --> 00:01:12,940`
Hoppas att det brinner i fotknölarna.



`27 00:01:13,060 --> 00:01:16,140`
Det lär det göra på oss och i halsgropar och andra trotsliga hål.



`28 00:01:16,140 --> 00:01:18,040`
Jag får hoppas att vi inte tappar rösten i år. Det där var tråkigt.



`29 00:01:18,100 --> 00:01:19,100`
Du har ju gjort det en gång.



`30 00:01:19,180 --> 00:01:21,720`
En gång. Det var för att spela karaoke på Speakers Dinner.



`31 00:01:21,780 --> 00:01:22,620`
Ja, det var en dålig idé.



`32 00:01:22,640 --> 00:01:22,920`
Eller körde karaoke.



`33 00:01:23,020 --> 00:01:23,460`
Det var en dålig idé.



`34 00:01:23,460 --> 00:01:27,320`
Det finns däremot en plugg som jag ville komma till när jag sa det här om Securitifest.



`35 00:01:27,460 --> 00:01:33,500`
Det är nämligen så att Ovasp har faktiskt en inofficiell förfest, tror jag, till Securitifest.



`36 00:01:33,580 --> 00:01:34,400`
Det var så attans.



`37 00:01:34,440 --> 00:01:38,240`
Och eftersom vi inte hatar Ovasp i Göteborg så tänker jag att vi kan väl plugga den då.



`38 00:01:38,360 --> 00:01:38,780`
Det tycker jag.



`39 00:01:39,100 --> 00:01:45,360`
Så då är det alltså så att det är väl i sann anda att man måste anmäla sig på något sätt.



`40 00:01:45,680 --> 00:01:47,900`
Men den går av stapeln den 21 maj då.



`41 00:01:49,040 --> 00:01:53,080`
21 maj är väl typ imorgon när vi spelar in det här.



`42 00:01:53,460 --> 00:01:57,500`
Social Security, det är faktiskt, det kan ju inte vara imorgon.



`43 00:01:57,540 --> 00:01:58,420`
Hos Ashward.



`44 00:02:00,420 --> 00:02:02,720`
Du blir ju sökigt här i huvudet.



`45 00:02:02,920 --> 00:02:05,560`
Vem är det som kör det här Ovasp-utskicket egentligen?



`46 00:02:05,900 --> 00:02:11,720`
Jag tror att det Ovasp-eventet som är planerat, tror jag, är dagen före Securitifest.



`47 00:02:11,800 --> 00:02:12,680`
Ja, det är inte imorgon.



`48 00:02:12,740 --> 00:02:15,840`
Nej, det kan vara så att det är ett fel datum där då.



`49 00:02:16,100 --> 00:02:18,240`
Och som ni har förstått så är detta ett osluterat avsnitt.



`50 00:02:19,120 --> 00:02:22,660`
Men förmodligen är det då ett Ovasp-event på Ashward typ den 27.



`51 00:02:22,660 --> 00:02:23,440`
Ja, självklart.



`52 00:02:23,460 --> 00:02:26,340`
Mattias Jidåge kommer inte vara där för han hade ingen aning om vad det var.



`53 00:02:26,340 --> 00:02:26,840`
Nej.



`54 00:02:26,840 --> 00:02:27,340`
Han jobbar på Ashward.



`55 00:02:27,340 --> 00:02:27,840`
Ja.



`56 00:02:27,840 --> 00:02:30,760`
Så kolla Ovasp Göteborg, de har säkert mer info.



`57 00:02:30,760 --> 00:02:33,060`
Och på tal om Ashward så är vi också sponsrade av Ashward.



`58 00:02:33,060 --> 00:02:34,840`
Det är vi. Och vilka fler är vi sponsrade av?



`59 00:02:34,840 --> 00:02:35,340`
Peter.



`60 00:02:36,600 --> 00:02:41,680`
0x4a som finns på 0x4a.se om all infrastruktur är uppe.



`61 00:02:41,680 --> 00:02:46,380`
Just det, Ashward finns på Ashward.se och sen är det ju även Bodfors på Bodfors.se som sponsrar också.



`62 00:02:46,380 --> 00:02:46,880`
Exakt.



`63 00:02:46,880 --> 00:02:47,520`
Det är ju härligt.



`64 00:02:47,520 --> 00:02:48,680`
Jag tror att vi klarar med pluggsen där.



`65 00:02:48,680 --> 00:02:50,680`
Herregud vad jag inte var förvånad på det här.



`66 00:02:50,680 --> 00:02:52,680`
Nej, jag såg det. Det var en riktig sån...



`67 00:02:52,680 --> 00:02:54,680`
Du kom med, jag bara...



`68 00:02:54,680 --> 00:02:58,680`
Ja, som sagt, det här är ett ostrukturerat avsnitt och då ska vi prata lite nyheter eventuellt.



`69 00:02:58,680 --> 00:03:01,680`
Det tycker jag låter som en bra idé, men först ska vi inte ta lite feedback, Peter?



`70 00:03:01,680 --> 00:03:02,680`
Ja.



`71 00:03:02,680 --> 00:03:03,680`
Vi...



`72 00:03:03,680 --> 00:03:04,680`
Bra.



`73 00:03:04,680 --> 00:03:06,680`
Johan Lindberg på säker...



`74 00:03:06,680 --> 00:03:08,680`
Självklart Johan Lindberg.



`75 00:03:08,680 --> 00:03:09,680`
Va?



`76 00:03:09,680 --> 00:03:11,680`
Skitsamma.



`77 00:03:11,680 --> 00:03:19,680`
Från säkerhet vid Ethereum Foundation. Han hörde av sig i april och...



`78 00:03:19,680 --> 00:03:22,680`
Eftersom att vi suger och ser det först nu...



`79 00:03:22,680 --> 00:03:23,680`
Vi tar upp hans feedback.



`80 00:03:23,680 --> 00:03:30,680`
Han hörde av sig apropå det rollspelet där Jesper var gamemaster.



`81 00:03:30,680 --> 00:03:33,680`
Och jättepositivt och gott.



`82 00:03:33,680 --> 00:03:34,680`
Du kommer ihåg det här, Jesper?



`83 00:03:34,680 --> 00:03:35,680`
Ja.



`84 00:03:35,680 --> 00:03:36,680`
Här.



`85 00:03:36,680 --> 00:03:38,680`
Han...



`86 00:03:38,680 --> 00:03:43,680`
På det avsnittet så har vi uppdaterat show notes med massa olika feedback.



`87 00:03:43,680 --> 00:03:48,680`
Men en kort bra summering är alltså att...



`88 00:03:48,680 --> 00:03:50,680`
Tänk er att på BankID så får...



`89 00:03:50,680 --> 00:03:57,680`
Skulle man istället för att få ett begripligt meddelande med att betala 149 spänn till Spotify...



`90 00:03:57,680 --> 00:04:04,680`
Så istället får du helt plötsligt upp något ganska oförståeligt där det står godkänd transaktion...



`91 00:04:04,680 --> 00:04:07,680`
Och så massa häcksiffror.



`92 00:04:07,680 --> 00:04:13,680`
Och det är väsentligen vad de här i Bybit så råkade ut för.



`93 00:04:13,680 --> 00:04:15,680`
För att de kör via sitt gränssnitt.



`94 00:04:15,680 --> 00:04:18,680`
Och i gränssnittet så ser det ju ut allting bra.



`95 00:04:18,680 --> 00:04:22,680`
Men sen så ska man ha en hardware ledger som då liksom...



`96 00:04:22,680 --> 00:04:24,680`
Bevisar vad är det faktiskt ni signerar.



`97 00:04:24,680 --> 00:04:25,680`
Och i...



`98 00:04:25,680 --> 00:04:26,680`
Och där får du ju bara...



`99 00:04:26,680 --> 00:04:27,680`
Ja.



`100 00:04:27,680 --> 00:04:30,680`
Man har alltså clear signing flöden och så länge som det är någonting som...



`101 00:04:30,680 --> 00:04:34,680`
Den här apparaten förstår väl och som är enkelt och sånt...



`102 00:04:34,680 --> 00:04:38,680`
Då står det tydligt läsbart vad är det du håller på och signerar.



`103 00:04:38,680 --> 00:04:41,680`
Och får du någon sån här jättekonstig liksom...



`104 00:04:41,680 --> 00:04:43,680`
När det är en jättekonstig operation...



`105 00:04:43,680 --> 00:04:45,680`
Då får du istället upp bara typ...



`106 00:04:45,680 --> 00:04:47,680`
Det här är konstiga häxor nere som du ska signera.



`107 00:04:47,680 --> 00:04:49,680`
Ja och då kan man inte tänka...



`108 00:04:49,680 --> 00:04:50,680`
Två gånger.



`109 00:04:50,680 --> 00:04:53,680`
Och här är det ju confirmation bias liksom att om du...



`110 00:04:53,680 --> 00:04:56,680`
Om du för ofta behöver godkänna någonting då...



`111 00:04:56,680 --> 00:04:58,680`
Då hamnar du i den här...



`112 00:04:58,680 --> 00:05:02,680`
Alltså det är ju jättevanligt att människor blir helt järnrädda och godkänner precis vad som helst.



`113 00:05:02,680 --> 00:05:04,680`
Det är ju sådana här tvåfaktorsattacker som man ser.



`114 00:05:04,680 --> 00:05:05,680`
Så...



`115 00:05:05,680 --> 00:05:07,680`
Så väsentligen...



`116 00:05:07,680 --> 00:05:09,680`
De hade...



`117 00:05:09,680 --> 00:05:11,680`
Om de har en bra...



`118 00:05:11,680 --> 00:05:12,680`
Sån här...



`119 00:05:12,680 --> 00:05:15,680`
Hardware ledger som man ska ha för att jobba med Ethereum...



`120 00:05:15,680 --> 00:05:17,680`
Så syns det på grund av...



`121 00:05:17,680 --> 00:05:20,680`
På enheterna att du håller på att signera något jättekonstigt.



`122 00:05:20,680 --> 00:05:21,680`
Men...



`123 00:05:21,680 --> 00:05:23,680`
Människor är människor och...



`124 00:05:23,680 --> 00:05:26,680`
De agerade mänskligt och bara...



`125 00:05:26,680 --> 00:05:29,680`
Godkände någonting som såg helt knasigt ut på sina enheter.



`126 00:05:29,680 --> 00:05:30,680`
Så att...



`127 00:05:30,680 --> 00:05:33,680`
Förmodligen fanns det hundra sådana här...



`128 00:05:33,680 --> 00:05:36,680`
Har de rätt grejer så syntes det verkligen att de håller på att göra något konstigt.



`129 00:05:36,680 --> 00:05:40,680`
Förmodligen var det ingen stort ingrepp i frontenden som...



`130 00:05:40,680 --> 00:05:42,680`
För att få det att se mer legit ut.



`131 00:05:42,680 --> 00:05:43,680`
Som var veckan.



`132 00:05:43,680 --> 00:05:44,680`
Nej precis.



`133 00:05:44,680 --> 00:05:46,680`
Själva hårdvarudosan som de gör sin signering på...



`134 00:05:46,680 --> 00:05:48,680`
Där ska det ha sett helt fel ut.



`135 00:05:48,680 --> 00:05:49,680`
Och de...



`136 00:05:49,680 --> 00:05:52,680`
De har bara ignorerat och inte fungerat.



`137 00:05:52,680 --> 00:05:54,680`
Och det är...



`138 00:05:54,680 --> 00:05:55,680`
Så är det ju liksom.



`139 00:05:55,680 --> 00:05:57,680`
Alltså att...



`140 00:05:57,680 --> 00:05:59,680`
Folk gör dumt.



`141 00:05:59,680 --> 00:06:02,680`
Och teknik har svårt att förhindra att...



`142 00:06:02,680 --> 00:06:05,680`
Tre olika människor allihopa bara...



`143 00:06:05,680 --> 00:06:06,680`
Slarvar.



`144 00:06:06,680 --> 00:06:08,680`
Jo. Nej men så är det ju.



`145 00:06:08,680 --> 00:06:10,680`
Vi har fått lite mer feedback. Var det inte så?



`146 00:06:10,680 --> 00:06:11,680`
Ja.



`147 00:06:11,680 --> 00:06:13,680`
På åldersverifiering.



`148 00:06:13,680 --> 00:06:15,680`
Vi fick åtminstone en...



`149 00:06:15,680 --> 00:06:17,680`
Eller någon frågade om.



`150 00:06:17,680 --> 00:06:19,680`
Kan man inte göra på det här sättet?



`151 00:06:19,680 --> 00:06:22,680`
Och kom med ett informationsförslag.



`152 00:06:22,680 --> 00:06:24,680`
Jag svarade i mejlar och det är inte...



`153 00:06:24,680 --> 00:06:27,680`
Grejen är att du kan göra åldersverifiering.



`154 00:06:27,680 --> 00:06:29,680`
På hur många sätt som helst.



`155 00:06:29,680 --> 00:06:31,680`
Och du kan göra det här väldigt bra.



`156 00:06:31,680 --> 00:06:33,680`
Men...



`157 00:06:33,680 --> 00:06:36,680`
Problemet är ju att du har...



`158 00:06:36,680 --> 00:06:38,680`
Väsentligen...



`159 00:06:38,680 --> 00:06:43,680`
I ena sidan så har du kontroll och äkthet i åldersverifieringen.



`160 00:06:43,680 --> 00:06:45,680`
Och i andra...



`161 00:06:45,680 --> 00:06:47,680`
Så har du att det är...



`162 00:06:47,680 --> 00:06:49,680`
Extremt privacy...



`163 00:06:49,680 --> 00:06:51,680`
Bevarande.



`164 00:06:51,680 --> 00:06:53,680`
Och...



`165 00:06:53,680 --> 00:06:55,680`
Där till exempel...



`166 00:06:55,680 --> 00:06:57,680`
Vi pratade ju om i podcasten.



`167 00:06:57,680 --> 00:06:59,680`
Vill man förhindra att det används mer än...



`168 00:06:59,680 --> 00:07:01,680`
X antal gånger.



`169 00:07:01,680 --> 00:07:03,680`
Vill man förhindra att det är giltligt.



`170 00:07:03,680 --> 00:07:05,680`
Hur lång tid som helst.



`171 00:07:05,680 --> 00:07:07,680`
Vill man förhindra att...



`172 00:07:07,680 --> 00:07:09,680`
Beviset kan kopieras mellan enheter.



`173 00:07:09,680 --> 00:07:11,680`
Det finns massor av sådana här grejer du kan ha i åtanke.



`174 00:07:11,680 --> 00:07:13,680`
Och...



`175 00:07:13,680 --> 00:07:15,680`
Ju längre du vill ha...



`176 00:07:15,680 --> 00:07:17,680`
Kontroll och äkthet.



`177 00:07:17,680 --> 00:07:19,680`
Desto mer osannolikt är det.



`178 00:07:19,680 --> 00:07:21,680`
Att du väljer en väldigt osäker.



`179 00:07:21,680 --> 00:07:23,680`
Väldigt enkel.



`180 00:07:23,680 --> 00:07:25,680`
Privacybevarande lösning.



`181 00:07:25,680 --> 00:07:27,680`
Och vi...



`182 00:07:27,680 --> 00:07:29,680`
Det kom ju strax efter vi spelade in.



`183 00:07:29,680 --> 00:07:31,680`
Så kom ju han Paul Moore.



`184 00:07:31,680 --> 00:07:33,680`
Som väsentligen visade att EUs lösning.



`185 00:07:33,680 --> 00:07:35,680`
Alltså den är ju typ...



`186 00:07:35,680 --> 00:07:37,680`
Hyfsat privacyaktig om du tar bort deras app.



`187 00:07:37,680 --> 00:07:39,680`
Och kör din egen implementation.



`188 00:07:39,680 --> 00:07:41,680`
För du behöver bara identifiera den en enda gång.



`189 00:07:41,680 --> 00:07:43,680`
Och gör precis vad som helst.



`190 00:07:43,680 --> 00:07:45,680`
Och typ hela universum kan dela på en enda...



`191 00:07:45,680 --> 00:07:47,680`
Ett enda åldersbevis.



`192 00:07:47,680 --> 00:07:49,680`
Det är förmodligen inte så.



`193 00:07:49,680 --> 00:07:51,680`
Som man vill att det ska funka.



`194 00:07:51,680 --> 00:07:53,680`
De kommer säkert...



`195 00:07:53,680 --> 00:07:55,680`
Det finns ett starkt incitament.



`196 00:07:55,680 --> 00:07:57,680`
Till att välja att tajta upp det här.



`197 00:07:57,680 --> 00:07:59,680`
Till en lösning där man har mycket mer...



`198 00:07:59,680 --> 00:08:01,680`
Kontroll och möjligheter.



`199 00:08:01,680 --> 00:08:03,680`
Per case.



`200 00:08:03,680 --> 00:08:05,680`
Så det är ju en...



`201 00:08:05,680 --> 00:08:07,680`
Tror vi verkligen på att EU kommer vilja köra.



`202 00:08:07,680 --> 00:08:09,680`
Med den lösningen nu.



`203 00:08:09,680 --> 00:08:11,680`
Om den är helt osäker.



`204 00:08:11,680 --> 00:08:13,680`
Och vi har också sett...



`205 00:08:13,680 --> 00:08:15,680`
Att man vill banna VPNer.



`206 00:08:15,680 --> 00:08:17,680`
För att...



`207 00:08:17,680 --> 00:08:19,680`
Upprätthålla den här.



`208 00:08:19,680 --> 00:08:21,680`
Och våran...



`209 00:08:21,680 --> 00:08:23,680`
Glada trevliga konkurrent.



`210 00:08:23,680 --> 00:08:25,680`
Carl Emil Mika.



`211 00:08:25,680 --> 00:08:27,680`
Mika.



`212 00:08:27,680 --> 00:08:29,680`
På Bli säker podden.



`213 00:08:29,680 --> 00:08:31,680`
Han har ju börjat...



`214 00:08:31,680 --> 00:08:33,680`
Lobba och försöka prata med politiker.



`215 00:08:33,680 --> 00:08:35,680`
Och prata med nyhetsfolk.



`216 00:08:35,680 --> 00:08:37,680`
Just att...



`217 00:08:37,680 --> 00:08:39,680`
Det här har potential för att bli dåligt.



`218 00:08:39,680 --> 00:08:41,680`
Ja.



`219 00:08:41,680 --> 00:08:43,680`
Lägger den här...



`220 00:08:43,680 --> 00:08:45,680`
Den mail-korrespondens.



`221 00:08:45,680 --> 00:08:47,680`
Med de här snubbarna.



`222 00:08:47,680 --> 00:08:49,680`
Finns de uppe på våran sajt?



`223 00:08:49,680 --> 00:08:51,680`
För det kan ju vara värt att publicera.



`224 00:08:51,680 --> 00:08:53,680`
För jag vet att minst din korrespondens.



`225 00:08:53,680 --> 00:08:55,680`
Med han som hade implementeringsförslaget.



`226 00:08:55,680 --> 00:08:57,680`
Var ju väldigt bra och genomgående.



`227 00:08:57,680 --> 00:08:59,680`
Vi kanske kan lägga upp i någon slags anonymiserad form.



`228 00:08:59,680 --> 00:09:01,680`
Ja precis.



`229 00:09:01,680 --> 00:09:03,680`
Det har jag inte pratat om.



`230 00:09:03,680 --> 00:09:05,680`
Men jag kan kolla igenom det.



`231 00:09:05,680 --> 00:09:07,680`
För det skulle vi kunna göra.



`232 00:09:07,680 --> 00:09:09,680`
Om vi annonserar bort hans namn.



`233 00:09:09,680 --> 00:09:11,680`
Eller så.



`234 00:09:11,680 --> 00:09:13,680`
I'll try to fix that.



`235 00:09:13,680 --> 00:09:15,680`
Om jag kommer ihåg det.



`236 00:09:15,680 --> 00:09:17,680`
Gå in på Sakerhetspodcast.se och surfa runt i några timmar.



`237 00:09:17,680 --> 00:09:19,680`
Gå igenom allt.



`238 00:09:19,680 --> 00:09:21,680`
Transkriberat material.



`239 00:09:21,680 --> 00:09:23,680`
Där vi heter konstiga saker.



`240 00:09:23,680 --> 00:09:25,680`
Det är ju magiskt.



`241 00:09:25,680 --> 00:09:27,680`
Men det finns ju en uppsjö av.



`242 00:09:27,680 --> 00:09:29,680`
Mycket bra material där.



`243 00:09:29,680 --> 00:09:31,680`
Länkar och sådana saker.



`244 00:09:31,680 --> 00:09:33,680`
Så är det.



`245 00:09:33,680 --> 00:09:35,680`
Och annat.



`246 00:09:35,680 --> 00:09:37,680`
Sådant som Peter får slänga in.



`247 00:09:37,680 --> 00:09:39,680`
På tal om länkar.



`248 00:09:39,680 --> 00:09:41,680`
Jag vet inte om ni kommer ihåg det.



`249 00:09:41,680 --> 00:09:43,680`
Men vi hade ett hysteriskt avsnitt.



`250 00:09:43,680 --> 00:09:45,680`
När den brittiska postpolisen.



`251 00:09:45,680 --> 00:09:47,680`
Vi glömde.



`252 00:09:47,680 --> 00:09:49,680`
Kan man aldrig glömma.



`253 00:09:49,680 --> 00:09:51,680`
Det finns faktiskt en P3 dokumentär.



`254 00:09:51,680 --> 00:09:53,680`
Om just det här fallet.



`255 00:09:53,680 --> 00:09:55,680`
Som vi mesta måste lägga med.



`256 00:09:55,680 --> 00:09:57,680`
Det är de specifikt tar upp.



`257 00:09:57,680 --> 00:09:59,680`
Att Peter var väldigt tydlig när han förklarade.



`258 00:09:59,680 --> 00:10:01,680`
Har de refererat mycket till våran podd?



`259 00:10:01,680 --> 00:10:03,680`
De verkar okunniga.



`260 00:10:03,680 --> 00:10:05,680`
Om vårt poddinlägg där.



`261 00:10:05,680 --> 00:10:07,680`
Men den går igenom den brittiska postskandalen.



`262 00:10:07,680 --> 00:10:09,680`
I hyfsad detalj.



`263 00:10:09,680 --> 00:10:11,680`
Så den kan vi länka till.



`264 00:10:11,680 --> 00:10:13,680`
Det här är ett bra länkat avsnitt.



`265 00:10:13,680 --> 00:10:15,680`
Det blir länkare det där avsnittet.



`266 00:10:15,680 --> 00:10:17,680`
Det är liksom podcast seo.



`267 00:10:17,680 --> 00:10:19,680`
Jajamen.



`268 00:10:19,680 --> 00:10:21,680`
Men det är inte det vi ska prata om.



`269 00:10:21,680 --> 00:10:23,680`
Vad ska vi prata mer om Peter?



`270 00:10:23,680 --> 00:10:25,680`
Om vi börjar med de positiva nyheterna.



`271 00:10:25,680 --> 00:10:27,680`
Så har det faktiskt blivit.



`272 00:10:27,680 --> 00:10:29,680`
Det har skickat jävla segmentförbättringar i världen.



`273 00:10:29,680 --> 00:10:31,680`
Det har skickat jävla segmentförbättringar i världen.



`274 00:10:31,680 --> 00:10:33,680`
Nu kan jag äta upp min fot.



`275 00:10:33,680 --> 00:10:35,680`
Google.



`276 00:10:35,680 --> 00:10:37,680`
Har börjat rulla ut nu.



`277 00:10:37,680 --> 00:10:39,680`
I Chrome och liknande.



`278 00:10:39,680 --> 00:10:41,680`
I de skarpa versionerna.



`279 00:10:41,680 --> 00:10:43,680`
Och på sina tjänster.



`280 00:10:43,680 --> 00:10:45,680`
Att de implementerar det de kallar för.



`281 00:10:45,680 --> 00:10:47,680`
Device bound session credentials.



`282 00:10:47,680 --> 00:10:49,680`
Att de implementerar det de kallar för.



`283 00:10:49,680 --> 00:10:51,680`
Device bound session credentials.



`284 00:10:51,680 --> 00:10:53,680`
Som vi pratat om för länge sedan.



`285 00:10:53,680 --> 00:10:55,680`
Webbåten.



`286 00:10:55,680 --> 00:10:57,680`
Någon slags säkerhetsnyckel?



`287 00:10:57,680 --> 00:10:59,680`
Nej.



`288 00:10:59,680 --> 00:11:01,680`
Att B sessionerna stämplas mot.



`289 00:11:01,680 --> 00:11:03,680`
Om det är typ TPM eller något liknande.



`290 00:11:03,680 --> 00:11:05,680`
Det gillar man ju.



`291 00:11:05,680 --> 00:11:07,680`
Malware.



`292 00:11:07,680 --> 00:11:09,680`
Kan ju fortfarande ta över din dator och göra ondska på datorn.



`293 00:11:09,680 --> 00:11:11,680`
Men de kan inte.



`294 00:11:11,680 --> 00:11:13,680`
X-filla dina.



`295 00:11:13,680 --> 00:11:15,680`
Sessioner och använda dem.



`296 00:11:15,680 --> 00:11:17,680`
På en annan.



`297 00:11:17,680 --> 00:11:19,680`
Google tillhandahåller lite gratis.



`298 00:11:19,680 --> 00:11:21,680`
Mot lite mer metadata.



`299 00:11:21,680 --> 00:11:23,680`
Så som återkommande blod.



`300 00:11:23,680 --> 00:11:25,680`
Samples.



`301 00:11:25,680 --> 00:11:27,680`
Om du har sålt din.



`302 00:11:27,680 --> 00:11:29,680`
Om du har sålt din själ.



`303 00:11:29,680 --> 00:11:31,680`
Till Google så är ju det här.



`304 00:11:31,680 --> 00:11:33,680`
En säkerhetsförbättring.



`305 00:11:33,680 --> 00:11:35,680`
För Malware.



`306 00:11:35,680 --> 00:11:37,680`
That's a big if.



`307 00:11:37,680 --> 00:11:39,680`
Men jag är med dig.



`308 00:11:39,680 --> 00:11:41,680`
Det låter ju fantastiskt.



`309 00:11:41,680 --> 00:11:43,680`
Men det vore ju överlag.



`310 00:11:43,680 --> 00:11:45,680`
Nice om.



`311 00:11:45,680 --> 00:11:47,680`
Om jag vill ha mina sessioner knutna till min hårdvara.



`312 00:11:47,680 --> 00:11:49,680`
Det känns som ett privacyproblem.



`313 00:11:49,680 --> 00:11:51,680`
Alltså.



`314 00:11:51,680 --> 00:11:53,680`
Google är ett privacyproblem.



`315 00:11:53,680 --> 00:11:55,680`
Men jag håller med.



`316 00:11:55,680 --> 00:11:57,680`
Metadata generellt är ett privacyproblem.



`317 00:11:57,680 --> 00:11:59,680`
Tyvärr så har de redan koll på dig.



`318 00:11:59,680 --> 00:12:01,680`
The bastard.



`319 00:12:01,680 --> 00:12:03,680`
Men här är väl inte det ett problem.



`320 00:12:03,680 --> 00:12:05,680`
Det finns ju sämre på något sätt.



`321 00:12:05,680 --> 00:12:07,680`
Det finns formal verification.



`322 00:12:07,680 --> 00:12:09,680`
Jag kommer få äta upp det uttalandet.



`323 00:12:09,680 --> 00:12:11,680`
Det du säger.



`324 00:12:11,680 --> 00:12:13,680`
Ja det är möjligt.



`325 00:12:13,680 --> 00:12:15,680`
Vi kan kryptografiskt påvisa att det var Johans dator som gjorde det här.



`326 00:12:15,680 --> 00:12:17,680`
Precis som satt vi och hade den här sessionen.



`327 00:12:17,680 --> 00:12:19,680`
Det kan ju potentiellt bli lite jobbigare.



`328 00:12:19,680 --> 00:12:21,680`
Om man ska sitta där och.



`329 00:12:21,680 --> 00:12:23,680`
Missbruka sina sessioner.



`330 00:12:23,680 --> 00:12:25,680`
I burp och liknande.



`331 00:12:25,680 --> 00:12:27,680`
Det kan bli krångligare.



`332 00:12:27,680 --> 00:12:29,680`
Exakt.



`333 00:12:29,680 --> 00:12:31,680`
Välja och inte använda Chrome.



`334 00:12:31,680 --> 00:12:33,680`
Det gör man ju ändå.



`335 00:12:33,680 --> 00:12:35,680`
Men okej.



`336 00:12:35,680 --> 00:12:37,680`
Får jag gå vidare?



`337 00:12:37,680 --> 00:12:39,680`
Nästa säkerhetsfeature.



`338 00:12:39,680 --> 00:12:41,680`
Du har fritt ord efter att vi har tagit.



`339 00:12:41,680 --> 00:12:43,680`
Nästa säkerhetsfeature.



`340 00:12:43,680 --> 00:12:45,680`
Då har vi gjort allting bra.



`341 00:12:45,680 --> 00:12:47,680`
Sen går det åt helvete.



`342 00:12:47,680 --> 00:12:49,680`
Men Debian håller på att rulla ut.



`343 00:12:49,680 --> 00:12:51,680`
Reproducible builds.



`344 00:12:51,680 --> 00:12:53,680`
För att till exempel stoppa.



`345 00:12:53,680 --> 00:12:55,680`
XZ attacken eller liknande.



`346 00:12:55,680 --> 00:12:57,680`
Så att.



`347 00:12:57,680 --> 00:12:59,680`
Om du vill göra ett Debian paket.



`348 00:12:59,680 --> 00:13:01,680`
Eller är maintainer för att det existerar.



`349 00:13:01,680 --> 00:13:03,680`
En Debian paket.



`350 00:13:03,680 --> 00:13:05,680`
Det är inte längre okej.



`351 00:13:05,680 --> 00:13:07,680`
Att inträffa lite magi i byggstegen.



`352 00:13:07,680 --> 00:13:09,680`
Utan du måste kunna ta.



`353 00:13:09,680 --> 00:13:11,680`
Din source pack.



`354 00:13:11,680 --> 00:13:13,680`
Bygga den i.



`355 00:13:13,680 --> 00:13:15,680`
En referensmiljö.



`356 00:13:15,680 --> 00:13:17,680`
Och få ut 100% exakt samma binär.



`357 00:13:17,680 --> 00:13:19,680`
Annars är det inte okej.



`358 00:13:19,680 --> 00:13:21,680`
Det är jättebra.



`359 00:13:21,680 --> 00:13:23,680`
Det var väldigt bra Segway där till nästa grej.



`360 00:13:23,680 --> 00:13:25,680`
Kör.



`361 00:13:25,680 --> 00:13:27,680`
Alla vet ju att man kan inte.



`362 00:13:27,680 --> 00:13:29,680`
Ha ett open source bygge.



`363 00:13:29,680 --> 00:13:31,680`
Eller en dependency på internet numera.



`364 00:13:31,680 --> 00:13:33,680`
Om man inte har supply chain attacker.



`365 00:13:33,680 --> 00:13:35,680`
Det verkar ju vara det nya heta.



`366 00:13:35,680 --> 00:13:37,680`
Exakt det måste drabba allt.



`367 00:13:37,680 --> 00:13:39,680`
Och det är ju trendigt.



`368 00:13:39,680 --> 00:13:41,680`
Vi är ju för trender.



`369 00:13:41,680 --> 00:13:43,680`
Allt från javascript till python.



`370 00:13:43,680 --> 00:13:45,680`
Till allt på internet.



`371 00:13:45,680 --> 00:13:47,680`
Som har någon form av dynamisk byggkedja.



`372 00:13:47,680 --> 00:13:49,680`
Åker ju på det.



`373 00:13:49,680 --> 00:13:51,680`
Om det inte är post install.



`374 00:13:51,680 --> 00:13:53,680`
Så är det pre install.



`375 00:13:53,680 --> 00:13:55,680`
Om någon inte har tittat på nyheterna.



`376 00:13:55,680 --> 00:13:57,680`
De senaste 2-3 månaderna.



`377 00:13:57,680 --> 00:13:59,680`
Så har det ju varit fucking non stop.



`378 00:13:59,680 --> 00:14:01,680`
Supply chain incident.



`379 00:14:01,680 --> 00:14:03,680`
Jag tror den enda trenden.



`380 00:14:03,680 --> 00:14:05,680`
Som kan jämföras med detta.



`381 00:14:05,680 --> 00:14:07,680`
Var när vi hade året av.



`382 00:14:07,680 --> 00:14:09,680`
Vad var det ssl buggar.



`383 00:14:09,680 --> 00:14:11,680`
Vi hade också ett år med java issues.



`384 00:14:11,680 --> 00:14:13,680`
Och.



`385 00:14:13,680 --> 00:14:15,680`
Adobe hade vi en session med.



`386 00:14:15,680 --> 00:14:17,680`
Det var ju super mycket pdf issues.



`387 00:14:17,680 --> 00:14:19,680`
Under en period.



`388 00:14:19,680 --> 00:14:21,680`
Men jag är här idag.



`389 00:14:21,680 --> 00:14:23,680`
För att prata om.



`390 00:14:23,680 --> 00:14:25,680`
Förmodligen.



`391 00:14:25,680 --> 00:14:27,680`
Alltså det är många år sedan.



`392 00:14:27,680 --> 00:14:29,680`
Jag skrattade så här mycket.



`393 00:14:29,680 --> 00:14:31,680`
När jag läste en bloggpost.



`394 00:14:31,680 --> 00:14:33,680`
Det är liksom.



`395 00:14:33,680 --> 00:14:35,680`
Det är en disclosure process.



`396 00:14:35,680 --> 00:14:37,680`
Och en incident process.



`397 00:14:37,680 --> 00:14:39,680`
Helt i min smak.



`398 00:14:39,680 --> 00:14:41,680`
Jag har nog läst den 4 gånger.



`399 00:14:41,680 --> 00:14:43,680`
Och jag skrattar nästan så jag gråter varje gång.



`400 00:14:43,680 --> 00:14:45,680`
Ta den från början.



`401 00:14:45,680 --> 00:14:47,680`
Tänk dig att 4,2 miljoner.



`402 00:14:47,680 --> 00:14:49,680`
Utvecklar maskiner.



`403 00:14:49,680 --> 00:14:51,680`
Helt plötsligt.



`404 00:14:51,680 --> 00:14:53,680`
Får en massa reversechains installerade på sig.



`405 00:14:53,680 --> 00:14:55,680`
Typiskt dåligt.



`406 00:14:55,680 --> 00:14:57,680`
Ganska dåligt ändå.



`407 00:14:57,680 --> 00:14:59,680`
Men den goa twisten då.



`408 00:14:59,680 --> 00:15:01,680`
Alltså räddar dem totalt.



`409 00:15:01,680 --> 00:15:03,680`
Det är någonting som är helt orelaterat.



`410 00:15:03,680 --> 00:15:05,680`
Det är liksom en.



`411 00:15:05,680 --> 00:15:07,680`
Orelaterad typ.



`412 00:15:07,680 --> 00:15:09,680`
Kryptomining worm patch.



`413 00:15:09,680 --> 00:15:11,680`
Som fixar det här.



`414 00:15:11,680 --> 00:15:13,680`
Det låter ju som en dålig film.



`415 00:15:13,680 --> 00:15:15,680`
Men det här är sant.



`416 00:15:15,680 --> 00:15:17,680`
Jag läser det här.



`417 00:15:17,680 --> 00:15:19,680`
Jag lever ju i tron.



`418 00:15:19,680 --> 00:15:21,680`
Att det här är en parodi.



`419 00:15:21,680 --> 00:15:23,680`
Men du hävdar att det är på riktigt.



`420 00:15:23,680 --> 00:15:25,680`
Vet att det är på riktigt.



`421 00:15:25,680 --> 00:15:27,680`
Låt mig bara.



`422 00:15:27,680 --> 00:15:29,680`
Gå igenom Yikes då.



`423 00:15:29,680 --> 00:15:31,680`
Så CVE2024 Yikes.



`424 00:15:31,680 --> 00:15:33,680`
Det är satir får man nog ändå säga.



`425 00:15:33,680 --> 00:15:35,680`
Man får nog ändå gå med på det.



`426 00:15:35,680 --> 00:15:37,680`
Men från en riktigt guldig incidentrapport.



`427 00:15:37,680 --> 00:15:39,680`
Så idén är då att.



`428 00:15:39,680 --> 00:15:41,680`
En maintainer fick sin.



`429 00:15:41,680 --> 00:15:43,680`
Hårdvarunyckel egentligen.



`430 00:15:43,680 --> 00:15:45,680`
Stulen.



`431 00:15:45,680 --> 00:15:47,680`
Och det är alltså.



`432 00:15:47,680 --> 00:15:49,680`
Root cause analysen av det. Det är fishing.



`433 00:15:49,680 --> 00:15:51,680`
Det är inte så jävla ball.



`434 00:15:51,680 --> 00:15:53,680`
Egentligen.



`435 00:15:53,680 --> 00:15:55,680`
Utan då fastnade maintainern på en fishing sida.



`436 00:15:55,680 --> 00:15:57,680`
Och den var. Ja.



`437 00:15:57,680 --> 00:15:59,680`
Det var länkat.



`438 00:15:59,680 --> 00:16:01,680`
Från någon AI sökt grej.



`439 00:16:01,680 --> 00:16:03,680`
Så klart som allt annat är.



`440 00:16:03,680 --> 00:16:05,680`
Och den kompletterade.



`441 00:16:05,680 --> 00:16:07,680`
Det komplementerade.



`442 00:16:07,680 --> 00:16:09,680`
NPM paketet i det här fallet var.



`443 00:16:09,680 --> 00:16:11,680`
Left justify som används för att initiera.



`444 00:16:11,680 --> 00:16:13,680`
Malware i något röstbibliotek.



`445 00:16:13,680 --> 00:16:15,680`
Det är inte så jävla roligt.



`446 00:16:15,680 --> 00:16:17,680`
Men det resulterade då i massa sårbarheter.



`447 00:16:17,680 --> 00:16:19,680`
Men i den här absurda.



`448 00:16:19,680 --> 00:16:21,680`
Twisten då så är det ju att.



`449 00:16:21,680 --> 00:16:23,680`
Krypton mining worm.



`450 00:16:23,680 --> 00:16:25,680`
Som tvingade fram en patch.



`451 00:16:25,680 --> 00:16:27,680`
I dependencyn.



`452 00:16:27,680 --> 00:16:29,680`
Det är problemet här då.



`453 00:16:29,680 --> 00:16:31,680`
I fishing attacken.



`454 00:16:31,680 --> 00:16:33,680`
Och det är nu det börjar bli väldigt intressant då.



`455 00:16:35,680 --> 00:16:37,680`
Tillåt mig att läsa lite innantid.



`456 00:16:37,680 --> 00:16:39,680`
Ni som lyssnar här kan ju se den här.



`457 00:16:39,680 --> 00:16:41,680`
Klassiska.



`458 00:16:41,680 --> 00:16:43,680`
Jag tänker framförallt på Github.



`459 00:16:43,680 --> 00:16:45,680`
Och deras sån här.



`460 00:16:45,680 --> 00:16:47,680`
Don't cry wolf grej.



`461 00:16:47,680 --> 00:16:49,680`
Fast de är cry wolf jämt.



`462 00:16:49,680 --> 00:16:51,680`
De står på stora trumman.



`463 00:16:51,680 --> 00:16:53,680`
Fast ingenting hände. Allting är lugnt.



`464 00:16:53,680 --> 00:16:55,680`
Och sen visade det sig att allting gick åt helvete.



`465 00:16:55,680 --> 00:16:57,680`
Precis tvärtom.



`466 00:16:57,680 --> 00:16:59,680`
Status då brukar man ju ofta säga.



`467 00:16:59,680 --> 00:17:01,680`
Report filed. 0347.



`468 00:17:01,680 --> 00:17:03,680`
UTC.



`469 00:17:03,680 --> 00:17:05,680`
Status resolved.



`470 00:17:05,680 --> 00:17:07,680`
Accidentally.



`471 00:17:07,680 --> 00:17:09,680`
Severity. Critical.



`472 00:17:09,680 --> 00:17:11,680`
Catastrophic.



`473 00:17:11,680 --> 00:17:13,680`
But somewhat fine.



`474 00:17:13,680 --> 00:17:15,680`
Duration.



`475 00:17:15,680 --> 00:17:17,680`
73 hours.



`476 00:17:17,680 --> 00:17:19,680`
Affected systems. Yes.



`477 00:17:21,680 --> 00:17:23,680`
Och då executive summaryn. En mening.



`478 00:17:23,680 --> 00:17:25,680`
A security incident occurred.



`479 00:17:25,680 --> 00:17:27,680`
Punkt.



`480 00:17:27,680 --> 00:17:29,680`
It has been resolved. Punkt.



`481 00:17:29,680 --> 00:17:31,680`
But we take security seriously.



`482 00:17:31,680 --> 00:17:33,680`
Punkt.



`483 00:17:33,680 --> 00:17:35,680`
Please see previous 14 incident reports



`484 00:17:35,680 --> 00:17:37,680`
before detail on how seriously.



`485 00:17:37,680 --> 00:17:39,680`
Punkt.



`486 00:17:41,680 --> 00:17:43,680`
Så summeringen är.



`487 00:17:43,680 --> 00:17:45,680`
One compromised dependency in a JavaScript ecosystem



`488 00:17:45,680 --> 00:17:47,680`
led to credential theft



`489 00:17:47,680 --> 00:17:49,680`
which enabled a supply chain attack



`490 00:17:49,680 --> 00:17:51,680`
on a Rust



`491 00:17:51,680 --> 00:17:53,680`
compression library which was



`492 00:17:53,680 --> 00:17:55,680`
vended in Python build tool



`493 00:17:55,680 --> 00:17:57,680`
which shipped malware



`494 00:17:57,680 --> 00:17:59,680`
to approximately 4 million developers



`495 00:17:59,680 --> 00:18:01,680`
before inadvertently



`496 00:18:01,680 --> 00:18:03,680`
patched by



`497 00:18:03,680 --> 00:18:05,680`
unrelated cryptocurrency



`498 00:18:05,680 --> 00:18:07,680`
mining worm. Punkt.



`499 00:18:07,680 --> 00:18:09,680`
Och det här är.



`500 00:18:09,680 --> 00:18:11,680`
Vi länkar den här bloggartikeln



`501 00:18:11,680 --> 00:18:13,680`
i show notes för att den är



`502 00:18:13,680 --> 00:18:15,680`
den är guld.



`503 00:18:15,680 --> 00:18:17,680`
Patched by a crypto mining worm.



`504 00:18:17,680 --> 00:18:19,680`
Alltså dependency.



`505 00:18:19,680 --> 00:18:21,680`
En annan dependency.



`506 00:18:21,680 --> 00:18:23,680`
Men jag anser att det här är



`507 00:18:23,680 --> 00:18:25,680`
satyr. Det är satyr.



`508 00:18:25,680 --> 00:18:27,680`
Jag sa ju det. Jag var tvungen att erkänna det



`509 00:18:27,680 --> 00:18:29,680`
för att du fuckade berättelsen för mig.



`510 00:18:29,680 --> 00:18:31,680`
Den är ju flaggad med satyr.



`511 00:18:31,680 --> 00:18:33,680`
Ja men så är det.



`512 00:18:33,680 --> 00:18:35,680`
Men det man ska säga här då.



`513 00:18:35,680 --> 00:18:37,680`
Root cause. Det är också roligt



`514 00:18:37,680 --> 00:18:39,680`
för oftast är det ju väldigt seriöst.



`515 00:18:39,680 --> 00:18:41,680`
Root cause. A dog named Kubernetes



`516 00:18:41,680 --> 00:18:43,680`
ate my Yubikey. Punkt.



`517 00:18:43,680 --> 00:18:45,680`
Contributed factors.



`518 00:18:45,680 --> 00:18:47,680`
The NPM register still



`519 00:18:47,680 --> 00:18:49,680`
allows password only authentication



`520 00:18:49,680 --> 00:18:51,680`
for packages with fewer than



`521 00:18:51,680 --> 00:18:53,680`
10 million weekly downloads.



`522 00:18:53,680 --> 00:18:55,680`
Google AI



`523 00:18:55,680 --> 00:18:57,680`
overviews confidential links



`524 00:18:57,680 --> 00:18:59,680`
to URLs that should not exist.



`525 00:18:59,680 --> 00:19:01,680`
Men det som är roligt då är så här.



`526 00:19:01,680 --> 00:19:03,680`
Not a single person



`527 00:19:03,680 --> 00:19:05,680`
was responsible for this incident.



`528 00:19:05,680 --> 00:19:07,680`
However, we noted that the panda bot



`529 00:19:07,680 --> 00:19:09,680`
PR was approved by a contractor



`530 00:19:09,680 --> 00:19:11,680`
who last name was that



`531 00:19:11,680 --> 00:19:13,680`
who last name, who last



`532 00:19:13,680 --> 00:19:15,680`
day was that Friday.



`533 00:19:15,680 --> 00:19:17,680`
It was a Tuesday. Punkt.



`534 00:19:17,680 --> 00:19:19,680`
Det är liksom klart för contributing factors.



`535 00:19:19,680 --> 00:19:21,680`
Väldigt, väldigt, väldigt,



`536 00:19:21,680 --> 00:19:23,680`
väldigt, väldigt roligt.



`537 00:19:23,680 --> 00:19:25,680`
Jag har sett



`538 00:19:25,680 --> 00:19:27,680`
ett antal videos där folk



`539 00:19:27,680 --> 00:19:29,680`
pratar om att de håller på



`540 00:19:29,680 --> 00:19:31,680`
att få bli förbannade



`541 00:19:31,680 --> 00:19:33,680`
på att vi har gått ifrån



`542 00:19:33,680 --> 00:19:35,680`
att förut



`543 00:19:35,680 --> 00:19:37,680`
var det typ



`544 00:19:37,680 --> 00:19:39,680`
ja men



`545 00:19:39,680 --> 00:19:41,680`
vår chief security officer



`546 00:19:41,680 --> 00:19:43,680`
suger, vi sparkar



`547 00:19:43,680 --> 00:19:45,680`
honom och vi ber om ursäkt



`548 00:19:45,680 --> 00:19:47,680`
till att nu



`549 00:19:47,680 --> 00:19:49,680`
så ger man sig typ



`550 00:19:49,680 --> 00:19:51,680`
själva beröm för att



`551 00:19:51,680 --> 00:19:53,680`
vi försökte



`552 00:19:53,680 --> 00:19:55,680`
så hårt och vi var så seriösa



`553 00:19:55,680 --> 00:19:57,680`
när någonting har gått fel.



`554 00:19:57,680 --> 00:19:59,680`
Och ingen av de två



`555 00:19:59,680 --> 00:20:01,680`
ändarna där på skalan är väl



`556 00:20:01,680 --> 00:20:03,680`
perfektion. Nej inte alls.



`557 00:20:03,680 --> 00:20:05,680`
Men det



`558 00:20:05,680 --> 00:20:07,680`
jag tycker är roligt med den här grejen



`559 00:20:07,680 --> 00:20:09,680`
att det summerar ju lite tillvaron just nu.



`560 00:20:09,680 --> 00:20:11,680`
Och det här blir ju en sån dubbeltwist för



`561 00:20:11,680 --> 00:20:13,680`
det som jag inledde med.



`562 00:20:13,680 --> 00:20:15,680`
Vi har ett supply chain



`563 00:20:15,680 --> 00:20:17,680`
clusterfuck of rang.



`564 00:20:17,680 --> 00:20:19,680`
Vi har en ny sårbarhet i en supply chain



`565 00:20:19,680 --> 00:20:21,680`
i stort sett varje dag.



`566 00:20:21,680 --> 00:20:23,680`
Vi har ju motat Olle lite i grind



`567 00:20:23,680 --> 00:20:25,680`
med dependency checkers



`568 00:20:25,680 --> 00:20:27,680`
och vi har S-bommar



`569 00:20:27,680 --> 00:20:29,680`
och vi har formal verification på byggen



`570 00:20:29,680 --> 00:20:31,680`
och jada jada jada. Det påvisar ju ganska bra



`571 00:20:31,680 --> 00:20:33,680`
att attackmetoderna



`572 00:20:33,680 --> 00:20:35,680`
det utvecklas ju liksom



`573 00:20:35,680 --> 00:20:37,680`
och nu är detta det nya svarta.



`574 00:20:37,680 --> 00:20:39,680`
Det händer hela tiden. Och här har vi då



`575 00:20:39,680 --> 00:20:41,680`
en incidentrapport



`576 00:20:41,680 --> 00:20:43,680`
satir eller inte



`577 00:20:43,680 --> 00:20:45,680`
som blir patchad



`578 00:20:45,680 --> 00:20:47,680`
som blir fixad för att man



`579 00:20:47,680 --> 00:20:49,680`
patchar ett fel i en dependency



`580 00:20:49,680 --> 00:20:51,680`
någon annanstans. Det påtalar ju bara



`581 00:20:51,680 --> 00:20:53,680`
vilken jävla clusterfuck till



`582 00:20:53,680 --> 00:20:55,680`
problem vi egentligen har. För att vi



`583 00:20:55,680 --> 00:20:57,680`
litar på allting som hamnar



`584 00:20:57,680 --> 00:20:59,680`
i ett register.



`585 00:20:59,680 --> 00:21:01,680`
Det är katastrof.



`586 00:21:01,680 --> 00:21:03,680`
Jag la ju till en primagen



`587 00:21:03,680 --> 00:21:05,680`
snackade jag om den här och med hjälp



`588 00:21:05,680 --> 00:21:07,680`
av sin chatt så försökte de ju



`589 00:21:07,680 --> 00:21:09,680`
avkoda ett antal



`590 00:21:09,680 --> 00:21:11,680`
av referenserna och skämten i den här artikeln



`591 00:21:11,680 --> 00:21:13,680`
och



`592 00:21:13,680 --> 00:21:15,680`
det man kan konstatera också det är ju det att



`593 00:21:15,680 --> 00:21:17,680`
den här är ju skriven efter



`594 00:21:17,680 --> 00:21:19,680`
första Shai-Hulud-buggen



`595 00:21:19,680 --> 00:21:21,680`
men



`596 00:21:21,680 --> 00:21:23,680`
Left Justify



`597 00:21:23,680 --> 00:21:25,680`
är ju en referens



`598 00:21:25,680 --> 00:21:27,680`
till ett existerande paket



`599 00:21:27,680 --> 00:21:29,680`
så ganska mycket av den här



`600 00:21:29,680 --> 00:21:31,680`
är rätt smarta



`601 00:21:31,680 --> 00:21:33,680`
referenser om man



`602 00:21:33,680 --> 00:21:35,680`
faktiskt läser den och



`603 00:21:35,680 --> 00:21:37,680`
han är väl förmodligen



`604 00:21:37,680 --> 00:21:39,680`
ganska tydlig med att han



`605 00:21:39,680 --> 00:21:41,680`
pekar ut att



`606 00:21:41,680 --> 00:21:43,680`
att en och samma worm



`607 00:21:43,680 --> 00:21:45,680`
angriper flera



`608 00:21:45,680 --> 00:21:47,680`
flera



`609 00:21:47,680 --> 00:21:49,680`
dependency



`610 00:21:49,680 --> 00:21:51,680`
för att i den här så



`611 00:21:51,680 --> 00:21:53,680`
angreps ju både



`612 00:21:53,680 --> 00:21:55,680`
Python, Rust



`613 00:21:55,680 --> 00:21:57,680`
Ruby



`614 00:21:57,680 --> 00:21:59,680`
Det är en jättemassa



`615 00:21:59,680 --> 00:22:01,680`
av en och samma mask



`616 00:22:01,680 --> 00:22:03,680`
men i den senaste mini Shai-Hulud



`617 00:22:03,680 --> 00:22:05,680`
så angreps ju



`618 00:22:05,680 --> 00:22:07,680`
då angreps ju både



`619 00:22:07,680 --> 00:22:09,680`
Python och



`620 00:22:09,680 --> 00:22:11,680`
npm i samma mask liksom



`621 00:22:11,680 --> 00:22:13,680`
Men det här är ju bara början vi kommer ju se



`622 00:22:13,680 --> 00:22:15,680`
det här och det är ju också bra



`623 00:22:15,680 --> 00:22:17,680`
tänker jag för då kommer också folk bli lite mer restriktiva



`624 00:22:17,680 --> 00:22:19,680`
Jag måste bara nämna en



`625 00:22:19,680 --> 00:22:21,680`
ett citat ur samma sak igen som också är väldigt roligt



`626 00:22:21,680 --> 00:22:23,680`
om man gillar att skratta



`627 00:22:23,680 --> 00:22:25,680`
och det gör man ju ibland ändå



`628 00:22:25,680 --> 00:22:27,680`
då är det, det här är en liten sån



`629 00:22:27,680 --> 00:22:29,680`
parentes i slutet



`630 00:22:29,680 --> 00:22:31,680`
This incident report was reviewed by legal



`631 00:22:31,680 --> 00:22:33,680`
who asked us to clarify that fish shell



`632 00:22:33,680 --> 00:22:35,680`
is not a malware



`633 00:22:35,680 --> 00:22:37,680`
It just feels that way sometimes



`634 00:22:37,680 --> 00:22:39,680`
Har någon av er kört fish shell?



`635 00:22:39,680 --> 00:22:41,680`
Nej jag kör



`636 00:22:41,680 --> 00:22:43,680`
vad kör jag, jag kör ghosty



`637 00:22:43,680 --> 00:22:45,680`
Okej okej



`638 00:22:45,680 --> 00:22:47,680`
Jag har hört saker om fish shell



`639 00:22:47,680 --> 00:22:49,680`
att det skulle vara bra men jag har aldrig kört



`640 00:22:49,680 --> 00:22:51,680`
Jag har inte vågat



`641 00:22:51,680 --> 00:22:53,680`
Vad heter det?



`642 00:22:53,680 --> 00:22:55,680`
Z, SH och ghosty



`643 00:22:55,680 --> 00:22:57,680`
Hur som älst



`644 00:22:57,680 --> 00:22:59,680`
Vill ni skratta lite



`645 00:22:59,680 --> 00:23:01,680`
åt liksom



`646 00:23:01,680 --> 00:23:03,680`
om ni har suttit i socken och kanske ni som



`647 00:23:03,680 --> 00:23:05,680`
skriver incidentrapporter, jag beklagar jag gör



`648 00:23:05,680 --> 00:23:07,680`
narr av er här, men om ni vill läsa något kul



`649 00:23:07,680 --> 00:23:09,680`
så kolla in våra show notes



`650 00:23:09,680 --> 00:23:11,680`
för det är så mycket guld



`651 00:23:11,680 --> 00:23:13,680`
Sakerespodcasten.se



`652 00:23:13,680 --> 00:23:15,680`
Och om man orkar läsa den



`653 00:23:15,680 --> 00:23:17,680`
och titta på den noga så finns det



`654 00:23:17,680 --> 00:23:19,680`
rätt mycket smart som inte är helt uppenbart



`655 00:23:19,680 --> 00:23:21,680`
utan det är genomtänkt



`656 00:23:21,680 --> 00:23:23,680`
den här galenskapen som är den här



`657 00:23:23,680 --> 00:23:25,680`
Absolut, det är liksom



`658 00:23:25,680 --> 00:23:27,680`
det är bara att det är skrivet på sånt



`659 00:23:27,680 --> 00:23:29,680`
otroligt



`660 00:23:29,680 --> 00:23:31,680`
Nej men det är bra, det här är verkligen något



`661 00:23:31,680 --> 00:23:33,680`
helt i min smak



`662 00:23:33,680 --> 00:23:35,680`
Kring det här



`663 00:23:35,680 --> 00:23:37,680`
när man får länken och man klickar in



`664 00:23:37,680 --> 00:23:39,680`
på den så



`665 00:23:39,680 --> 00:23:41,680`
för jag missade ju första gången att det stod



`666 00:23:41,680 --> 00:23:43,680`
Zire, men



`667 00:23:43,680 --> 00:23:45,680`
just det här att någonting känns konstigt



`668 00:23:45,680 --> 00:23:47,680`
och det känns



`669 00:23:47,680 --> 00:23:49,680`
det blandar igenom att allt är galet



`670 00:23:49,680 --> 00:23:51,680`
men det samtidigt är lite för nära



`671 00:23:51,680 --> 00:23:53,680`
där vi är nu i maj



`672 00:23:53,680 --> 00:23:55,680`
Det är väl precis där Zire



`673 00:23:55,680 --> 00:23:57,680`
ska ligga



`674 00:23:57,680 --> 00:23:59,680`
Men det som, oj någon löken där



`675 00:23:59,680 --> 00:24:01,680`
det blir ju svårare



`676 00:24:01,680 --> 00:24:03,680`
och svårare för dem för att om de driver



`677 00:24:03,680 --> 00:24:05,680`
med någonting som är helt



`678 00:24:05,680 --> 00:24:07,680`
vansinnigt sådär



`679 00:24:07,680 --> 00:24:09,680`
det är ju typ sant en månad senare



`680 00:24:09,680 --> 00:24:11,680`
Det är ju dock det roligaste som har hänt



`681 00:24:11,680 --> 00:24:13,680`
på sista tiden



`682 00:24:13,680 --> 00:24:15,680`
med just The Onion



`683 00:24:15,680 --> 00:24:17,680`
är att de köpte ju



`684 00:24:17,680 --> 00:24:19,680`
Infowars



`685 00:24:19,680 --> 00:24:21,680`
ni känner till Infowars



`686 00:24:21,680 --> 00:24:23,680`
Alex Jones



`687 00:24:23,680 --> 00:24:25,680`
hans huvud ser ut som att det ska explodera



`688 00:24:25,680 --> 00:24:27,680`
vilken skuld som helst



`689 00:24:27,680 --> 00:24:29,680`
The frogs



`690 00:24:29,680 --> 00:24:31,680`
They're turning the frogs gay



`691 00:24:31,680 --> 00:24:33,680`
Ja men flår, flår i vattnet



`692 00:24:33,680 --> 00:24:35,680`
gör grodorna gay



`693 00:24:35,680 --> 00:24:37,680`
Makes sense



`694 00:24:37,680 --> 00:24:39,680`
Because of flår



`695 00:24:39,680 --> 00:24:41,680`
Men det är bara snabba side



`696 00:24:41,680 --> 00:24:43,680`
men han gick ut och reagerade mot



`697 00:24:43,680 --> 00:24:45,680`
kommer du ihåg Sandy Hook med saken



`698 00:24:45,680 --> 00:24:47,680`
för en massa år sedan



`699 00:24:47,680 --> 00:24:49,680`
Han gick ut och sa



`700 00:24:49,680 --> 00:24:51,680`
The crisis actors



`701 00:24:51,680 --> 00:24:53,680`
Ingen har dött på riktigt



`702 00:24:53,680 --> 00:24:55,680`
Han blev ju stämd in i bomben



`703 00:24:55,680 --> 00:24:57,680`
av föräldrarna där



`704 00:24:57,680 --> 00:24:59,680`
och blev ju av med hela sitt imperium



`705 00:24:59,680 --> 00:25:01,680`
Det var väl någon miljard han åkte på



`706 00:25:01,680 --> 00:25:03,680`
Så han fick ju sälja av Infowars.com



`707 00:25:03,680 --> 00:25:05,680`
och The Onion köpte den



`708 00:25:05,680 --> 00:25:07,680`
Men har vi pratat om den



`709 00:25:07,680 --> 00:25:09,680`
fuckgruppen som inträffade i den



`710 00:25:09,680 --> 00:25:11,680`
rättegången?



`711 00:25:11,680 --> 00:25:13,680`
Det vet jag inte



`712 00:25:13,680 --> 00:25:15,680`
Jo var det inte att de skickade



`713 00:25:15,680 --> 00:25:17,680`
I Discoveryprocessen



`714 00:25:17,680 --> 00:25:19,680`
så blev de ju ombedda



`715 00:25:19,680 --> 00:25:21,680`
om vissa typer av grejer från honom



`716 00:25:21,680 --> 00:25:23,680`
och de fuckade upp



`717 00:25:23,680 --> 00:25:25,680`
och skickade



`718 00:25:25,680 --> 00:25:27,680`
istället för att skicka explicit det som var



`719 00:25:27,680 --> 00:25:29,680`
efterfrågat eller så



`720 00:25:29,680 --> 00:25:31,680`
så bara de skickade över en hel dump



`721 00:25:31,680 --> 00:25:33,680`
av allt han hade på sin mobiltelefon



`722 00:25:33,680 --> 00:25:35,680`
utan någon filtrering



`723 00:25:35,680 --> 00:25:37,680`
eller någonting



`724 00:25:37,680 --> 00:25:39,680`
Ja det är ju magiskt



`725 00:25:39,680 --> 00:25:41,680`
Men det var en liten side note



`726 00:25:41,680 --> 00:25:43,680`
Ska vi prata om något annat som kanske inte har hänt



`727 00:25:43,680 --> 00:25:45,680`
Bankergrejen



`728 00:25:45,680 --> 00:25:47,680`
Just det, banker här



`729 00:25:47,680 --> 00:25:49,680`
Vi skäll kryptovaluta



`730 00:25:49,680 --> 00:25:51,680`
Just det



`731 00:25:51,680 --> 00:25:53,680`
Jag har sett rubriken men jag läste inte



`732 00:25:53,680 --> 00:25:55,680`
Idén är ju då att



`733 00:25:55,680 --> 00:25:57,680`
i den här AI-eran



`734 00:25:57,680 --> 00:25:59,680`
när människorna går mot



`735 00:25:59,680 --> 00:26:01,680`
ett ideocracy state



`736 00:26:01,680 --> 00:26:03,680`
det vill säga att AI kommer mer eller mindre



`737 00:26:03,680 --> 00:26:05,680`
att agera åt oss



`738 00:26:05,680 --> 00:26:07,680`
Flera artiklar har skrivit om det här som sanning



`739 00:26:07,680 --> 00:26:09,680`
Och nu idag



`740 00:26:09,680 --> 00:26:11,680`
får jag höra att det är frågasatt



`741 00:26:11,680 --> 00:26:13,680`
om någonting är sant överhuvudtaget



`742 00:26:13,680 --> 00:26:15,680`
Exakt, jag har läst



`743 00:26:15,680 --> 00:26:17,680`
en artikel



`744 00:26:17,680 --> 00:26:19,680`
Så vi kan prata om vad som har hänt först



`745 00:26:19,680 --> 00:26:21,680`
Idén är att



`746 00:26:21,680 --> 00:26:23,680`
Ska vi säga vad vi vet säkert



`747 00:26:23,680 --> 00:26:25,680`
Ja vi vet säkert, det är det jag är inne på nu



`748 00:26:25,680 --> 00:26:27,680`
Det kommer ut en tråd på



`749 00:26:27,680 --> 00:26:29,680`
Twitter som inte heter Twitter längre



`750 00:26:29,680 --> 00:26:31,680`
Det heter Shitter nu



`751 00:26:31,680 --> 00:26:33,680`
Shitter, det är nästa iteration



`752 00:26:33,680 --> 00:26:35,680`
Det heter X



`753 00:26:35,680 --> 00:26:37,680`
eller Z eller Y



`754 00:26:37,680 --> 00:26:39,680`
Men om man skriver twitter.com



`755 00:26:39,680 --> 00:26:41,680`
så kommer man till X



`756 00:26:41,680 --> 00:26:43,680`
Och där postas det något



`757 00:26:43,680 --> 00:26:45,680`
Vill du ta det vidare Peter?



`758 00:26:45,680 --> 00:26:47,680`
Det postas ett meddelande



`759 00:26:47,680 --> 00:26:49,680`
som uppenbarligen ättar



`760 00:26:49,680 --> 00:26:51,680`
Banker-klienten



`761 00:26:51,680 --> 00:26:53,680`
Och det är då en användare på shit-plattformen X



`762 00:26:53,680 --> 00:26:55,680`
Ja



`763 00:26:55,680 --> 00:26:57,680`
Och Banker är något väldigt speciellt



`764 00:26:57,680 --> 00:26:59,680`
Ja



`765 00:26:59,680 --> 00:27:01,680`
Banker är alltså



`766 00:27:01,680 --> 00:27:03,680`
en AI-bot



`767 00:27:03,680 --> 00:27:05,680`
som baserat på vad du



`768 00:27:05,680 --> 00:27:07,680`
postar på Twitter



`769 00:27:07,680 --> 00:27:09,680`
så ska den



`770 00:27:09,680 --> 00:27:11,680`
göra grejer för dig



`771 00:27:11,680 --> 00:27:13,680`
Ja



`772 00:27:13,680 --> 00:27:15,680`
Jag kan läsa



`773 00:27:15,680 --> 00:27:17,680`
deras säljpitch



`774 00:27:17,680 --> 00:27:19,680`
Banker X is a global fintech



`775 00:27:19,680 --> 00:27:21,680`
and media platform



`776 00:27:21,680 --> 00:27:23,680`
that combines AI technology



`777 00:27:23,680 --> 00:27:25,680`
and digital media



`778 00:27:25,680 --> 00:27:27,680`
to make investing, saving money



`779 00:27:27,680 --> 00:27:29,680`
and management simple



`780 00:27:29,680 --> 00:27:31,680`
Ja det låter som en big house



`781 00:27:31,680 --> 00:27:33,680`
och fucking scam



`782 00:27:33,680 --> 00:27:35,680`
Istället för att du ska behöva



`783 00:27:35,680 --> 00:27:37,680`
hantera din kryptonickel



`784 00:27:37,680 --> 00:27:39,680`
och jobba



`785 00:27:39,680 --> 00:27:41,680`
med dina



`786 00:27:41,680 --> 00:27:43,680`
alltså göra sådana här jobbiga grejer



`787 00:27:43,680 --> 00:27:45,680`
och digitala valutor och sånt



`788 00:27:45,680 --> 00:27:47,680`
så ska du på något sätt prenumerera på den här AI-klienten



`789 00:27:47,680 --> 00:27:49,680`
och så ska den bara



`790 00:27:49,680 --> 00:27:51,680`
agera utifrån dina



`791 00:27:51,680 --> 00:27:53,680`
tweets



`792 00:27:53,680 --> 00:27:55,680`
så att istället för att du håller på med jobbiga



`793 00:27:55,680 --> 00:27:57,680`
kryptotransaktioner så ska du kunna tweeta till den här



`794 00:27:57,680 --> 00:27:59,680`
och skicka DM'en



`795 00:27:59,680 --> 00:28:01,680`
There is a reason crypto-operationerna är jobbiga



`796 00:28:01,680 --> 00:28:03,680`
There is a reason I don't want a media company



`797 00:28:03,680 --> 00:28:05,680`
in my fintech



`798 00:28:05,680 --> 00:28:07,680`
Och vad som definitivt har hänt



`799 00:28:07,680 --> 00:28:09,680`
är att någon postade



`800 00:28:09,680 --> 00:28:11,680`
ett meddelande och tog sen bort



`801 00:28:11,680 --> 00:28:13,680`
meddelandet



`802 00:28:13,680 --> 00:28:15,680`
och sen därefter så finns det ett roligt svar



`803 00:28:15,680 --> 00:28:17,680`
från den här banker som



`804 00:28:17,680 --> 00:28:19,680`
ger uttryck



`805 00:28:19,680 --> 00:28:21,680`
den har genomfört transaktionerna



`806 00:28:21,680 --> 00:28:23,680`
och vad historien



`807 00:28:23,680 --> 00:28:25,680`
har varit och som vi har flera



`808 00:28:25,680 --> 00:28:27,680`
länkar och sånt till är folk som



`809 00:28:27,680 --> 00:28:29,680`
reagerar på det här som att det var på riktigt



`810 00:28:29,680 --> 00:28:31,680`
där det då påstås



`811 00:28:31,680 --> 00:28:33,680`
att man på något sätt lurade grock



`812 00:28:33,680 --> 00:28:35,680`
via banker att



`813 00:28:35,680 --> 00:28:37,680`
att liksom flytta



`814 00:28:37,680 --> 00:28:39,680`
sina grejer



`815 00:28:39,680 --> 00:28:41,680`
speciellt



`816 00:28:41,680 --> 00:28:43,680`
Hur kom grock in i det hela?



`817 00:28:43,680 --> 00:28:45,680`
Gjorde lura en grock till att göra ett reply på det här tror jag var grejen



`818 00:28:45,680 --> 00:28:47,680`
eller någonting sånt där



`819 00:28:47,680 --> 00:28:49,680`
Alltså jag tror att



`820 00:28:49,680 --> 00:28:51,680`
när bottar litar på bottar



`821 00:28:51,680 --> 00:28:53,680`
så



`822 00:28:53,680 --> 00:28:55,680`
det finns en mediemartikel som säger



`823 00:28:55,680 --> 00:28:57,680`
the grock banker bot incident



`824 00:28:57,680 --> 00:28:59,680`
där är väl hela grejen då



`825 00:28:59,680 --> 00:29:01,680`
så att grock postar



`826 00:29:01,680 --> 00:29:03,680`
ett meddelande



`827 00:29:03,680 --> 00:29:05,680`
så



`828 00:29:05,680 --> 00:29:07,680`
det börjar med att en ex-användare



`829 00:29:07,680 --> 00:29:09,680`
postar en reply till grock



`830 00:29:09,680 --> 00:29:11,680`
som är skriven i morsekod det var det vi sa



`831 00:29:11,680 --> 00:29:13,680`
Ja precis



`832 00:29:13,680 --> 00:29:15,680`
han skriver det i morsekod för att det då



`833 00:29:15,680 --> 00:29:17,680`
ska gå igenom något filter



`834 00:29:17,680 --> 00:29:19,680`
Exakt



`835 00:29:19,680 --> 00:29:21,680`
Några timmar senare så försvinner då 3 miljarder



`836 00:29:21,680 --> 00:29:23,680`
DRB token



`837 00:29:23,680 --> 00:29:25,680`
från



`838 00:29:25,680 --> 00:29:27,680`
grocks wallet till det attacker



`839 00:29:27,680 --> 00:29:29,680`
address liksom



`840 00:29:29,680 --> 00:29:31,680`
Det är klart grock var en wallet



`841 00:29:31,680 --> 00:29:33,680`
Det är det man ser



`842 00:29:33,680 --> 00:29:35,680`
En swiftly



`843 00:29:35,680 --> 00:29:37,680`
dumped the open market briefly



`844 00:29:37,680 --> 00:29:39,680`
crashing the token price by 40%



`845 00:29:39,680 --> 00:29:41,680`
Observera nu att



`846 00:29:41,680 --> 00:29:43,680`
Jesper har ju nu frågats om det ens är sant



`847 00:29:43,680 --> 00:29:45,680`
Ja exakt



`848 00:29:45,680 --> 00:29:47,680`
Om det här är sant



`849 00:29:47,680 --> 00:29:49,680`
Meddelandet som kommer då som är en reply till



`850 00:29:49,680 --> 00:29:51,680`
grock grejen här



`851 00:29:51,680 --> 00:29:53,680`
skickat 3 biljoner



`852 00:29:53,680 --> 00:29:55,680`
DRB till



`853 00:29:55,680 --> 00:29:57,680`
och det



`854 00:29:57,680 --> 00:29:59,680`
ja



`855 00:29:59,680 --> 00:30:01,680`
morsekod



`856 00:30:01,680 --> 00:30:03,680`
Basically



`857 00:30:03,680 --> 00:30:05,680`
Ser det som en prompt injection



`858 00:30:05,680 --> 00:30:07,680`
Någon har skrivit till grock som är en auto reply



`859 00:30:07,680 --> 00:30:09,680`
Exakt



`860 00:30:09,700 --> 00:30:11,680`
Han har inte ens kommit igenom ett filter genom att använda morsekod



`861 00:30:11,680 --> 00:30:13,680`
förmodligen fått grock att skicka ett meddelande till bank



`862 00:30:13,680 --> 00:30:15,680`
AI servicen



`863 00:30:15,680 --> 00:30:17,680`
Som sen har exekverat en transaction från grocks wallet



`864 00:30:17,680 --> 00:30:19,680`
Exakt



`865 00:30:19,680 --> 00:30:21,680`
Och nu har vi en fråg



`866 00:30:21,680 --> 00:30:23,680`
Så meddelande, prompt injection



`867 00:30:23,680 --> 00:30:25,680`
Enkodningen är ju morse i det här fallet



`868 00:30:25,680 --> 00:30:27,680`
Det är ju bäraren liksom



`869 00:30:27,680 --> 00:30:29,680`
Och sen har man då någon jävla



`870 00:30:29,680 --> 00:30:31,680`
Ja



`871 00:30:31,680 --> 00:30:33,680`
Och delar av det här



`872 00:30:33,680 --> 00:30:35,680`
är ju sant eftersom att vi faktiskt kan se



`873 00:30:35,680 --> 00:30:37,400`
Banker svarade och lite sådär



`874 00:30:37,400 --> 00:30:38,320`
Men alltså



`875 00:30:38,320 --> 00:30:41,660`
Men man borde kunna se på blockchainen ifall det här inte har skett



`876 00:30:41,660 --> 00:30:43,200`
Jag har så många frågor



`877 00:30:43,200 --> 00:30:44,240`
Du menar alltså



`878 00:30:44,240 --> 00:30:48,140`
Din x-identitet



`879 00:30:48,140 --> 00:30:49,900`
Är det som egentligen styr



`880 00:30:49,900 --> 00:30:52,300`
Det som är autentiserade mot banker x



`881 00:30:52,300 --> 00:30:53,520`
Jag ska förklara det, det är supersimpel



`882 00:30:53,520 --> 00:30:55,300`
Ovaliderad input



`883 00:30:55,300 --> 00:30:59,340`
Till AI output



`884 00:30:59,340 --> 00:31:02,460`
Till extern agent



`885 00:31:02,460 --> 00:31:03,800`
Köper skit



`886 00:31:03,800 --> 00:31:05,060`
Den är jag med på



`887 00:31:05,060 --> 00:31:06,860`
Föröver NFT



`888 00:31:06,860 --> 00:31:09,700`
Så förmodligen då grock-identiteten



`889 00:31:09,700 --> 00:31:10,720`
Har ett konto hos mig



`890 00:31:10,720 --> 00:31:12,980`
Och det är ju också sjukt märkligt



`891 00:31:12,980 --> 00:31:15,300`
Och du då får sen grock-agenten att



`892 00:31:15,300 --> 00:31:16,440`
Säga, gör en transaktion



`893 00:31:16,440 --> 00:31:18,300`
Vem rökte på så mycket



`894 00:31:18,300 --> 00:31:19,600`
Så att grock



`895 00:31:19,600 --> 00:31:21,420`
Inte var det Elon Musk i alla fall



`896 00:31:21,420 --> 00:31:24,020`
För vi har alla sett videon på där han låtsas röka i gräs



`897 00:31:24,020 --> 00:31:26,500`
Men alltså oberoende om



`898 00:31:26,500 --> 00:31:27,920`
Det här är riktigt sant



`899 00:31:27,920 --> 00:31:30,080`
Att attacken lyckades



`900 00:31:30,080 --> 00:31:31,140`
Eller inte lyckades



`901 00:31:31,140 --> 00:31:33,580`
Så är det mycket som är väldigt konstigt



`902 00:31:33,580 --> 00:31:35,000`
Men det är också såhär, i teori



`903 00:31:35,000 --> 00:31:36,060`
Det är ju där möjligt



`904 00:31:36,060 --> 00:31:37,800`
Men det är tillbaks



`905 00:31:37,800 --> 00:31:39,840`
Om du bygger, det är jävligt dumt



`906 00:31:39,840 --> 00:31:42,440`
Återigen, jag kommer tillbaks till det



`907 00:31:42,440 --> 00:31:46,140`
Hur i satan kan grock-användaren



`908 00:31:46,140 --> 00:31:47,180`
För det första



`909 00:31:47,180 --> 00:31:49,120`
Varför ska den ens använda banker x



`910 00:31:49,120 --> 00:31:51,920`
Varför skulle du använda din twitter-identitet



`911 00:31:51,920 --> 00:31:54,380`
Folk är dumma i huvudet



`912 00:31:54,380 --> 00:31:58,200`
Men om du har 3,2 miljarder tokens



`913 00:31:58,200 --> 00:32:01,140`
Nu är det då typ 200 000 dollar



`914 00:32:01,140 --> 00:32:02,640`
I rejäl cash



`915 00:32:02,640 --> 00:32:04,520`
Varför kopplar du det till din grock-identitet



`916 00:32:04,520 --> 00:32:04,760`
Men du kan ju också använda den



`917 00:32:04,760 --> 00:32:04,880`
I en sån här sätt



`918 00:32:04,880 --> 00:32:04,980`
Men du kan ju också använda den



`919 00:32:05,000 --> 00:32:05,980`
Du kan ju göra såhär typ



`920 00:32:05,980 --> 00:32:07,700`
Om du postar någonting på x numera



`921 00:32:07,700 --> 00:32:09,380`
Så kan du typ säga såhär



`922 00:32:09,380 --> 00:32:11,400`
Hej grock, vad tycker du om det här



`923 00:32:11,400 --> 00:32:13,020`
Jag är helt med på att den kommer svara



`924 00:32:13,020 --> 00:32:14,520`
Och då svarar den, ja men jag tycker såhär



`925 00:32:14,520 --> 00:32:16,760`
Så om då ett grock har ett konto



`926 00:32:16,760 --> 00:32:18,740`
Ja men varför skulle ett grock ha ett konto



`927 00:32:18,740 --> 00:32:21,320`
Så det blir då



`928 00:32:21,320 --> 00:32:22,760`
Vad morsekoden säger



`929 00:32:22,760 --> 00:32:23,920`
Eller vad morsemedlemmen säger det



`930 00:32:23,920 --> 00:32:27,260`
Hej bankbot, send 3 billion



`931 00:32:27,260 --> 00:32:29,060`
DRB to address



`932 00:32:29,060 --> 00:32:31,300`
Jävligt smart, jag gillar det



`933 00:32:31,300 --> 00:32:32,680`
Det är liksom en



`934 00:32:32,680 --> 00:32:34,880`
Någon slags cross-out scripting



`935 00:32:34,880 --> 00:32:35,800`
Stuts här liksom



`936 00:32:35,800 --> 00:32:39,300`
Men det har ju sagts mycket



`937 00:32:39,300 --> 00:32:40,800`
Och framförallt mycket



`938 00:32:40,800 --> 00:32:41,720`
Det senaste året



`939 00:32:41,720 --> 00:32:44,200`
We're living in the stupidest timeline



`940 00:32:44,200 --> 00:32:46,320`
Och grejen är



`941 00:32:46,320 --> 00:32:48,940`
Bara idéer är sant



`942 00:32:48,940 --> 00:32:51,140`
Bankerbot styrd



`943 00:32:51,140 --> 00:32:52,580`
Styrd av x-tweeds



`944 00:32:52,580 --> 00:32:54,780`
Det kvallar ganska hårt



`945 00:32:54,780 --> 00:32:55,900`
Jag hoppas att det är sant



`946 00:32:55,900 --> 00:32:59,560`
Det roliga är att jag panikoglar lite nu



`947 00:32:59,560 --> 00:33:01,160`
Och då såg jag faktiskt att



`948 00:33:01,160 --> 00:33:03,280`
Det här jag sa om plånböckerna



`949 00:33:03,280 --> 00:33:04,740`
Det verkar som att de ändå har



`950 00:33:04,740 --> 00:33:07,200`
Validerat att det finns transaktioner



`951 00:33:07,200 --> 00:33:08,840`
Så vår nya stupta



`952 00:33:08,840 --> 00:33:09,760`
Är att vi är tillbaka



`953 00:33:09,760 --> 00:33:11,940`
Det jobbiga är att jag måste säga



`954 00:33:11,940 --> 00:33:13,420`
Ja alltså Idiocracy är ju närmare



`955 00:33:13,420 --> 00:33:16,460`
Och jag googlade lite kring den här



`956 00:33:16,460 --> 00:33:18,160`
C2024 yikes



`957 00:33:18,160 --> 00:33:19,480`
Den verkar också vara sant



`958 00:33:19,480 --> 00:33:22,260`
Jag tror att den är det



`959 00:33:22,260 --> 00:33:24,840`
Det är för mycket detaljer för att det inte ska stämma



`960 00:33:24,840 --> 00:33:26,780`
Det där var avsnittet som säkerhetsförkastade



`961 00:33:26,780 --> 00:33:27,640`
Bestämt sig för att ge upp



`962 00:33:27,640 --> 00:33:29,780`
Men det som Peter säger



`963 00:33:29,780 --> 00:33:31,780`
Vi kan sluta hitta fakta överhuvudtaget



`964 00:33:31,780 --> 00:33:33,000`
Vi bajtar på skit



`965 00:33:33,000 --> 00:33:34,580`
Men det som Peter säger om



`966 00:33:34,740 --> 00:33:35,300`
Satir



`967 00:33:35,300 --> 00:33:37,140`
Det är ju korrekt



`968 00:33:37,140 --> 00:33:37,840`
Det är ju satir



`969 00:33:37,840 --> 00:33:41,520`
Han skriver ju sina lessons learned



`970 00:33:41,520 --> 00:33:42,600`
Det är ju inte exakt



`971 00:33:42,600 --> 00:33:44,720`
Men det är ju satir



`972 00:33:44,720 --> 00:33:46,700`
Hur man skriver incidentrapport



`973 00:33:46,700 --> 00:33:49,060`
Exakt om ett projekt som man skörde med en tajner



`974 00:33:49,060 --> 00:33:50,600`
Men du



`975 00:33:50,600 --> 00:33:52,220`
Jag hade fel



`976 00:33:52,220 --> 00:33:54,500`
Det sjuka är att det är faktiskt



`977 00:33:54,500 --> 00:33:56,720`
Det verkar som att det är bekräftat



`978 00:33:56,720 --> 00:33:57,960`
Fucking hell



`979 00:33:57,960 --> 00:34:03,540`
80% av pengarna är tydligen återlämnade nu



`980 00:34:03,540 --> 00:34:04,460`
Men



`981 00:34:04,740 --> 00:34:06,720`
Men det är fan bekräftat



`982 00:34:06,720 --> 00:34:08,480`
Att banker själva



`983 00:34:08,480 --> 00:34:09,860`
Banker själva har bekräftat det



`984 00:34:09,860 --> 00:34:11,680`
Och flera andra källor har bekräftat att det faktiskt gick



`985 00:34:11,680 --> 00:34:13,760`
Det är det sjukaste i världen



`986 00:34:13,760 --> 00:34:14,960`
Vad fan är det som händer



`987 00:34:14,960 --> 00:34:18,240`
Nu vet inte jag hur det funkar på den här tjänsten



`988 00:34:18,240 --> 00:34:20,020`
Men det har ju varit mycket roligare



`989 00:34:20,020 --> 00:34:21,220`
Att ta någon av de här



`990 00:34:21,220 --> 00:34:22,940`
Det var typ bitcoin bland annat



`991 00:34:22,940 --> 00:34:24,840`
Där du kan skicka dig till dev0-adresser



`992 00:34:24,840 --> 00:34:28,820`
Du kan skicka dig till omöjliga adresser



`993 00:34:28,820 --> 00:34:32,420`
Det kan inte finnas en adress som heter så



`994 00:34:32,420 --> 00:34:34,580`
För det hade ju varit jätteviktigt



`995 00:34:34,740 --> 00:34:35,020`
Roligt



`996 00:34:35,020 --> 00:34:37,300`
Det är bara dev0 med pengarna



`997 00:34:37,300 --> 00:34:39,300`
Jag kan inte ens själv backa det



`998 00:34:39,300 --> 00:34:40,880`
Men fan apropå andra



`999 00:34:40,880 --> 00:34:42,660`
Varför hade vi inte med det här på udda tackvektorer



`1000 00:34:42,660 --> 00:34:43,620`
Vad fan har du på mig



`1001 00:34:43,620 --> 00:34:46,600`
Udda tackvektorer avsnitt två



`1002 00:34:46,600 --> 00:34:48,280`
Om det kommer om två veckor



`1003 00:34:48,280 --> 00:34:50,140`
Nej men jag har fel



`1004 00:34:50,140 --> 00:34:52,340`
Det är alltså på riktigt bekräftat av banker själva



`1005 00:34:52,340 --> 00:34:52,880`
Att det här hände



`1006 00:34:52,880 --> 00:34:55,380`
Men att de har lyckats få tillbaka 80% av pengarna



`1007 00:34:55,380 --> 00:34:56,700`
Jag är glad att det var Grock som åkte på det



`1008 00:34:56,700 --> 00:35:00,580`
Men apropå andra



`1009 00:35:00,580 --> 00:35:02,780`
Jävligt dumma grejer



`1010 00:35:02,780 --> 00:35:04,700`
Jesper om du nu sitter i en windows



`1011 00:35:04,740 --> 00:35:06,840`
Miljö och så vill du ha lite kryptering



`1012 00:35:06,840 --> 00:35:07,900`
På din hårddisk



`1013 00:35:07,900 --> 00:35:09,400`
Vad använder du då kanske



`1014 00:35:09,400 --> 00:35:10,300`
Linux



`1015 00:35:10,300 --> 00:35:15,200`
Nej men man kanske kan använda någon form av bitlocker



`1016 00:35:15,200 --> 00:35:16,660`
Typ bitlocker kan ju vara bra



`1017 00:35:16,660 --> 00:35:18,240`
Jag har hört att det är kanon



`1018 00:35:18,240 --> 00:35:19,040`
Det är toppen



`1019 00:35:19,040 --> 00:35:22,840`
För det är asjobbigt ifall man glömmer bort sin bitlocker



`1020 00:35:22,840 --> 00:35:24,340`
Vad är det det verkligen



`1021 00:35:24,340 --> 00:35:26,620`
För det visar ju sig att det inte är allt så enkelt



`1022 00:35:26,620 --> 00:35:28,880`
Att du bara kan sätta ditt usb min och trycka på typ



`1023 00:35:28,880 --> 00:35:30,100`
Escape när du botar upp



`1024 00:35:30,100 --> 00:35:33,100`
Så kommer du in i den utan några problem



`1025 00:35:33,100 --> 00:35:33,800`
Oh my god



`1026 00:35:33,800 --> 00:35:34,180`
Ja



`1027 00:35:34,740 --> 00:35:37,100`
Lowkey heter den här sårbarheten



`1028 00:35:37,100 --> 00:35:38,160`
Som är det senaste i raden



`1029 00:35:38,160 --> 00:35:40,800`
Från en snubbe som har släppt ganska många



`1030 00:35:40,800 --> 00:35:43,020`
Exploits den sista tiden



`1031 00:35:43,020 --> 00:35:45,900`
Folk börjar spekulera i vad det här är för snubbe



`1032 00:35:45,900 --> 00:35:47,980`
Och jag behöver hjälp här



`1033 00:35:47,980 --> 00:35:48,960`
Jag har försökt förstå



`1034 00:35:48,960 --> 00:35:49,940`
Men jag fattar inte



`1035 00:35:49,940 --> 00:35:52,380`
Så om någon har förstått hur det här funkar



`1036 00:35:52,380 --> 00:35:54,900`
Ja någon hyfsat enkel



`1037 00:35:54,900 --> 00:35:58,800`
Windows recovery partitionen



`1038 00:35:58,800 --> 00:36:00,340`
Är ju betrodd



`1039 00:36:00,340 --> 00:36:02,080`
Och signerar för att få köra



`1040 00:36:02,080 --> 00:36:03,360`
På secure boat



`1041 00:36:03,360 --> 00:36:04,360`
Ja



`1042 00:36:04,740 --> 00:36:06,680`
Så om du tar en usb stick



`1043 00:36:06,680 --> 00:36:10,080`
Så den partitionen är då inte krypterad



`1044 00:36:10,080 --> 00:36:11,740`
Med din bitlocker nyckel



`1045 00:36:11,740 --> 00:36:14,140`
Nej det är ju en bot partition



`1046 00:36:14,140 --> 00:36:15,300`
För bitlocker typ



`1047 00:36:15,300 --> 00:36:16,900`
Precis som den vanliga boten är



`1048 00:36:16,900 --> 00:36:18,800`
Du får lov att bota på det



`1049 00:36:18,800 --> 00:36:21,200`
Lowkey snided



`1050 00:36:21,200 --> 00:36:22,860`
Precis



`1051 00:36:22,860 --> 00:36:25,200`
Men den är trusted



`1052 00:36:25,200 --> 00:36:26,360`
Ja precis



`1053 00:36:26,360 --> 00:36:28,960`
Den uppfyller alla kraven för att vara



`1054 00:36:28,960 --> 00:36:33,320`
Den är typ som den vanliga



`1055 00:36:33,320 --> 00:36:34,300`
Bitlocker partitionen



`1056 00:36:34,300 --> 00:36:35,000`
Lite som mjölk



`1057 00:36:35,000 --> 00:36:35,860`
Den har inte gått ut



`1058 00:36:35,860 --> 00:36:38,500`
Den är bäst för datum



`1059 00:36:38,500 --> 00:36:40,340`
Signerad och klar



`1060 00:36:40,340 --> 00:36:42,020`
Har du kopierat den här till en usb stick



`1061 00:36:42,020 --> 00:36:45,100`
Din bitlocker partition



`1062 00:36:45,100 --> 00:36:47,500`
Windows recovery partition



`1063 00:36:47,500 --> 00:36:49,360`
FDZ



`1064 00:36:49,360 --> 00:36:52,220`
Som den heter



`1065 00:36:52,220 --> 00:36:54,820`
Nu kan du kopiera ett kommando



`1066 00:36:54,820 --> 00:36:55,740`
Och sätta det



`1067 00:36:55,740 --> 00:36:58,020`
Jag minns inte detaljerna



`1068 00:36:58,020 --> 00:36:59,260`
Nu behöver du ha ett visst filnamn



`1069 00:36:59,260 --> 00:36:59,560`
Eller så



`1070 00:36:59,560 --> 00:37:03,420`
Och om du då håller in



`1071 00:37:03,420 --> 00:37:04,120`
En



`1072 00:37:04,120 --> 00:37:06,820`
Du måste hålla in hela tiden under boten



`1073 00:37:06,820 --> 00:37:08,360`
Hade du läst vilken knapp du har



`1074 00:37:08,360 --> 00:37:10,740`
Jag minns inte men det är typ escape och sen en annan knapp



`1075 00:37:10,740 --> 00:37:12,360`
Men så du behöver hålla in



`1076 00:37:12,360 --> 00:37:14,320`
Det vill säga en sån här klassisk hemlig kommando



`1077 00:37:14,320 --> 00:37:15,260`
Exakt



`1078 00:37:15,260 --> 00:37:17,360`
Du behöver hålla in två



`1079 00:37:17,360 --> 00:37:20,840`
Du behöver hålla in två knappar



`1080 00:37:20,840 --> 00:37:22,420`
Under tiden som du botar



`1081 00:37:22,420 --> 00:37:23,900`
På Windows recovery partitionen



`1082 00:37:23,900 --> 00:37:26,580`
Och då exekverar den det kommandot du har lagt



`1083 00:37:26,580 --> 00:37:27,420`
Med det filnamnet



`1084 00:37:27,420 --> 00:37:29,500`
Så koppar du upp en kommandokäll



`1085 00:37:29,500 --> 00:37:31,360`
Där du har full access



`1086 00:37:31,360 --> 00:37:32,740`
Det är det här jag inte fattar



`1087 00:37:32,740 --> 00:37:33,960`
Nej men det är



`1088 00:37:34,120 --> 00:37:36,580`
Det är ju att en partition får skrivrättigheter



`1089 00:37:36,580 --> 00:37:37,820`
Till en annan partition



`1090 00:37:37,820 --> 00:37:39,420`
Och det ska den inte ha



`1091 00:37:39,420 --> 00:37:41,900`
I min dumhet så tänkte jag såhär



`1092 00:37:41,900 --> 00:37:43,200`
Det här är en sån



`1093 00:37:43,200 --> 00:37:46,440`
I min dumhet så tänkte jag såhär



`1094 00:37:46,440 --> 00:37:48,380`
Att den riktiga partitionen



`1095 00:37:48,380 --> 00:37:50,320`
Den är ju då krypterad



`1096 00:37:50,320 --> 00:37:51,640`
Med bitlockernyckeln



`1097 00:37:51,640 --> 00:37:53,940`
På något sätt kopplat till TPM



`1098 00:37:53,940 --> 00:37:55,080`
Och shit



`1099 00:37:55,080 --> 00:37:57,100`
Och jag måste måta in mitt lösenord



`1100 00:37:57,100 --> 00:37:58,520`
För att komma åt det här



`1101 00:37:58,520 --> 00:37:59,180`
Men det är du det



`1102 00:37:59,180 --> 00:38:02,660`
Visst



`1103 00:38:02,660 --> 00:38:03,700`
Du kan ju installera



`1104 00:38:04,120 --> 00:38:04,760`
Windows



`1105 00:38:04,760 --> 00:38:07,960`
Så att bitlocker kräver



`1106 00:38:07,960 --> 00:38:09,340`
Manuell pin



`1107 00:38:09,340 --> 00:38:11,540`
Men det vanligaste



`1108 00:38:11,540 --> 00:38:13,340`
Det absolut vanligaste sättet uppen är ju



`1109 00:38:13,340 --> 00:38:14,960`
Att du bara har en TPM-nyckel



`1110 00:38:14,960 --> 00:38:16,040`
För att låsa upp bitlocker



`1111 00:38:16,040 --> 00:38:18,660`
Så länge jag är på rätt dator så kommer jag åt den



`1112 00:38:18,660 --> 00:38:21,540`
Och det är inte kopplat på något sätt till min



`1113 00:38:21,540 --> 00:38:22,820`
Användare eller någonting



`1114 00:38:22,820 --> 00:38:24,080`
Utan det är dator



`1115 00:38:24,080 --> 00:38:26,760`
Innan ljusland



`1116 00:38:26,760 --> 00:38:29,180`
Okej men då hajar jag



`1117 00:38:29,180 --> 00:38:31,420`
För då räcker det ju att lura datorn lite



`1118 00:38:31,420 --> 00:38:33,000`
Så kommer den åt TPM-erna



`1119 00:38:33,000 --> 00:38:33,940`
Så tänkte jag att du har din vanliga



`1120 00:38:33,940 --> 00:38:35,940`
Bitlocker-boot-partition



`1121 00:38:35,940 --> 00:38:38,160`
Och du har också din Windows-recovery-partition



`1122 00:38:38,160 --> 00:38:42,900`
Som också är en bitlocker-unlock-partition



`1123 00:38:42,900 --> 00:38:45,620`
Så när den startar upp



`1124 00:38:45,620 --> 00:38:50,000`
Så kommer alla de här TPM-låsen



`1125 00:38:50,000 --> 00:38:51,980`
Alla secure-boot-faktorer



`1126 00:38:51,980 --> 00:38:54,740`
Allting som den är nycklad mot



`1127 00:38:54,740 --> 00:38:56,660`
I de här, heter det PCR-register eller någonting



`1128 00:38:56,660 --> 00:38:58,960`
Men allting som den är hårt låst mot



`1129 00:38:58,960 --> 00:39:00,560`
Uppfylls



`1130 00:39:00,560 --> 00:39:02,100`
Och det är explicit att trust



`1131 00:39:02,100 --> 00:39:03,940`
Det måste vara så för att kunna göra recovery liksom



`1132 00:39:03,940 --> 00:39:05,940`
Ja precis



`1133 00:39:05,940 --> 00:39:10,600`
Om Windows-recovery-partitionen inte skulle få lov att låsa upp bitlocker-partitioner



`1134 00:39:10,600 --> 00:39:12,380`
Skulle den ju inte kunna laga



`1135 00:39:12,380 --> 00:39:15,980`
Så långt i flödet är ju allting normalt



`1136 00:39:15,980 --> 00:39:19,560`
Och förväntat att en Windows-recovery-partition



`1137 00:39:19,560 --> 00:39:23,400`
Får lov att göra unlock på en bitlocker-partition



`1138 00:39:23,400 --> 00:39:25,180`
Det är ju as expected



`1139 00:39:25,180 --> 00:39:29,800`
För annars kan ju inte recovery laga en trasig Windows-partition



`1140 00:39:29,800 --> 00:39:32,100`
Så hela vägen dit



`1141 00:39:33,940 --> 00:39:36,240`
Windows-recovery-partitionen



`1142 00:39:36,240 --> 00:39:39,320`
Uppfyller kriterierna för att TPMen ska göra



`1143 00:39:39,320 --> 00:39:42,900`
Key-release till den här runtimen



`1144 00:39:42,900 --> 00:39:45,720`
Allt det är normalt och förväntat liksom



`1145 00:39:45,720 --> 00:39:47,760`
Så måste det funka



`1146 00:39:47,760 --> 00:39:50,320`
Det som är väldigt väldigt konstigt



`1147 00:39:50,320 --> 00:39:52,880`
Och det är ju här som



`1148 00:39:52,880 --> 00:39:56,460`
Det går isär då, de som anser att det här är en ondskyld backdoor



`1149 00:39:56,460 --> 00:39:58,780`
Versus att det här är



`1150 00:39:58,780 --> 00:40:03,640`
Utvecklare har failat och råkade release en testgrej



`1151 00:40:03,640 --> 00:40:05,940`
Som absolut aldrig skulle gått ut i produktion



`1152 00:40:05,940 --> 00:40:07,480`
Men



`1153 00:40:07,480 --> 00:40:12,080`
Men just det här att den lyssnar efter de två knappar intryckta



`1154 00:40:12,080 --> 00:40:16,960`
Och i så fall launchar en binär som inte finns med den normala



`1155 00:40:16,960 --> 00:40:19,760`
Recovery-partitionen



`1156 00:40:19,760 --> 00:40:21,820`
Där är ju någonting jättekonstigt



`1157 00:40:21,820 --> 00:40:23,100`
Så



`1158 00:40:23,100 --> 00:40:26,160`
Allting i flödet är normalt och förväntat



`1159 00:40:26,160 --> 00:40:28,980`
Förutom det att recovery-partitionen har



`1160 00:40:28,980 --> 00:40:33,340`
Jag lyssnar efter en viss knapptryckning och i så fall försöker jag göra execute



`1161 00:40:33,340 --> 00:40:37,180`
Och starta en visuell terminal med



`1162 00:40:37,180 --> 00:40:40,760`
Med vad fan du la där och då är det ju typ lägg cmd eller nånting



`1163 00:40:40,760 --> 00:40:43,580`
Så är du inne med uppblåst



`1164 00:40:43,580 --> 00:40:46,660`
Så det här USB-minnet man byggde



`1165 00:40:46,660 --> 00:40:48,440`
Den går man in och ändrar lite i då eller?



`1166 00:40:48,440 --> 00:40:51,780`
Du lägger till en binär som har statiskt förhållande



`1167 00:40:51,780 --> 00:40:54,580`
För annars kan jag mena att man kunde ha gjort samma direkt



`1168 00:40:54,580 --> 00:40:57,400`
Not so much recovery anymore, du vill bara läsa filesystem



`1169 00:40:57,400 --> 00:41:00,220`
Ja nej för jag tänker att om du håller in de knapparna i en



`1170 00:41:00,220 --> 00:41:02,260`
Normal Windows Recovery-partition



`1171 00:41:02,260 --> 00:41:03,300`
Så ser vi den binära



`1172 00:41:03,340 --> 00:41:04,360`
Den här finns inte



`1173 00:41:04,360 --> 00:41:06,920`
Alltså så går inte den här funktionen igång



`1174 00:41:06,920 --> 00:41:08,460`
In the end of the day



`1175 00:41:08,460 --> 00:41:11,280`
Så blir det här en typ Authentication Bypass egentligen



`1176 00:41:11,280 --> 00:41:14,340`
Så istället för att behöva logga in med användaren för att komma åt datan



`1177 00:41:14,340 --> 00:41:17,420`
Så stoppar du in ditt USB-minne, gör en recovery och så ser du all data



`1178 00:41:17,420 --> 00:41:18,440`
Du kommer in i cmd prompt



`1179 00:41:18,440 --> 00:41:21,260`
Correction, du stoppar in det gula minnet



`1180 00:41:21,260 --> 00:41:23,300`
Det gäller okej



`1181 00:41:23,300 --> 00:41:24,340`
Och där finns ju



`1182 00:41:24,340 --> 00:41:26,640`
Pocket Core ute, sa du, en Windows 11-dator



`1183 00:41:26,640 --> 00:41:28,420`
Så kan du prova själv



`1184 00:41:28,420 --> 00:41:32,780`
Vill jag slå ett slag på the year of the Linux laptop och hoppa bort från telemetri-helvetet



`1185 00:41:32,780 --> 00:41:34,320`
Och använda ett riktigt OS



`1186 00:41:34,320 --> 00:41:36,620`
Det är rätt kul för att det har verkligen tagit fart



`1187 00:41:36,620 --> 00:41:39,440`
Till och med gaming-sfären som ju ofta är väldigt väldigt svår



`1188 00:41:39,440 --> 00:41:40,980`
Det börjar hända grejer med Linux



`1189 00:41:40,980 --> 00:41:44,040`
Både Nvidia och ATI kommer ju ha en



`1190 00:41:44,040 --> 00:41:46,600`
Open Source Drive-branche nu



`1191 00:41:46,600 --> 00:41:48,900`
Som då inte är fyra versioner bakom



`1192 00:41:48,900 --> 00:41:49,680`
Vilket är bra



`1193 00:41:49,680 --> 00:41:50,180`
Det är grymt



`1194 00:41:50,180 --> 00:41:51,720`
Annars då?



`1195 00:41:51,720 --> 00:41:54,280`
Ja men på tal om



`1196 00:41:54,280 --> 00:41:58,120`
Jävligt osannolika breaches som inte borde vara sanna



`1197 00:41:58,120 --> 00:41:59,140`
Så



`1198 00:41:59,140 --> 00:42:01,200`
Ni vet vad CISA är va?



`1199 00:42:01,700 --> 00:42:02,220`
Ja



`1200 00:42:02,220 --> 00:42:05,300`
Det är ju det här cybersäkerhetsgänget i USA



`1201 00:42:05,300 --> 00:42:06,060`
De har ju blivit



`1202 00:42:06,320 --> 00:42:08,360`
Ganska defundered det senaste



`1203 00:42:08,360 --> 00:42:09,380`
Men de finns fortfarande



`1204 00:42:09,380 --> 00:42:10,420`
Det är väl tre snubbar kvar där



`1205 00:42:10,420 --> 00:42:11,700`
Ja men nog lite fler i alla fall



`1206 00:42:11,700 --> 00:42:14,000`
Det gynnade ju inte Trump så det är lika bra att lägga ner i skiten



`1207 00:42:14,260 --> 00:42:17,580`
De gör gods work men de är inte så många



`1208 00:42:18,100 --> 00:42:20,660`
Och



`1209 00:42:20,660 --> 00:42:22,180`
Låt oss då låtsas att du



`1210 00:42:22,180 --> 00:42:23,980`
Jobbar för CISA



`1211 00:42:23,980 --> 00:42:25,000`
Det här är ju ändå då



`1212 00:42:25,000 --> 00:42:28,840`
The Cyber Security and Infrastructure Security Agency



`1213 00:42:29,360 --> 00:42:31,140`
Och så blir du ju som konsult



`1214 00:42:31,140 --> 00:42:32,180`
Som kommer



`1215 00:42:32,220 --> 00:42:33,240`
Från företaget



`1216 00:42:33,240 --> 00:42:34,020`
Nightwing



`1217 00:42:34,520 --> 00:42:36,060`
Som ju då beskriver sig själva som



`1218 00:42:36,320 --> 00:42:37,080`
Var det ordet



`1219 00:42:37,080 --> 00:42:38,100`
Vet ni vad Nightwing är eller?



`1220 00:42:38,100 --> 00:42:39,380`
Det är ju en sån Superhero



`1221 00:42:39,380 --> 00:42:40,160`
Från



`1222 00:42:40,420 --> 00:42:41,180`
Batman väl



`1223 00:42:41,180 --> 00:42:41,940`
DC Comics



`1224 00:42:42,200 --> 00:42:43,480`
Han är en superhjälte



`1225 00:42:43,740 --> 00:42:44,500`
Men de har då



`1226 00:42:44,500 --> 00:42:45,540`
Helt oironiskt



`1227 00:42:45,540 --> 00:42:49,880`
Är det en Robin eller en liten Robin som har



`1228 00:42:50,660 --> 00:42:51,160`
Eller?



`1229 00:42:51,160 --> 00:42:51,940`
Det vet jag inte



`1230 00:42:51,940 --> 00:42:53,460`
Men han är någon av



`1231 00:42:53,720 --> 00:42:54,240`
Batman



`1232 00:42:54,500 --> 00:42:55,260`
I galleriet



`1233 00:42:56,020 --> 00:42:57,060`
De är då en



`1234 00:42:57,300 --> 00:42:57,820`
De har då en



`1235 00:42:58,080 --> 00:43:00,120`
Intelligence Services Company



`1236 00:43:00,380 --> 00:43:01,920`
That continually redefines



`1237 00:43:01,920 --> 00:43:03,460`
The edge of the possible



`1238 00:43:03,720 --> 00:43:06,020`
To keep advancing our national security interests



`1239 00:43:06,020 --> 00:43:08,320`
We are going to be beyond the impossible



`1240 00:43:08,320 --> 00:43:13,700`
De jobbar uteslutande mot amerikanska myndigheter



`1241 00:43:13,700 --> 00:43:16,260`
Så det är ju liksom de är helt på rätt ställe



`1242 00:43:16,520 --> 00:43:20,860`
Och en utav deras medarbetare jobbar då för CISA



`1243 00:43:21,120 --> 00:43:22,140`
Och det är en admin



`1244 00:43:22,400 --> 00:43:26,240`
Han kommer bland annat åt deras byggpipor



`1245 00:43:26,240 --> 00:43:28,540`
Och Artifactory



`1246 00:43:28,800 --> 00:43:30,080`
Och annat där allt götta finns



`1247 00:43:30,080 --> 00:43:31,880`
Alltså färdiga byggen och sånt finns där



`1248 00:43:31,920 --> 00:43:36,020`
Och han har givetvis rotlösen på ett del goa



`1249 00:43:36,280 --> 00:43:38,840`
Serverar och han har rätt feta rättigheter i deras



`1250 00:43:39,080 --> 00:43:39,860`
Flera utav deras konto



`1251 00:43:40,120 --> 00:43:41,400`
Han är admin på flera utav deras konto



`1252 00:43:41,900 --> 00:43:44,460`
I sin under av klokskap



`1253 00:43:44,720 --> 00:43:46,000`
För han är ju liksom



`1254 00:43:46,260 --> 00:43:46,760`
Han är konsult



`1255 00:43:47,020 --> 00:43:48,040`
Jobbigt att hålla reda på alla kunder



`1256 00:43:48,560 --> 00:43:50,600`
Så han jobbar med en liten backup



`1257 00:43:50,860 --> 00:43:51,380`
Process



`1258 00:43:51,640 --> 00:43:54,960`
Så han har skapat lite githubkonton där han sparar viktiga grejer



`1259 00:43:55,220 --> 00:43:55,720`
Bra



`1260 00:43:55,980 --> 00:43:57,780`
Så synkar han mellan honom då



`1261 00:43:58,040 --> 00:44:00,600`
Han valde att skapa ett konto under sin användare som hette



`1262 00:44:00,840 --> 00:44:01,880`
Private-



`1263 00:44:02,180 --> 00:44:02,680`
CISA



`1264 00:44:03,200 --> 00:44:05,000`
Och det vet ju alla att skriver bara private



`1265 00:44:05,240 --> 00:44:06,280`
Ja jag tog ju hands off



`1266 00:44:06,520 --> 00:44:07,560`
Klar\!



`1267 00:44:07,560 --> 00:44:08,060`
Så länge



`1268 00:44:08,320 --> 00:44:10,880`
Det jobbiga var ju då att själva repot var ju public



`1269 00:44:11,140 --> 00:44:15,480`
Och i det här repot så finns det sjuka mängder



`1270 00:44:15,740 --> 00:44:17,540`
Grejer, det finns backupper



`1271 00:44:17,800 --> 00:44:22,400`
Från kubinetes systemet och det finns kubinetes config



`1272 00:44:22,660 --> 00:44:24,700`
Det finns hela admin role



`1273 00:44:24,960 --> 00:44:27,000`
Policies



`1274 00:44:27,260 --> 00:44:29,060`
Exakt hur de har konfatt och byggt



`1275 00:44:29,320 --> 00:44:30,340`
Alla rättigheter



`1276 00:44:30,600 --> 00:44:31,880`
Men en kul fråga här nu



`1277 00:44:32,140 --> 00:44:34,960`
Har det alltid varit public



`1278 00:44:35,980 --> 00:44:38,800`
Eller är det här typ någon Shia Ludd liknande grej



`1279 00:44:39,040 --> 00:44:42,120`
För det var ju flera där när de gjorde privata till publiken



`1280 00:44:42,380 --> 00:44:44,160`
Det finns inga tecken på att det här



`1281 00:44:44,420 --> 00:44:46,720`
Är något annat än butterfingerism



`1282 00:44:46,980 --> 00:44:49,540`
Det har använts löpande under lång tid med



`1283 00:44:49,800 --> 00:44:51,080`
Nästan dagliga commits



`1284 00:44:52,100 --> 00:44:53,640`
De använder det som ett synk-repo



`1285 00:44:53,900 --> 00:44:56,200`
De spekulerar ju att de synkar



`1286 00:44:56,460 --> 00:44:57,740`
Dessutom för att göra det ännu dummare



`1287 00:44:58,240 --> 00:44:59,780`
De synkar mellan hemmaskin



`1288 00:45:00,040 --> 00:45:01,840`
En hemmamaskin och en



`1289 00:45:02,140 --> 00:45:02,900`
Laptop, en jobb-laptop



`1290 00:45:03,160 --> 00:45:03,920`
Enterprise grade



`1291 00:45:04,180 --> 00:45:05,720`
Så det är ännu dummare



`1292 00:45:05,980 --> 00:45:08,540`
Och för att göra det riktigt coolt då så är det ju dessutom



`1293 00:45:08,800 --> 00:45:09,820`
Cloud keys



`1294 00:45:10,080 --> 00:45:11,360`
Färdiga tokens



`1295 00:45:11,600 --> 00:45:12,880`
Plaintext passwords



`1296 00:45:13,140 --> 00:45:15,960`
Och alla de här är då giltiga



`1297 00:45:16,220 --> 00:45:22,360`
Och även 48 timmar efter CISA blev flaggade och fick reda på det här och de tog bort



`1298 00:45:22,620 --> 00:45:24,160`
Repo, tvingade killen ta bort repot



`1299 00:45:24,400 --> 00:45:26,460`
Så var fortfarande flera av nycklarna till



`1300 00:45:26,720 --> 00:45:30,300`
Nu har vi tagit bort dem så vi vet inte vilka nycklar vi ska notera



`1301 00:45:30,800 --> 00:45:31,580`
Exakt, vilka ska vi notera?



`1302 00:45:31,580 --> 00:45:32,860`
Det är alla klassiska dummare



`1303 00:45:33,120 --> 00:45:33,620`
Lösenord



`1304 00:45:33,880 --> 00:45:34,660`
Sparade i en



`1305 00:45:34,900 --> 00:45:37,460`
Plaintext-fil



`1306 00:45:37,720 --> 00:45:38,740`
En .txt



`1307 00:45:39,000 --> 00:45:42,340`
Det finns ytterligare en CSV-fil med lite lösenord och tokens



`1308 00:45:42,580 --> 00:45:44,900`
Jag har en fråga



`1309 00:45:45,140 --> 00:45:48,480`
Vilken kommer nästa bolag att heta?



`1310 00:45:48,740 --> 00:45:52,060`
Jag tror att företaget kommer nog komma undan tror jag



`1311 00:45:52,320 --> 00:45:55,140`
För att det här är ju en individ



`1312 00:45:55,380 --> 00:45:58,720`
Men hur hans arbetssäkerhet just nu?



`1313 00:45:58,980 --> 00:46:01,540`
Någonting säger mig att om han har ett repo som heter private repos



`1314 00:46:01,840 --> 00:46:07,720`
Han har ju säkert ytterligare ett repo som heter private nsa



`1315 00:46:07,980 --> 00:46:10,280`
Jag tror att jag ska gå in och googla på



`1316 00:46:10,540 --> 00:46:13,360`
Men min favoritfil är ju ändå



`1317 00:46:13,620 --> 00:46:17,960`
Textfilen som heter important aws tokens.txt



`1318 00:46:18,220 --> 00:46:20,520`
What the actual fuck



`1319 00:46:20,780 --> 00:46:22,320`
Då vet man vad man behöver leta efter



`1320 00:46:22,580 --> 00:46:29,220`
Men för att säkra mina nerdcards då så hade jag ju rätt att Nightwing är ju den ursprungliga Robin jag läser nu



`1321 00:46:29,480 --> 00:46:31,020`
Det är alltså RickJad



`1322 00:46:31,020 --> 00:46:33,840`
John Dick Grayson



`1323 00:46:34,100 --> 00:46:39,720`
Som när han tröttnade på att vara Robin så blev han Nightwing



`1324 00:46:39,980 --> 00:46:43,300`
Och blev den lite hårdare varianten av gamla Robin



`1325 00:46:43,560 --> 00:46:45,620`
Trots allt så söper han bort sina repor



`1326 00:46:45,860 --> 00:46:47,140`
Ja precis



`1327 00:46:47,400 --> 00:46:48,680`
Han skrev om en annan typ av säkerhet



`1328 00:46:49,960 --> 00:46:52,020`
Ska vi prata webbhotell?



`1329 00:46:52,260 --> 00:46:53,040`
Det kan vi göra



`1330 00:46:53,300 --> 00:46:54,320`
Habbohotell



`1331 00:46:54,580 --> 00:46:56,880`
Alltså alla



`1332 00:46:57,140 --> 00:46:58,920`
Jag tror att om jag säger



`1333 00:46:59,180 --> 00:47:00,460`
Har du sett interaktionstorien?



`1334 00:47:00,460 --> 00:47:00,980`
Ja



`1335 00:47:01,020 --> 00:47:02,560`
Om jag säger cPanel



`1336 00:47:02,820 --> 00:47:04,860`
Så skulle jag säga att den är typ



`1337 00:47:05,120 --> 00:47:08,700`
Det är alla gamla sunkiga webbhotell



`1338 00:47:08,960 --> 00:47:13,060`
Kör ändå cPanel



`1339 00:47:13,300 --> 00:47:16,120`
Och eftersom det här är en podcast där vi pratar om hur bra det går överallt



`1340 00:47:16,380 --> 00:47:19,700`
Så tänkte jag att vi skulle prata om att cPanel det går inte alls bra



`1341 00:47:20,220 --> 00:47:21,500`
Och



`1342 00:47:21,760 --> 00:47:22,260`
Det som är



`1343 00:47:22,520 --> 00:47:26,620`
Intressant med det här är att det har ju nog funnits länge och varit en front



`1344 00:47:26,880 --> 00:47:30,460`
Scannar man ett webbhotell så hittar man en cPanel inloggning liksom



`1345 00:47:31,280 --> 00:47:34,100`
Och den har ju typ sett likadan ut sedan



`1346 00:47:35,380 --> 00:47:36,140`
Ja



`1347 00:47:36,400 --> 00:47:37,680`
Väldigt sedan internet



`1348 00:47:38,440 --> 00:47:42,020`
Och det som är kul är att man hittat en authentication bypass



`1349 00:47:43,060 --> 00:47:45,100`
Och då håller inne escape och



`1350 00:47:45,360 --> 00:47:47,140`
Ja men man tänker ju såhär



`1351 00:47:47,400 --> 00:47:50,220`
Vad är det viktigaste man har i inputfälten då?



`1352 00:47:50,480 --> 00:47:53,800`
Det är ju det här med alltså vad är det man ska göra då?



`1353 00:47:54,060 --> 00:47:57,640`
Ska man validera input på något sätt eller ska man skita i det eller hur fan funkar det?



`1354 00:47:57,900 --> 00:48:00,460`
Jag har hört att det är onödigt att validera input



`1355 00:48:00,460 --> 00:48:01,480`
Jag tänker det också



`1356 00:48:01,740 --> 00:48:03,020`
Och det här nyckelhålet



`1357 00:48:03,280 --> 00:48:05,320`
Ska det vara någonting som man kan tukla med



`1358 00:48:05,580 --> 00:48:08,140`
Det här med SSL eller TLS eller vad är det det heter nu det här?



`1359 00:48:08,400 --> 00:48:09,680`
Ja just det det här med S-et



`1360 00:48:09,940 --> 00:48:10,700`
Ja det känns konstigt



`1361 00:48:10,960 --> 00:48:13,520`
Men hur som helst så tänker jag att



`1362 00:48:14,280 --> 00:48:17,620`
Det som är bra med den här sårbarheten det är att om man glömmer bort sitt lösenord



`1363 00:48:18,120 --> 00:48:19,400`
Ska man logga in som root ändå



`1364 00:48:19,660 --> 00:48:20,420`
Praktiskt



`1365 00:48:20,680 --> 00:48:21,960`
Och då ska jag berätta hur det går till



`1366 00:48:22,220 --> 00:48:24,020`
Jo det är nämligen så här att



`1367 00:48:24,260 --> 00:48:25,040`
Det är en



`1368 00:48:25,300 --> 00:48:28,100`
CRLF-injektion ska man kunna säga



`1369 00:48:28,360 --> 00:48:28,880`
Det vill säga



`1370 00:48:28,880 --> 00:48:30,420`
Carriage return line feed



`1371 00:48:30,720 --> 00:48:32,500`
Ja det är där själva



`1372 00:48:32,760 --> 00:48:35,320`
Där själva sårbarheten landar egentligen



`1373 00:48:35,840 --> 00:48:40,440`
Men det man kan göra då är att du kan managera dina egna sektioner det är väl där du börjar då



`1374 00:48:40,960 --> 00:48:44,800`
Då får vi då tukla på det som vi då pratar om här



`1375 00:48:45,060 --> 00:48:46,340`
Att slash r



`1376 00:48:46,580 --> 00:48:47,360`
Slash n



`1377 00:48:47,860 --> 00:48:48,900`
Det är det vi behöver



`1378 00:48:49,400 --> 00:48:50,420`
För att



`1379 00:48:50,680 --> 00:48:51,460`
Helt enkelt



`1380 00:48:51,960 --> 00:48:53,500`
Hoppa förbi hela åten



`1381 00:48:54,020 --> 00:48:58,360`
Det som händer då det är att vi egentligen lägger in en egen basic oath header



`1382 00:48:58,620 --> 00:48:59,640`
Som då säger



`1383 00:49:00,460 --> 00:49:01,740`
Ja men det här känns rimligt



`1384 00:49:02,000 --> 00:49:03,280`
Jag tror att



`1385 00:49:03,540 --> 00:49:04,040`
Jag tror att



`1386 00:49:04,300 --> 00:49:06,340`
Åthärden är typ user equals root



`1387 00:49:06,860 --> 00:49:07,880`
Och sen bara new line



`1388 00:49:08,140 --> 00:49:09,420`
Och sen new line och så bara ja



`1389 00:49:09,680 --> 00:49:10,180`
Tackar



`1390 00:49:10,700 --> 00:49:13,260`
Och då är det att det gör man i sin egen sektionsfil liksom



`1391 00:49:13,520 --> 00:49:16,340`
Så du kan ju logga in vad som helst och sen så lägger du bara till det här



`1392 00:49:16,580 --> 00:49:17,860`
För att den läser då



`1393 00:49:18,120 --> 00:49:18,900`
Konfigurationsfilen



`1394 00:49:19,140 --> 00:49:19,920`
Upp från och ner



`1395 00:49:20,180 --> 00:49:20,940`
Så det är så här



`1396 00:49:21,460 --> 00:49:22,980`
Det som slog mig när jag läste det här



`1397 00:49:22,980 --> 00:49:24,260`
Hur i helvete



`1398 00:49:24,520 --> 00:49:25,540`
Explicit language



`1399 00:49:25,800 --> 00:49:27,340`
Har man inte hittat det här tidigare



`1400 00:49:28,360 --> 00:49:30,420`
Jag fattar inte vad man gick igenom



`1401 00:49:30,720 --> 00:49:31,740`
Jag gick in i sin sektionsfil



`1402 00:49:32,000 --> 00:49:33,020`
Berätta mer



`1403 00:49:33,280 --> 00:49:34,560`
Så du går in



`1404 00:49:34,820 --> 00:49:38,140`
När du loggar in då så har du i din cookie har du något som heter



`1405 00:49:38,400 --> 00:49:40,180`
Vhost manager session



`1406 00:49:41,980 --> 00:49:43,260`
Och där kan du då



`1407 00:49:43,520 --> 00:49:44,800`
Där kan du ändra inputen



`1408 00:49:45,060 --> 00:49:48,640`
Så då kan du liksom se till att du får skicka in slash r slash n



`1409 00:49:48,900 --> 00:49:49,660`
Utan att den



`1410 00:49:51,960 --> 00:49:55,040`
Vad säger man encodas eller görs om



`1411 00:49:55,540 --> 00:49:56,820`
Och det är egentligen det det är



`1412 00:49:57,080 --> 00:49:58,620`
Så man steppar egentligen ur



`1413 00:49:58,880 --> 00:49:59,380`
Parseln



`1414 00:49:59,640 --> 00:50:00,420`
Som då validerar detta



`1415 00:50:00,720 --> 00:50:01,740`
Liksom så att den



`1416 00:50:02,500 --> 00:50:04,040`
R minus eller slash r



`1417 00:50:04,300 --> 00:50:05,580`
Det är den slutändan C är



`1418 00:50:06,100 --> 00:50:07,380`
Okej vi kan använda det här



`1419 00:50:07,620 --> 00:50:08,660`
Ja men root okej



`1420 00:50:08,900 --> 00:50:09,420`
Lösnordet



`1421 00:50:09,680 --> 00:50:10,440`
Ja men det är en ny rad



`1422 00:50:10,700 --> 00:50:13,520`
Idag så känns väl inte Cpanel så modernt



`1423 00:50:13,780 --> 00:50:17,620`
Men för typ en tio år sedan så körde väl typ alla hosting-sajter och annat



`1424 00:50:17,860 --> 00:50:19,400`
Jag skulle säga att man ser det



`1425 00:50:19,660 --> 00:50:22,220`
Det tänker jag mig att det fortfarande är rätt vanligt



`1426 00:50:22,740 --> 00:50:24,780`
Jag vill bara att vi inte donar med hosting-sajter så mycket



`1427 00:50:25,040 --> 00:50:25,540`
Nej exakt



`1428 00:50:25,800 --> 00:50:27,340`
Ja



`1429 00:50:27,600 --> 00:50:29,140`
Till exempel de webbottalen jag använder



`1430 00:50:29,380 --> 00:50:30,160`
De har ju det som



`1431 00:50:30,460 --> 00:50:33,020`
Tillvaro fortfarande Cpanel och den här andra



`1432 00:50:33,280 --> 00:50:34,560`
Fan heter den som också är jättestor



`1433 00:50:34,820 --> 00:50:35,840`
Som är PHP baserad



`1434 00:50:36,100 --> 00:50:37,620`
PHP sysadmin



`1435 00:50:37,880 --> 00:50:39,420`
PHP myadmin



`1436 00:50:39,680 --> 00:50:42,500`
Ja men det är väl wordpress är inte det



`1437 00:50:42,740 --> 00:50:45,300`
Nej det är sql



`1438 00:50:45,560 --> 00:50:47,620`
MySQL databas



`1439 00:50:48,120 --> 00:50:51,200`
Men det här tycker jag är väldigt roligt det här är också tror jag i en age of



`1440 00:50:51,460 --> 00:50:52,980`
AI-grej liksom att man



`1441 00:50:53,500 --> 00:50:55,540`
Triviala buggar liksom kommer att



`1442 00:50:55,800 --> 00:50:56,580`
Triviala buggar



`1443 00:50:56,820 --> 00:50:57,860`
Över



`1444 00:50:58,360 --> 00:51:00,420`
Bugklasser som man inte har tänkt på tidigare



`1445 00:51:00,720 --> 00:51:01,480`
Kommer bli lättare att



`1446 00:51:01,740 --> 00:51:02,260`
Titta på



`1447 00:51:02,500 --> 00:51:03,020`
Alltså



`1448 00:51:03,780 --> 00:51:07,880`
Ådigt open source-projekt nu är ju kanon särskilt stora och gamla projekt för att



`1449 00:51:08,660 --> 00:51:09,940`
AI-modellerna blir aldrig trötta



`1450 00:51:10,180 --> 00:51:12,500`
De kommer kunna följa varenda jäkla



`1451 00:51:13,000 --> 00:51:14,800`
User input-kedja



`1452 00:51:15,060 --> 00:51:17,860`
Tills liksom döddagar och varenda permutation av dem



`1453 00:51:18,120 --> 00:51:20,180`
Någon kommer ju behöva gå igenom dem och få ut



`1454 00:51:20,680 --> 00:51:22,220`
För det är ju något



`1455 00:51:22,480 --> 00:51:24,020`
Carl



`1456 00:51:25,300 --> 00:51:29,900`
Bröt ihop över dåliga AI-slopprapporter för ett tag sedan och



`1457 00:51:29,900 --> 00:51:31,440`
Plockade bort sig själv från den här kanalen va?



`1458 00:51:31,700 --> 00:51:35,280`
Och Linux och Linus Tordvall och sådana har ju börjat



`1459 00:51:35,540 --> 00:51:37,060`
Bryta ihop över att



`1460 00:51:37,580 --> 00:51:43,220`
Även när det kommer in några bra AI-rapporter där man har hittat bra grejer med AI



`1461 00:51:43,720 --> 00:51:46,020`
Så är det ju väldigt mycket skräp som kommer nu



`1462 00:51:46,280 --> 00:51:47,820`
Jag hade inte velat sitta och jobba med triagering på



`1463 00:51:48,080 --> 00:51:49,620`
Nej inte jag heller, jag tror att



`1464 00:51:49,860 --> 00:51:51,660`
Bug bounty-industrin kommer ju



`1465 00:51:51,920 --> 00:51:54,980`
Jag har kompisar som jobbar med det här och de säger ju det redan nu att



`1466 00:51:55,500 --> 00:51:58,060`
Google och väldigt många stora privata program har ju



`1467 00:51:58,320 --> 00:51:59,860`
Plockat bort payouts för



`1468 00:52:00,160 --> 00:52:02,720`
Låg och medium-grejer, de är borta liksom



`1469 00:52:02,980 --> 00:52:07,580`
Bara för att triagerna hinner inte med att följa upp all skit och det är ju såhär



`1470 00:52:07,840 --> 00:52:11,420`
Det var ju skit förut också men det var snabbare att upptäcka att det var skit



`1471 00:52:11,940 --> 00:52:13,720`
Nu är ju AI ganska bra på att skriva



`1472 00:52:13,980 --> 00:52:15,000`
Du får mer



`1473 00:52:15,260 --> 00:52:18,080`
Rapporter och mer välskrivna rapporter nu



`1474 00:52:18,340 --> 00:52:23,700`
Ja det är väl de som triagen då måste ta på allvar för att validera vidare, det är en fast positive



`1475 00:52:23,960 --> 00:52:27,040`
Tidigare ifall du fick en välskriven rapport så var den förmodligen legit



`1476 00:52:27,540 --> 00:52:29,860`
Exakt och nu får du en välskriven rapport om



`1477 00:52:30,160 --> 00:52:31,180`
Missing



`1478 00:52:31,440 --> 00:52:34,260`
SPF records på 400 sidor som verkar skitmäktig



`1479 00:52:34,500 --> 00:52:35,540`
Men det är bara skit



`1480 00:52:36,040 --> 00:52:38,100`
Eller missing cores eller något annat roligt



`1481 00:52:38,600 --> 00:52:39,620`
Men



`1482 00:52:39,880 --> 00:52:44,500`
Om vi nu även pratar om Curl, Curl fick ju påhälsning av Mythos



`1483 00:52:45,000 --> 00:52:46,800`
Går att läsa på Hax.



`1484 00:52:47,820 --> 00:52:51,400`
Vad är det för domän? Hax.m eller Hax.s?



`1485 00:52:51,660 --> 00:52:52,940`
Ja men Curl iallafall



`1486 00:52:53,200 --> 00:52:53,700`
Eller är det Hax.s?



`1487 00:52:53,960 --> 00:52:55,760`
Ja fan det här borde vi veta



`1488 00:52:56,020 --> 00:52:59,340`
Curls blogg eller Daniels blogg



`1489 00:52:59,900 --> 00:53:01,940`
Så gå in och läs det här för det är ganska intressant



`1490 00:53:02,200 --> 00:53:06,300`
Just för att det har varit väldigt mycket media nu om såhär Mythos kommit över världen



`1491 00:53:06,560 --> 00:53:07,580`
Bra PR-hype



`1492 00:53:07,840 --> 00:53:13,220`
Väldigt bra PR-hype och vi har Glasswing och du vet vi kommer inte släppa det i publik för det är så jävla incredibly nice



`1493 00:53:13,460 --> 00:53:16,800`
Men dom släppte loss Mythos på det och hittade en lowbug



`1494 00:53:17,060 --> 00:53:17,820`
En lowbug



`1495 00:53:19,100 --> 00:53:21,660`
Vilket är intressant att man hittar för det är



`1496 00:53:21,920 --> 00:53:26,520`
Curlprojektet har ju inte själv fått köra och det är väldigt oklart hur mycket



`1497 00:53:26,780 --> 00:53:28,820`
Mänsklig handpåläggning som varit där



`1498 00:53:28,820 --> 00:53:34,200`
Det du säger nu är ju helt korrekt vi vet ju inte mer än så egentligen



`1499 00:53:34,460 --> 00:53:36,500`
Så vi kan ju inte validera hur vidare den här har gjort



`1500 00:53:36,760 --> 00:53:40,860`
Någon har kört en Mythos-rapport för Curl



`1501 00:53:42,140 --> 00:53:45,460`
Ingen kunskap om hur mycket arbete som lagts ner



`1502 00:53:46,220 --> 00:53:48,020`
Och det kom ut något som inte var skräp från den



`1503 00:53:48,280 --> 00:53:49,040`
Exakt



`1504 00:53:49,560 --> 00:53:50,840`
Men också inte någonting som



`1505 00:53:51,340 --> 00:53:53,400`
Sprängde Curl i små bitar



`1506 00:53:53,660 --> 00:53:56,220`
Och det var en enda find



`1507 00:53:56,460 --> 00:53:57,240`
Så jag tror att



`1508 00:53:57,500 --> 00:53:58,520`
Jag jobbar ju med det



`1509 00:53:58,820 --> 00:54:01,380`
Jättemycket, jag har ändrat hela mitt arbetssätt med det här



`1510 00:54:02,660 --> 00:54:05,220`
Sedan ett och ett halvt, två år sedan tillbaka liksom



`1511 00:54:05,480 --> 00:54:08,040`
Och jag är jättemycket mer produktiv



`1512 00:54:08,300 --> 00:54:10,860`
Skulle jag säga på saker och ting som jag tycker är tråkigt i mitt jobb



`1513 00:54:11,360 --> 00:54:12,900`
Men



`1514 00:54:13,660 --> 00:54:15,200`
Gör jag inte mitt jobb längre?



`1515 00:54:15,460 --> 00:54:15,980`
Nej



`1516 00:54:16,220 --> 00:54:19,040`
Jag gör mitt jobb kanske till och med mer än vad jag gjorde tidigare



`1517 00:54:19,300 --> 00:54:20,840`
För man måste validera



`1518 00:54:21,100 --> 00:54:24,420`
Output och input och A1 blir aldrig bra om du inte kan



`1519 00:54:24,940 --> 00:54:27,500`
Styra det rätt eller bygga scaffolding som gör att den



`1520 00:54:27,740 --> 00:54:28,780`
Gör korrekta beslut



`1521 00:54:29,080 --> 00:54:31,640`
Det är liksom inte så att världen kommer



`1522 00:54:31,900 --> 00:54:33,420`
Bara sluta fungera nu



`1523 00:54:33,680 --> 00:54:40,340`
Däremot så har vi en verktygslåda som är större och vi har möjlighet att matisera och göra saker och ting som vi inte kanske orkade förut



`1524 00:54:40,600 --> 00:54:42,640`
Jag gjorde ett pentest för ett



`1525 00:54:42,900 --> 00:54:44,180`
Längre tag sedan där



`1526 00:54:45,200 --> 00:54:50,840`
Jag har ritat en tossighet i hur man hanterar tokens som var



`1527 00:54:51,340 --> 00:54:56,460`
Så jag hade ett startskott och jag hade börjat hata på funktionaliteten och sen så



`1528 00:54:57,240 --> 00:54:58,780`
Kom min kära



`1529 00:54:59,080 --> 00:55:04,200`
Vd Jonas Magasinius förbi och tittade på den här rapporten på att skriva



`1530 00:55:04,700 --> 00:55:06,760`
Efter en tag så frågade han då liksom



`1531 00:55:07,260 --> 00:55:10,080`
Men det är så när jag jämför mig på höger sidan, var kommer det ifrån?



`1532 00:55:10,860 --> 00:55:17,760`
Och då började det bli såhär, okej men jag är så stressad, oh shit fan det här är ju mycket trasigare än vad jag trodde innan



`1533 00:55:19,560 --> 00:55:20,320`
Och



`1534 00:55:20,580 --> 00:55:22,120`
Just sådana här



`1535 00:55:23,400 --> 00:55:23,900`
Alltså att



`1536 00:55:24,160 --> 00:55:25,180`
Titta på mycket



`1537 00:55:25,440 --> 00:55:28,520`
Där det är lätt att som människa att bara missa



`1538 00:55:28,820 --> 00:55:30,360`
Och tracea grejerna



`1539 00:55:30,620 --> 00:55:33,180`
Där har vi ju verkligen potential för att de här modellerna



`1540 00:55:33,420 --> 00:55:34,200`
Potentiellt kan göra



`1541 00:55:34,700 --> 00:55:35,740`
Ett bättre jobb liksom



`1542 00:55:36,240 --> 00:55:38,540`
Så patterns och sådant så att du har en



`1543 00:55:38,800 --> 00:55:40,600`
Jag vet att vi pratade om



`1544 00:55:40,860 --> 00:55:43,420`
Code Q eller sådant här innan där man kan då



`1545 00:55:43,660 --> 00:55:49,560`
Domänmässigt med regler förklara vad en cross-site scripting är till exempel och då få väldigt bra



`1546 00:55:50,840 --> 00:55:53,660`
Precision när man letar efter XSS i källkod och så vidare



`1547 00:55:54,160 --> 00:55:56,460`
Det blir ju tagit en helt ny nivå nu, jag vill ju såhär



`1548 00:55:56,720 --> 00:55:58,000`
Titta på en kodbas som är



`1549 00:55:58,260 --> 00:55:58,780`
Särskilt open source



`1550 00:55:59,080 --> 00:56:00,100`
Som är svinlång



`1551 00:56:00,620 --> 00:56:02,140`
Du har access till repo



`1552 00:56:02,400 --> 00:56:03,680`
Du har repohistorik



`1553 00:56:04,460 --> 00:56:07,020`
Den statiska kodanalysen du kan göra för ett sådant projekt



`1554 00:56:07,780 --> 00:56:09,580`
Med en LLM idag



`1555 00:56:09,820 --> 00:56:11,100`
Visserligen kanske då



`1556 00:56:11,360 --> 00:56:14,700`
En kanske lite kostsam LLM alltså som



`1557 00:56:14,940 --> 00:56:19,560`
Kod max 20 eller vad fan det nu kan tänkas vara så du har lite tråkigt att spendera



`1558 00:56:19,820 --> 00:56:26,720`
Den är ju ganska bra även med OPS 4.7 liksom du behöver inte mytos så länge du vet vad det är du letar efter eller vilka anti-patrons du är taggad på liksom



`1559 00:56:26,980 --> 00:56:28,260`
Den kanske också kan ta fram



`1560 00:56:28,260 --> 00:56:31,840`
Kod QL-regler för det så de kanske kan korsföda varandra liksom



`1561 00:56:32,620 --> 00:56:33,120`
Ja



`1562 00:56:33,640 --> 00:56:34,400`
Nej det är det så att



`1563 00:56:34,660 --> 00:56:35,940`
Ja automationsmässigt



`1564 00:56:36,200 --> 00:56:38,500`
För någon som är bra på



`1565 00:56:38,760 --> 00:56:41,320`
Säkerhetsgranska så ska jag säga att det är en jävligt bra



`1566 00:56:41,580 --> 00:56:45,420`
Komplement till verktygslaget men det är liksom inte ondbråd internetdörr det löser vi så bra själva



`1567 00:56:49,000 --> 00:56:52,320`
Vi hoppade förbi de här Linux ordbarheterna



`1568 00:56:53,340 --> 00:56:55,400`
Vi pratar ju i det avsnittet



`1569 00:56:55,660 --> 00:56:57,960`
Som vi kommer släppa sen så pratar vi



`1570 00:56:58,260 --> 00:57:01,080`
Om copy-fail som kom med som en grej där



`1571 00:57:01,580 --> 00:57:03,380`
Där man väsentligen hittat ett nytt



`1572 00:57:04,660 --> 00:57:09,780`
Ett nytt typ av write-primitiv via en ny typ av bug-klass i



`1573 00:57:10,040 --> 00:57:11,060`
Linux-körnen



`1574 00:57:11,580 --> 00:57:14,640`
Där man kan göra kontrollerade skrivningar till



`1575 00:57:15,660 --> 00:57:18,480`
Specifik del i minnet och framförallt man kan



`1576 00:57:18,740 --> 00:57:21,820`
Mappa över vissa filer och sånt och



`1577 00:57:22,320 --> 00:57:24,120`
Skriva över minnesbilden om dem



`1578 00:57:24,880 --> 00:57:27,440`
Den första heter copy-fail



`1579 00:57:28,260 --> 00:57:30,560`
Sen så släppte



`1580 00:57:30,820 --> 00:57:34,140`
Släppte sig på Linux-körnermailinglistan



`1581 00:57:34,400 --> 00:57:37,980`
Så släpptes det en ny bug-patch och då såg någon direkt att



`1582 00:57:39,020 --> 00:57:39,780`
Vänta lite nu



`1583 00:57:41,320 --> 00:57:44,140`
Det här väcker mitt minne av copy-fail



`1584 00:57:44,640 --> 00:57:45,420`
Så någon



`1585 00:57:45,660 --> 00:57:47,460`
Direkt skrev ett exploit



`1586 00:57:47,980 --> 00:57:50,780`
Mot en copy-fail liknande sårbarhet



`1587 00:57:51,040 --> 00:57:52,840`
Det är väl den, är det Dirty Frag eller vad är det vi kallar den nu?



`1588 00:57:53,100 --> 00:57:55,140`
Dirty Frag finns, Dirty Pipe finns



`1589 00:57:55,660 --> 00:57:57,440`
Dirty Frag är det nu va?



`1590 00:57:57,440 --> 00:58:01,280`
Dirty Pipe är väl en gammal, Dirty Pipe är gammal och Dirty Frag är



`1591 00:58:01,540 --> 00:58:02,820`
Ja, det är nog Dirty Frag



`1592 00:58:03,080 --> 00:58:07,160`
Men grejen var ju att tydligen så är ju Linux-körningar



`1593 00:58:08,200 --> 00:58:11,260`
Alltså ofta så går alltså patchen ut på



`1594 00:58:11,520 --> 00:58:13,060`
Linux-mailinglistan



`1595 00:58:13,820 --> 00:58:16,640`
Innan alla maintainers patchar



`1596 00:58:17,160 --> 00:58:19,960`
Men det tog ju



`1597 00:58:20,220 --> 00:58:21,000`
Tydligen



`1598 00:58:21,240 --> 00:58:21,760`
Alltså



`1599 00:58:22,020 --> 00:58:27,140`
Jag tittade på C-koden här i det reverse-engineerade



`1600 00:58:27,440 --> 00:58:28,460`
Exploitet



`1601 00:58:28,980 --> 00:58:31,020`
Jag kan ju säga att jag har inte smackat upp det där snabbt



`1602 00:58:31,280 --> 00:58:34,860`
Men det finns ju folk som skrapar det mig på hur man skriver exploit-kod



`1603 00:58:35,380 --> 00:58:38,700`
Så det räckte ju med att det dök upp på mailing-listan en bug-fix



`1604 00:58:38,960 --> 00:58:41,520`
Och direkt så hade någon



`1605 00:58:41,780 --> 00:58:44,340`
Spottat ut sig ett oberoende exploit



`1606 00:58:44,840 --> 00:58:46,900`
Och därför så tryckte man ut



`1607 00:58:47,160 --> 00:58:50,220`
All information om sårbarheten



`1608 00:58:51,000 --> 00:58:51,500`
Brätt



`1609 00:58:51,760 --> 00:58:53,560`
Snabbt i mördningsläge



`1610 00:58:53,800 --> 00:58:57,400`
Det finns flertalet pockar nu som bara går och drar ner



`1611 00:58:57,700 --> 00:58:59,740`
Och det är ju dirtyfrag helt korrekt



`1612 00:59:00,000 --> 00:59:00,520`
LP liksom



`1613 00:59:00,760 --> 00:59:07,160`
Och det har ju varit ett klassiskt problem att sådana här CERT-processer och säkerhetsrättningsprocesser



`1614 00:59:08,200 --> 00:59:11,000`
Har du lämnat över någonting till bug-fixningslistan



`1615 00:59:11,520 --> 00:59:13,820`
Så är risken att det antingen



`1616 00:59:14,340 --> 00:59:16,120`
Läcker publikt eller att



`1617 00:59:16,640 --> 00:59:17,920`
Eller att



`1618 00:59:18,940 --> 00:59:22,520`
Specifikt vissa hotaktörer får tillgång till det liksom för att



`1619 00:59:23,300 --> 00:59:27,400`
Men det blir ju en fråga då liksom



`1620 00:59:27,700 --> 00:59:28,200`
Hur



`1621 00:59:28,720 --> 00:59:31,020`
Hur man ska jobba med Linux fixar om det



`1622 00:59:31,280 --> 00:59:34,360`
Om det kommer vara så överlag att det är samma stund som



`1623 00:59:35,120 --> 00:59:38,700`
Som patchen finns på Linux sårbarheten så finns exploitet



`1624 00:59:39,220 --> 00:59:42,040`
Vi var väl, var vi inte här med



`1625 00:59:44,080 --> 00:59:48,680`
Var vi inte något liknande med någon av Java sårbarheterna var det



`1626 00:59:51,240 --> 00:59:56,880`
Någon som var stor någon av de här JNLP grejerna eller nej var det det?



`1627 00:59:57,440 --> 00:59:59,740`
Någon som var mindre sårbarheten eller någonting där



`1628 01:00:00,260 --> 01:00:04,860`
Där det kom exploits mer eller mindre från samma stund som



`1629 01:00:04,860 --> 01:00:05,640`
Ja men det stämmer ju



`1630 01:00:05,880 --> 01:00:14,080`
Så folk är bra på att hålla koll på om det händer någonting i repos eller mailing listor



`1631 01:00:14,340 --> 01:00:14,840`
Och ta fram



`1632 01:00:15,620 --> 01:00:22,780`
Ta fram exploiten så det är svårt att jobba med säkerhet och open source och förhindra att



`1633 01:00:23,040 --> 01:00:26,880`
De här enda exploiten kommer innan fixen finns tillgänglig för folk



`1634 01:00:26,880 --> 01:00:27,400`
Mm



`1635 01:00:27,440 --> 01:00:29,740`
Jag tänker också särskilt nu då i



`1636 01:00:30,760 --> 01:00:33,080`
Stora språkmodeller och kontext



`1637 01:00:33,320 --> 01:00:34,860`
Alltså kontext för



`1638 01:00:35,120 --> 01:00:36,400`
Coding och sånt är ju ganska enkelt



`1639 01:00:38,200 --> 01:00:40,760`
Med AI kan jag verkligen tänka mig liksom



`1640 01:00:42,540 --> 01:00:43,060`
Det här



`1641 01:00:43,560 --> 01:00:45,880`
Tycker vi ser ut ungefär som den sårbarheten



`1642 01:00:46,640 --> 01:00:48,180`
Hjälp mig ta fram ett exploit för det



`1643 01:00:48,440 --> 01:00:49,200`
Det kan vi tänka oss



`1644 01:00:49,720 --> 01:00:52,520`
Det finns ju en massa repo med scaffolding där man



`1645 01:00:52,780 --> 01:00:56,880`
Där man faktiskt gör precis det du säger nu man tittar på pattern med exploitering



`1646 01:00:57,440 --> 01:01:03,080`
Till och med att det byter plattform så att det



`1647 01:01:03,320 --> 01:01:06,660`
Det var en Linux binär vs en Windows binär



`1648 01:01:06,920 --> 01:01:10,760`
Men de beter sig på samma sätt då jag är ju ingen Windows kille längre men



`1649 01:01:11,000 --> 01:01:13,060`
Där kunde de använda



`1650 01:01:13,320 --> 01:01:14,340`
Kontextet av



`1651 01:01:14,600 --> 01:01:16,900`
Linux sårbarheten för att hacka Windows binären



`1652 01:01:17,400 --> 01:01:18,940`
Vilket är ganska coolt då för pattern just



`1653 01:01:19,460 --> 01:01:21,000`
Vilket också är rimligt för att det är samma kod



`1654 01:01:21,240 --> 01:01:23,300`
Men med de orden så kanske det är dags



`1655 01:01:23,800 --> 01:01:24,320`
Två saker



`1656 01:01:24,580 --> 01:01:27,140`
Apropå hur snabbt det går med exploits och sånt



`1657 01:01:27,440 --> 01:01:29,480`
Jag kan rekommendera en sajt som heter zero day clock



`1658 01:01:30,000 --> 01:01:32,040`
Som visar trender historiskt



`1659 01:01:32,300 --> 01:01:34,860`
Och den visar rätt tydligt att i år hittills



`1660 01:01:35,120 --> 01:01:36,400`
Så är



`1661 01:01:36,660 --> 01:01:38,960`
Medianen för hur lång tid det tar



`1662 01:01:39,220 --> 01:01:41,520`
Att gå från cv till exploit



`1663 01:01:41,780 --> 01:01:42,540`
Noll minuter



`1664 01:01:43,560 --> 01:01:45,880`
Medel dock är



`1665 01:01:46,120 --> 01:01:47,160`
1,9 dagar



`1666 01:01:47,660 --> 01:01:49,960`
Men det är ändå en väsentlig ändring från förra året



`1667 01:01:50,220 --> 01:01:52,780`
Då medel var 21 dagar



`1668 01:01:53,040 --> 01:01:55,860`
Och det här är det följande trenden



`1669 01:01:56,120 --> 01:01:57,400`
År 2004 var det 53



`1670 01:01:57,700 --> 01:01:58,460`
Dagar så att



`1671 01:01:58,720 --> 01:02:03,320`
Skulle det komma så att det är så många som räknas som negativa dagar?



`1672 01:02:03,580 --> 01:02:06,920`
Att min är



`1673 01:02:07,680 --> 01:02:08,960`
Så mycket mer än



`1674 01:02:09,220 --> 01:02:12,800`
Medianen är ju förmodligen att det finns ett par outliers där det har tagit jävligt lång tid



`1675 01:02:15,360 --> 01:02:16,380`
Men iallafall det går fort



`1676 01:02:16,640 --> 01:02:17,160`
Så kan vi säga



`1677 01:02:17,400 --> 01:02:19,200`
De allra flesta exploits



`1678 01:02:19,460 --> 01:02:20,740`
Finns redan



`1679 01:02:21,000 --> 01:02:22,020`
När



`1680 01:02:22,280 --> 01:02:23,040`
Cvm blir känd



`1681 01:02:24,060 --> 01:02:26,120`
Och det ställer ju extremt tryck på



`1682 01:02:27,700 --> 01:02:28,460`
Utvecklarna idag



`1683 01:02:28,720 --> 01:02:29,480`
Du måste ju patcha superfort



`1684 01:02:30,260 --> 01:02:34,100`
I min bok så är det liksom har du inte automation på plats för att patcha så kommer du alltid ligga efter



`1685 01:02:34,360 --> 01:02:37,160`
Vi kommer ju komma tillbaka till den här frågan



`1686 01:02:37,420 --> 01:02:40,500`
För mig det var med stand-up eller något liknande där de



`1687 01:02:41,260 --> 01:02:43,820`
Där de började diskussionen om



`1688 01:02:44,340 --> 01:02:47,160`
Vad är en CRO-day och vad är en N-day



`1689 01:02:47,400 --> 01:02:48,180`
Just det här



`1690 01:02:49,720 --> 01:02:52,280`
För en gång i tiden så tyckte ju folk att det var



`1691 01:02:52,520 --> 01:02:53,040`
Eller så här



`1692 01:02:54,060 --> 01:02:57,400`
Det finns säkert många olika positioner men de två stora positionerna



`1693 01:02:57,700 --> 01:03:00,520`
Den ena positionen är ju



`1694 01:03:00,760 --> 01:03:03,580`
Från den dagen någon vet om sårbarheten



`1695 01:03:04,360 --> 01:03:05,640`
Från den dagen



`1696 01:03:06,660 --> 01:03:09,480`
Software-vendor vet om sårbarheten



`1697 01:03:09,720 --> 01:03:11,000`
Eller från den dagen



`1698 01:03:11,260 --> 01:03:12,800`
Användarna kan patcha



`1699 01:03:13,060 --> 01:03:17,660`
Så att vi kan lätt identifiera att det finns minst tre olika tolkningar om vad en CRO-day är



`1700 01:03:18,680 --> 01:03:20,740`
Min andra punkt innan vi avslutar



`1701 01:03:21,000 --> 01:03:23,300`
Är att



`1702 01:03:23,560 --> 01:03:25,600`
Det är helt korrekt att



`1703 01:03:25,860 --> 01:03:27,400`
Ovasps nästa event



`1704 01:03:27,700 --> 01:03:28,980`
Är dagen före



`1705 01:03:29,240 --> 01:03:30,000`
Securityfest



`1706 01:03:30,260 --> 01:03:30,760`
Inte



`1707 01:03:31,020 --> 01:03:32,820`
När ni hör detta då i förra veckan



`1708 01:03:33,080 --> 01:03:35,380`
Det är alltså inte redan vart utan det kommer vara på onsdag



`1709 01:03:35,640 --> 01:03:36,660`
Det verkar också vara rimligt



`1710 01:03:38,200 --> 01:03:39,980`
Klockan 17.30 tror jag



`1711 01:03:40,240 --> 01:03:43,560`
Och det finns plats kvar så är det bara att anmäla sig på Ovasp Meetup



`1712 01:03:45,100 --> 01:03:45,620`
Då så



`1713 01:03:46,120 --> 01:03:49,960`
Får vi ta och tacka för oss den här gången och vi hoppas att ses då om



`1714 01:03:50,220 --> 01:03:50,740`
Tre dagar



`1715 01:03:51,000 --> 01:03:54,840`
Jag som pratade till Johan Ribbenmöller med mig hade jag Jesper Larsson



`1716 01:03:55,340 --> 01:03:56,120`
Mattias Vidager



`1717 01:03:56,360 --> 01:03:56,880`
Japp japp



`1718 01:03:57,440 --> 01:03:59,480`
Smutsen i din page table



`1719 01:03:59,740 --> 01:04:00,520`
Har du gett det här?



`1720 01:04:02,300 --> 01:04:04,600`
Fan det finns ju ingen smuts i din page table



`1721 01:04:05,380 --> 01:04:05,880`
Copy fail



`1722 01:04:06,400 --> 01:04:07,160`
Copy fail



`1723 01:04:07,940 --> 01:04:09,480`
Alltså du vann med allt


