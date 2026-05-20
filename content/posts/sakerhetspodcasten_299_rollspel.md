---
date: '2026-03-16T09:55:00'
tags:
- tema
title: 'Säkerhetspodcasten #299 - Rollspel'
---
Game Master Jesper leder podden in i ett rollspel / äventyr (AI genererat)
  äventyr om en krypto-myntstöld.
Podden försöker utifrån gamla citat med mera gissa sig fram till vad som kan
   ha hänt, hur man skulle skydda sig, med mera.

## Lyssna
* [mp3](https://traffic.libsyn.com/secure/sakerhetspodcasten/2026-02-18_Roleplay.mp3?dest-id=117848), längd: 01:00:58

## Plugs

* **Informell afterwork**, *spelat in 300 avsnitt firande*:
  24 Mars 2026 18:00,
  på Bishops Arms Park Avenue (på Avenyn).
  _Finns inga reservationer eller dylikt, vi är bara där och tar någon öl, kika efter oss._
* [Foss-North](https://foss-north.se/),
  27-28 april 2026, Chalmers.

## Feedback: Bybit hacket

Johan Lindberg, Säkerhet, Ethereum Foundation
  hörde av sig i April med lite förtydlingar,
  efter att lyssnat på avsnittet:

### Den enkla formuleringen till podden, jämför med BankID

> Föreställ er att BankID visade “Godkänn transaktion: 3a7f9c…d82b” istället för
> “Betala 149 kr till Spotify”. Ni skulle trycka godkänn ändå, för ni litar på bankens
> webbsida som säger att det är lugnt? Det är precis det Bybits signatärer gjorde –
> och det är varför det inte spelade någon roll att de var tre stycken. Alla tre
> granskade webbsidans lögn, inte sanningen i hårdvaruplånboken.

### En övergipande förklaring av osäkra blind signering flödet

> De som skulle signera satt vid sina datorer och öppnade Safe{Wallet}s webbgränssnitt i
> sin webbläsare.  Webbläsaren hämtade JavaScript från app.safe.global och renderade en
> sida som visade: “Flytta X ETH från “cold wallet adress” till “hot wallet adress” – allt såg legitimt ut.
>
> Sedan kopplade de in sin Ledger hårdvaruplånbok. Webbsidan skickade då ett EIP–712-
> meddelande till Ledgern för signering. Och här är det kritiska problemet: Ledgern kan
> inte avkoda och visa EIP–712-meddelandets faktiska innehåll i läsbar form när det
> innehåller nestade operationer som delegatecall.
>
> Vad Ledgern visade på sin lilla skärm var i praktiken ett kryptografiskt hash
> – en lång teckensträng –
> inte transaktionens faktiska innebörd.
>
> Alla tre tryckte godkänn på Ledgern baserat på vad webbsidan visade, inte vad
> Ledgern visade. Det är blind signing.

> Hade de faktiskt granskat vad Ledgern visade hade de sett att hashen inte stämde med
> en normal överföring. De hade troligtvis inte kunnat läsa sig till exakt vad som skulle
> ske – men de hade sett att något var fel.

### Läsbar signering, transparent signering (Clear signing) flöden

> Det finns något som kallas clear signing som alla hårdvaruplånböcker försöker
> implementera på ett eller annat sätt – principen att det du ser på enhetens skärm
> bokstavligen är det du signerar, utan att behöva lita på webbsidan däremellan.

### Vad är en hårdvaruplånbok – och varför spelar det roll?

> En hårdvaruplånbok är en fysisk enhet – ungefär som ett USB-minne – vars
> enda uppgift är att skydda din privata nyckel. Den privata nyckeln
> är det som bevisar äganderätt till kryptotillgångar: den som kontrollerar
> nyckeln kontrollerar pengarna, oavsett vad som står någon annanstans.
> Nyckeln lämnar aldrig hårdvaruplånboken, vilket innebär att en angripare
> som tar sig in på din dator eller i din e-post ändå inte kan komma åt den.
> De vanligaste enheterna är Trezor och Ledger – båda väletablerade, men med
> olika designfilosofier kring öppenhet och säkerhet.

### Multisig – när en nyckel inte räcker

> För tillgångar av högre värde används ofta multisignatur (multisig),
> vilket innebär att en transaktion kräver godkännande från flera nycklar.
> Upplägget beskrivs som M-av-N – t.ex.:
>
> * 3-av-5: Fem nycklar existerar, varav tre måste signera.
>   Ger redundans (du kan tappa två nycklar utan att förlora åtkomst)
>   och skydd mot kompromiss (en angripare som tar sig in på en enhet
>   kan inte agera ensam).
> * 7-av-10: Används för mycket höga värden eller organisationer med fler
>   intressenter. Kräver bred konsensus, vilket gör obehörig åtkomst ännu svårare
>    – men ställer också högre krav på koordination


## AI transkribering

_AI försöker förstå oss... Ha överseende med galna feltranskriberingar._

`1 00:00:00,000 --> 00:00:02,200`
Hej och välkommen till Säkerhetsbordgasen.



`2 00:00:02,280 --> 00:00:05,200`
Jag som pratar heter Johan Ryberg Möller, men man har ju av Mattias Hidhage,



`3 00:00:05,400 --> 00:00:08,500`
Jesper Larsson och Peter Magnusson.



`4 00:00:08,560 --> 00:00:10,400`
Vi har en skill.md nära dig.



`5 00:00:10,820 --> 00:00:14,060`
Rick är tyvärr inte med oss, han återkommer förhoppningsvis i maj ungefär.



`6 00:00:14,440 --> 00:00:16,780`
Ja, april-maj. Då är han tillbaka.



`7 00:00:17,140 --> 00:00:20,480`
Vi ska nämna att det är den 18 februari när vi spelar in detta,



`8 00:00:20,600 --> 00:00:24,660`
nådans år 2026, och vi är sponsrade av Ashore som finns på ashore.se



`9 00:00:24,660 --> 00:00:30,180`
så även av Nollix4a som finns på nollix4a.se och av Bortfors som finns på bortfors.se.



`10 00:00:30,620 --> 00:00:31,100`
Snyggt\!



`11 00:00:31,960 --> 00:00:34,760`
Precis innan vi drar igång här så ska vi nämna några snabba plugs.



`12 00:00:35,960 --> 00:00:39,980`
Förra gången vi körde så pratade vi om Fast North, men då var det det CFP vi pluggade för.



`13 00:00:40,560 --> 00:00:44,800`
Så nu tänkte vi att vi skulle plugga även för själva eventet som går av staten



`14 00:00:44,800 --> 00:00:52,780`
27-28 april på Chalmers, det är alltså en open source-konferens.



`15 00:00:52,780 --> 00:00:54,640`
Läs mer om det på post.se.



`16 00:00:54,660 --> 00:00:59,660`
Så känner ni att ni är fast på den hemska östkusten så kan ni komma till bästkusten



`17 00:01:00,260 --> 00:01:02,340`
och uppleva fri mjukvara.



`18 00:01:02,480 --> 00:01:04,240`
Exakt, om man inte vill ha bräckt vatten längre.



`19 00:01:04,480 --> 00:01:05,240`
Och saltsten.



`20 00:01:08,860 --> 00:01:13,280`
Men utöver det så har vi ju en circuitfest coming up, slutet på maj som vanligt.



`21 00:01:13,480 --> 00:01:16,640`
Exakt, och biljetterna nu, hot of the press.



`22 00:01:16,920 --> 00:01:17,800`
Första släppet har varit.



`23 00:01:18,040 --> 00:01:19,460`
De tog slut jättetort.



`24 00:01:19,960 --> 00:01:24,640`
Och nästa släpp har vi nu från en väldigt säker källa fått förklarat för oss.



`25 00:01:24,660 --> 00:01:26,660`
Det är ungefär om tre veckor.



`26 00:01:26,980 --> 00:01:30,380`
Så när detta kommer ut, kanske om en vecka då?



`27 00:01:30,380 --> 00:01:31,380`
Ja, exakt.



`28 00:01:31,380 --> 00:01:32,480`
Eller något sånt.



`29 00:01:32,480 --> 00:01:36,580`
Men ni kan ju gå in och kika lite extra på detta på circuitfest.com



`30 00:01:36,580 --> 00:01:39,340`
eller skriva upp för er på nyhetsutvecklingen där så går det ni på in.



`31 00:01:39,340 --> 00:01:40,660`
Ja, stay vigilant.



`32 00:01:40,660 --> 00:01:42,660`
Så är det.



`33 00:01:42,660 --> 00:01:47,540`
Nej, men det är faktiskt så roligt att vi har kommit upp i vårt 300-e avsnitt.



`34 00:01:47,540 --> 00:01:49,540`
Ser ut så gott.



`35 00:01:49,540 --> 00:01:51,540`
Lite beroende på hur man räknar så kan det vara mer eller mindre.



`36 00:01:51,540 --> 00:01:54,580`
Men vi har bestämt oss för att det är ett 300-e avsnitt som ska träffas in.



`37 00:01:54,580 --> 00:01:56,580`
Den 24 mars.



`38 00:01:56,580 --> 00:01:57,580`
Exakt.



`39 00:01:57,580 --> 00:02:01,080`
Och det tänkte vi att vi skulle fira med de lyssnare som vill och kan.



`40 00:02:01,080 --> 00:02:02,080`
Exakt.



`41 00:02:02,080 --> 00:02:05,580`
Så vi kommer se oss spela in ett avsnitt där vi pratar lite gamla goa minnen.



`42 00:02:05,580 --> 00:02:09,080`
Och sen så kommer vi gå och träffa de som vill för att ta en öl.



`43 00:02:09,080 --> 00:02:12,580`
Så höj volymen. Vart träffas vi?



`44 00:02:12,580 --> 00:02:15,580`
Vi träffas på Bishops Arms på Avenyn.



`45 00:02:15,580 --> 00:02:18,580`
Park Avenue tror jag lokalen heter.



`46 00:02:18,580 --> 00:02:21,580`
Det ligger alltså i samma hus som Circuitfest brukar vara.



`47 00:02:21,580 --> 00:02:22,580`
I källaren.



`48 00:02:22,580 --> 00:02:24,580`
Men högt upp på Avenyn på vänster sida där.



`49 00:02:24,580 --> 00:02:27,580`
Och det tänkte vi göra från klockan 18 då, den 24 mars.



`50 00:02:27,580 --> 00:02:32,580`
Och vi tänker vara så bold och säga att kom bara.



`51 00:02:32,580 --> 00:02:35,580`
Ja, exakt. Ni behöver inte anmäla er. Ni behöver bara dyka upp.



`52 00:02:35,580 --> 00:02:37,580`
Ni fem som lyssnar, kom.



`53 00:02:37,580 --> 00:02:38,580`
Såna det.



`54 00:02:38,580 --> 00:02:42,580`
Om ni vill ta reda på hur populära vi egentligen är så kan det vara roligt att dyka upp.



`55 00:02:42,580 --> 00:02:43,580`
Det kan inte bara bli du som kommer.



`56 00:02:43,580 --> 00:02:47,580`
Precis, och ni får titta efter oss. Vi kommer väl inte vara anmälda eller någonting sånt.



`57 00:02:47,580 --> 00:02:52,580`
Och om vi mot all förmodan har mejlat eller ändrat våra planer.



`58 00:02:52,580 --> 00:02:59,580`
Så håll koll på våran plock på sky för om vi fuckar upp det här så ska vi säga till att vi har fuckat upp.



`59 00:02:59,580 --> 00:03:02,580`
Exakt. Det lovar vi att göra i de kanaler vi har.



`60 00:03:02,580 --> 00:03:03,580`
Exakt.



`61 00:03:03,580 --> 00:03:08,580`
Men det var det om detta. Jesper, det är du som ska ta över spelpinnarna här.



`62 00:03:08,580 --> 00:03:09,580`
Så är det faktiskt.



`63 00:03:09,580 --> 00:03:13,580`
Nu ska vi göra någonting som vi aldrig har gjort i podcastens historia.



`64 00:03:13,580 --> 00:03:18,580`
Så ikväll så ska vi ta ett verkligt fall, alltså en incident.



`65 00:03:18,580 --> 00:03:24,580`
Och vad vi ska göra då är att försöka lista ut vad som hände.



`66 00:03:24,580 --> 00:03:29,580`
Utan att ha läst några analyser. Ingen här i panelen har läst analyserna.



`67 00:03:29,580 --> 00:03:33,580`
Och utan att ha kollat på några efterrapporter.



`68 00:03:33,580 --> 00:03:38,580`
Vi kommer då helt utan förutsättningar egentligen.



`69 00:03:38,580 --> 00:03:45,580`
Köra vår tankegång. Vi tänker högt. Vi har förmodligen fel om vissa delar.



`70 00:03:45,580 --> 00:03:47,580`
Och vi kommer kanske ha fel om massa saker.



`71 00:03:47,580 --> 00:03:50,580`
Och jag tänker att det är hela poängen.



`72 00:03:50,580 --> 00:03:55,580`
För jag tänker att vi ska försöka påvisa att det är svårt med säkerhet.



`73 00:03:55,580 --> 00:03:58,580`
Och att vi ska försöka ta oss an ett cold case här ikväll.



`74 00:03:58,580 --> 00:04:00,580`
Och vad är då ett cold case?



`75 00:04:00,580 --> 00:04:02,580`
Jo, men snabbt om det här formatet då.



`76 00:04:02,580 --> 00:04:05,580`
Det är att vi börjar med en ny sammanfattning.



`77 00:04:05,580 --> 00:04:08,580`
Bara fakta. Inga tekniska förklaringar överhuvudtaget.



`78 00:04:08,580 --> 00:04:11,580`
Sen diskuterar vi helt fritt vad vi tror hände.



`79 00:04:11,580 --> 00:04:14,580`
Och sen får vi facit.



`80 00:04:14,580 --> 00:04:16,580`
Och då jämför vi det, tänker jag.



`81 00:04:16,580 --> 00:04:18,580`
Men vad vi kom fram till.



`82 00:04:18,580 --> 00:04:20,580`
Känns läskigt.



`83 00:04:20,580 --> 00:04:22,580`
Vi alla här i panelen har fått samma brief.



`84 00:04:22,580 --> 00:04:26,580`
Ingen av oss har läst analysen i förväg.



`85 00:04:26,580 --> 00:04:28,580`
Jag blir lite gamemaster. Men jag har heller inte kollat på facit.



`86 00:04:28,580 --> 00:04:30,580`
Så att, så är det.



`87 00:04:30,580 --> 00:04:32,580`
Så, så är det.



`88 00:04:32,580 --> 00:04:34,580`
Vad tror ni om det?



`89 00:04:34,580 --> 00:04:37,580`
Ja, det här känns ju spännande och lite läskigt.



`90 00:04:37,580 --> 00:04:40,580`
Det kan ju hända. Det kan ju bli precis vad som helst.



`91 00:04:40,580 --> 00:04:44,580`
Och vad om lyssnaren undrar. Vi har ett papper som jag tror Jesper kommer läsa ihop.



`92 00:04:44,580 --> 00:04:48,580`
Och så har vi ett buzzwordkort där det finns lite mer information.



`93 00:04:48,580 --> 00:04:55,580`
Så att vi har inte mycket mer information än vad Jesper kommer läsa upp.



`94 00:04:55,580 --> 00:04:57,580`
Eller vad ni lyssnare har nu.



`95 00:04:57,580 --> 00:04:59,580`
Om de inte är redan insatta då.



`96 00:04:59,580 --> 00:05:03,580`
Så om ni är insatta på det här så kommer ni ju kunna titta och småfinnissa nu.



`97 00:05:03,580 --> 00:05:04,580`
Han var dumma nu.



`98 00:05:04,580 --> 00:05:08,580`
Exakt. Men ni kan ju också vara med och försöka säga vad knasiga ni är som resonerar sådär.



`99 00:05:08,580 --> 00:05:13,580`
Men en spännande fråga nu. Det här inträffade ju tidigare i 2025.



`100 00:05:13,580 --> 00:05:14,580`
Mm.



`101 00:05:14,580 --> 00:05:16,580`
Har vi pratat om det här i podcasten?



`102 00:05:16,580 --> 00:05:17,580`
Kanske.



`103 00:05:17,580 --> 00:05:19,580`
Det är det jag satt och funderade på också.



`104 00:05:19,580 --> 00:05:21,580`
Men det ringer ingen seriöst.



`105 00:05:21,580 --> 00:05:25,580`
Vag klocka vi kanske har nämnt någonting om en stor kryptohajs.



`106 00:05:25,580 --> 00:05:27,580`
Vi kommer komma in på det här snart.



`107 00:05:27,580 --> 00:05:30,580`
Men det är ingenting vi har gått igenom i detalj i alla fall.



`108 00:05:30,580 --> 00:05:32,580`
Så vi tänker att vi provar det här formatet.



`109 00:05:32,580 --> 00:05:36,580`
Det här är ju Jespers temaavsnitt.



`110 00:05:36,580 --> 00:05:38,580`
För jag kom inte på något annat tema.



`111 00:05:38,580 --> 00:05:40,580`
Så då kör vi en cold case drabbning här.



`112 00:05:40,580 --> 00:05:41,580`
Så får vi se vad det blir.



`113 00:05:41,580 --> 00:05:43,580`
Du byggde det här lite på, vad heter de?



`114 00:05:43,580 --> 00:05:44,580`
Hidden reality-spelen.



`115 00:05:44,580 --> 00:05:45,580`
Ja just det.



`116 00:05:45,580 --> 00:05:47,580`
Alltså lösa en mordgåta.



`117 00:05:47,580 --> 00:05:51,580`
Så du har bett Claude att göra en hidden reality av ett cybercase typ?



`118 00:05:51,580 --> 00:05:52,580`
Exakt.



`119 00:05:52,580 --> 00:05:56,580`
Och sen då i faser så att vi då kan göra bort oss så mycket som möjligt.



`120 00:05:56,580 --> 00:05:57,580`
Mm.



`121 00:05:57,580 --> 00:05:59,580`
För er lyssnarens förtjusning.



`122 00:05:59,580 --> 00:06:01,580`
Hidden reality-spelet är en jävla bra affärsidé ändå.



`123 00:06:01,580 --> 00:06:03,580`
Så är det någonting som bara går att använda en gång.



`124 00:06:03,580 --> 00:06:06,580`
Ja fast hidden reality är ju ofta, det är ju inte som exit.



`125 00:06:06,580 --> 00:06:07,580`
Exit måste man ju riva sönder.



`126 00:06:07,580 --> 00:06:08,580`
Det kan vara exit jag tänker på.



`127 00:06:08,580 --> 00:06:10,580`
Hidden reality kan man nog ändå återanvända lite.



`128 00:06:10,580 --> 00:06:11,580`
Ja så kanske det.



`129 00:06:11,580 --> 00:06:12,580`
Men nog om det.



`130 00:06:12,580 --> 00:06:15,580`
Ni som lyssnar är ju taggade på att höra det här nu då.



`131 00:06:15,580 --> 00:06:16,580`
Så jag tänker att vi drar igång.



`132 00:06:16,580 --> 00:06:17,580`
Kör.



`133 00:06:17,580 --> 00:06:19,580`
Resten kommer liksom att ordna sig.



`134 00:06:19,580 --> 00:06:21,580`
Så vi kör igång då.



`135 00:06:21,580 --> 00:06:23,580`
Dubai.



`136 00:06:23,580 --> 00:06:26,580`
21 februari 2025.



`137 00:06:26,580 --> 00:06:38,580`
Kryptobörsen Bybit med säte i Dubai meddelar på fredagskvällen att det blivit utsatta för dataintrång som resulterat i att 401 346 Ethereum.



`138 00:06:38,580 --> 00:06:42,580`
Motsvarande ungefär 1,5 miljarder dollar försvunnit ur detta fallet.



`139 00:06:42,580 --> 00:06:44,580`
Företagets plånbokssystem.



`140 00:06:44,580 --> 00:06:47,580`
Det är det största kryptostölden i historien.



`141 00:06:47,580 --> 00:06:52,580`
Bybit är en av världens största kryptobörser med över 60 miljoner registrerade användare.



`142 00:06:52,580 --> 00:06:59,580`
Bolagets vd Ben Zhao gick inom en timma live på Twitch för att kommunicera direkt med sina kunder.



`143 00:06:59,580 --> 00:07:06,580`
Han beskrev hur han under dagen hade godkänt vad som verkade vara en rutinmässig intern överföring.



`144 00:07:06,580 --> 00:07:10,580`
En operation han och hans team genomfört många gånger tidigare.



`145 00:07:10,580 --> 00:07:12,580`
Allt såg normalt ut uppgav Zhao.



`146 00:07:12,580 --> 00:07:16,580`
Gränssnitten, beloppen, adresserna, allt stämde.



`147 00:07:16,580 --> 00:07:21,580`
Bybit använde ett så kallat multi signature system för sina kalla plånböcker.



`148 00:07:21,580 --> 00:07:29,580`
Ett säkerhetssystem som kräver att man har tre separata auktoriserade personer som godkänner varje transaktion innan den kan genomföras.



`149 00:07:29,580 --> 00:07:34,580`
Alla tre godkänningsprocesser genomfördes utan tekniska fel den aktuella dagen.



`150 00:07:34,580 --> 00:07:36,580`
Trots det försvann pengarna.



`151 00:07:36,580 --> 00:07:42,580`
Inom 48 timmar efter stölden hade en stor del av de stulna tillgångarna redan förflyttats.



`152 00:07:42,580 --> 00:07:48,580`
Genom ett flertal mellanliggande konton och plånböcker spridda över ett dussintal blockkedjor.



`153 00:07:48,580 --> 00:07:57,580`
Bybit medlade omedelbart att man påbörjat arbetet med blockchainsanalysföretag, advokatbyråer och myndigheter för att spåra tillgångarna.



`154 00:07:57,580 --> 00:08:04,580`
Börsen bekräftade att den är solvent och att kundmedel inte påverkas.



`155 00:08:04,580 --> 00:08:08,580`
Förlusterna täcks av bolagets egna reserver.



`156 00:08:08,580 --> 00:08:10,580`
Utredningen inleddes parallellt.



`157 00:08:10,580 --> 00:08:16,580`
Av flera internationella säkerhetsföretag.



`158 00:08:16,580 --> 00:08:21,580`
Så nu tänker jag att vi ska ta med det här i diskussionen.



`159 00:08:21,580 --> 00:08:23,580`
Vi behöver inte skicka ut några svar precis ännu.



`160 00:08:23,580 --> 00:08:26,580`
Utan det vi ska titta på är då vad sticker ut?



`161 00:08:26,580 --> 00:08:28,580`
Är det någonting som...



`162 00:08:28,580 --> 00:08:30,580`
Är det någon luktad i fisk?



`163 00:08:30,580 --> 00:08:32,580`
Är det någon fisk begraven någonstans?



`164 00:08:32,580 --> 00:08:34,580`
Vad saknas i informationen?



`165 00:08:34,580 --> 00:08:38,580`
Och vad är det vi oroar oss mest för?



`166 00:08:38,580 --> 00:08:41,580`
Så jag tänker spontant på den här auktoriseringsprocessen.



`167 00:08:41,580 --> 00:08:43,580`
Hur ser den ut?



`168 00:08:43,580 --> 00:08:45,580`
Jag satt och funderade på det också.



`169 00:08:45,580 --> 00:08:47,580`
Det här är ju kalla plånböcker som ligger lokalt.



`170 00:08:47,580 --> 00:08:50,580`
Och om vi ska ha multisig.



`171 00:08:50,580 --> 00:08:56,580`
Är det på något sätt så att det skickas någon slags begäran till alla de här tre personerna då?



`172 00:08:56,580 --> 00:08:58,580`
Ja, jag antar det.



`173 00:08:58,580 --> 00:09:01,580`
Det måste ju ske kommunikation mellan de olika personerna.



`174 00:09:01,580 --> 00:09:04,580`
Jag tänker typ någon sån här Shazam shared secret historia kanske.



`175 00:09:04,580 --> 00:09:06,580`
Jag gissar på att de inte träffas fysiskt i sitt rum.



`176 00:09:06,580 --> 00:09:07,580`
Nej.



`177 00:09:07,580 --> 00:09:09,580`
Det kommer ju säkert...



`178 00:09:09,580 --> 00:09:13,580`
Jag gissar på att det är ett centralt system på något sätt som skickar ut begäran.



`179 00:09:13,580 --> 00:09:16,580`
Ungefär som vi signerar dokument idag.



`180 00:09:16,580 --> 00:09:17,580`
Ja, exakt.



`181 00:09:17,580 --> 00:09:19,580`
Det kommer ut en begäran till dig att signera och så gör du det.



`182 00:09:19,580 --> 00:09:21,580`
En begäran till mig att signera så gör jag det.



`183 00:09:21,580 --> 00:09:23,580`
En begäran till Johan att signera så gör han det. Klart.



`184 00:09:23,580 --> 00:09:27,580`
Alla tre grotkännande processer genomfördes utan tekniska fel.



`185 00:09:27,580 --> 00:09:31,580`
Så om någon då har på något sätt lurat den.



`186 00:09:31,580 --> 00:09:35,580`
Och då borde det ju vara så att om man lurar en eller tre har ingen betydelse.



`187 00:09:35,580 --> 00:09:38,580`
För har man lurat en så kan man bara skicka den till tre personer och så är man hemma.



`188 00:09:38,580 --> 00:09:41,580`
Ja, exakt. Att man attackerar signatur...



`189 00:09:41,580 --> 00:09:46,580`
Under förutsättningen då att det stämmer det som han sa här.



`190 00:09:46,580 --> 00:09:49,580`
Gränssnittet, beloppen och dessutom.



`191 00:09:49,580 --> 00:09:51,580`
Gränssnittet är ett ord som sticker ut för mig.



`192 00:09:51,580 --> 00:09:54,580`
Ja, alltså den uppenbara här typen i webbserver.



`193 00:09:54,580 --> 00:10:03,580`
Kan du skilja vad som går till signeringsoperationen kontra vad som visas i gujjet?



`194 00:10:03,580 --> 00:10:11,580`
Är det en spearfishingattack där de har byggt upp ett snarlikt gränssnitt som de då sen har lurat de här tre personerna?



`195 00:10:11,580 --> 00:10:17,580`
Det jag reagerar på spontant är ju liksom att 1,5 miljarder i en enda transaktion.



`196 00:10:17,580 --> 00:10:18,580`
Ja, det är rutinmässigt.



`197 00:10:18,580 --> 00:10:21,580`
Och det är inget som råkar hända.



`198 00:10:21,580 --> 00:10:26,580`
Det är liksom antingen ett väldigt misstag eller någon som har lagt ner sjukt mycket tid. Eller vad tror ni liksom?



`199 00:10:26,580 --> 00:10:31,580`
Ja, det här är ju inte vaniljatack det här på något sätt.



`200 00:10:31,580 --> 00:10:32,580`
Nej.



`201 00:10:32,580 --> 00:10:34,580`
Det är ju väldigt mycket spearfishing.



`202 00:10:34,580 --> 00:10:37,580`
Men jag tycker att, vad ska vi summera då? Vad är det som sticker ut med det här?



`203 00:10:37,580 --> 00:10:41,580`
Gränssnitten ser likadana ut. Vad är det som, om vi summerar lite.



`204 00:10:41,580 --> 00:10:46,580`
Jag tycker att det svåra här är att eftersom jag inte vet hur det här systemet funkar.



`205 00:10:46,580 --> 00:10:49,580`
Så blir det jävligt svårt att försöka lista ut vad som har hänt.



`206 00:10:49,580 --> 00:10:52,580`
Men man kan ju kvalificera gissningarna som sagt.



`207 00:10:52,580 --> 00:10:54,580`
Men vad är det som känns konstigt då?



`208 00:10:54,580 --> 00:10:56,580`
Vad säger The SpiderSense?



`209 00:10:56,580 --> 00:10:59,580`
Ja, men det är ju just det egentligen.



`210 00:10:59,580 --> 00:11:02,580`
Om man då killgissar att det funkar så var det att det här är signeringsoperation.



`211 00:11:02,580 --> 00:11:06,580`
Det är just det här som kommer ut.



`212 00:11:06,580 --> 00:11:08,580`
Det är det jag killgissar.



`213 00:11:08,580 --> 00:11:10,580`
Och då gissar jag på att det är på något sätt.



`214 00:11:10,580 --> 00:11:13,580`
Den kalla plånboken ligger i det systemet.



`215 00:11:13,580 --> 00:11:17,580`
Det vill säga att det inte är en kall plånbok på min dator och på din dator och på din dator.



`216 00:11:17,580 --> 00:11:19,580`
Utan det är ett centralt system som har en kall plånbok.



`217 00:11:19,580 --> 00:11:22,580`
Och det finns ett admin-gui på något sätt där du gör dina.



`218 00:11:22,580 --> 00:11:24,580`
Eller kopplat till det på något sätt.



`219 00:11:24,580 --> 00:11:26,580`
Det kan ju vara en klient också eventuellt.



`220 00:11:26,580 --> 00:11:28,580`
Men det måste ju vara kopplat till den kalla plånboken på något sätt.



`221 00:11:28,580 --> 00:11:30,580`
Förhoppningsvis någonting man kör internt.



`222 00:11:30,580 --> 00:11:31,580`
Men där du loggar in.



`223 00:11:31,580 --> 00:11:34,580`
Det kan vara en signaturklient som vi har allihopa på våra dator.



`224 00:11:34,580 --> 00:11:36,580`
Men det kommer en begäran till den.



`225 00:11:36,580 --> 00:11:37,580`
Som vi signar.



`226 00:11:37,580 --> 00:11:40,580`
Och det är kanske det som menas med att gränssnittet såg korrekt ut.



`227 00:11:40,580 --> 00:11:41,580`
Ja, precis.



`228 00:11:41,580 --> 00:11:45,580`
Om man tänker BankID och liknande system så brukar det vara väldigt viktigt just att



`229 00:11:45,580 --> 00:11:49,580`
vad du gör ska ingå i signeringsoperationen.



`230 00:11:49,580 --> 00:11:55,580`
Jag vet att för någon gång för väldigt många år sedan så gjorde jag ett test där



`231 00:11:55,580 --> 00:12:00,580`
jag kunde byta vad som signerades men fortfarande kom igenom ett flöde.



`232 00:12:00,580 --> 00:12:03,580`
Där är jag med och därför såg jag lite vad du ut efter Jesper också tror jag.



`233 00:12:03,580 --> 00:12:05,580`
Det kan ju mycket väl vara så att det var inte det.



`234 00:12:05,580 --> 00:12:08,580`
Alltså en och en halv miljard, det är inte vanligt.



`235 00:12:08,580 --> 00:12:12,580`
Utan det de såg och signerade, det var vaniltransaktioner.



`236 00:12:12,580 --> 00:12:15,580`
Men det som hände i bakgrunden var något helt annat.



`237 00:12:15,580 --> 00:12:18,580`
Så att det såg helt vanligt ut, iguit.



`238 00:12:18,580 --> 00:12:21,580`
Men det de signerade och faktiskt genomförde var något helt annat.



`239 00:12:21,580 --> 00:12:23,580`
Destination och belopp var något helt annat.



`240 00:12:23,580 --> 00:12:26,580`
Vad är det som oroar er mest när ni hör det här?



`241 00:12:26,580 --> 00:12:28,580`
Att de inte vet hur det gick till.



`242 00:12:28,580 --> 00:12:30,580`
Det kan ju hända igen.



`243 00:12:30,580 --> 00:12:36,580`
Som vd hade jag konstaterat att vi signerar ingenting mer nu.



`244 00:12:36,580 --> 00:12:43,580`
Det låter ju som om man skulle kunna jämföra det med en JVT-signatursattack.



`245 00:12:43,580 --> 00:12:46,580`
Ja, att du kan manipulera.



`246 00:12:46,580 --> 00:12:50,580`
Precis, eller att du kan få en signatur att stämma för ett annat konto.



`247 00:12:50,580 --> 00:12:55,580`
Jag tror det handlar mycket mer om att det här är ett GUI-issue snarare.



`248 00:12:55,580 --> 00:12:56,580`
Det vill säga, jag visar någonting för mig.



`249 00:12:56,580 --> 00:12:57,580`
Du visar någonting.



`250 00:12:57,580 --> 00:12:59,580`
Men du signerar något annat.



`251 00:12:59,580 --> 00:13:01,580`
Men om vi hoppar in i en hypotes här.



`252 00:13:01,580 --> 00:13:04,580`
Om vi går vidare till nästa fas lite.



`253 00:13:04,580 --> 00:13:07,580`
Men får vi gissa olika teorier?



`254 00:13:07,580 --> 00:13:09,580`
Du måste hålla med oss, Peter.



`255 00:13:09,580 --> 00:13:15,580`
Men jag tänker att den första fingertoppskänslan, det behöver vi inte prata så mycket om teknik.



`256 00:13:15,580 --> 00:13:18,580`
Vad är det som sticker ut i det vi läser?



`257 00:13:18,580 --> 00:13:22,580`
Jag håller med om att 1,5 miljarder, allt såg bra ut.



`258 00:13:22,580 --> 00:13:24,580`
Det är normalt.



`259 00:13:24,580 --> 00:13:25,580`
Det känns ganska excessivt.



`260 00:13:25,580 --> 00:13:26,580`
Ja, alltså.



`261 00:13:26,580 --> 00:13:28,580`
De måste väl vara rätt stora?



`262 00:13:28,580 --> 00:13:33,580`
Det täcks upp av företagets tillgångar.



`263 00:13:33,580 --> 00:13:35,580`
Då måste de ha en del på banken.



`264 00:13:35,580 --> 00:13:38,580`
Är det verkligen så?



`265 00:13:38,580 --> 00:13:40,580`
Är det verkligen sant det där?



`266 00:13:40,580 --> 00:13:43,580`
Alltså bara det att man nämner att vi fortfarande är solvent.



`267 00:13:43,580 --> 00:13:46,580`
Alltså vi är fortfarande likvida och har soliditeten kvar.



`268 00:13:46,580 --> 00:13:48,580`
Efter att man har tappat några miljarder.



`269 00:13:48,580 --> 00:13:50,580`
Det känns också såhär.



`270 00:13:50,580 --> 00:13:51,580`
Det är lite sketchy.



`271 00:13:51,580 --> 00:13:54,580`
Men okej, gräns lite beloppen.



`272 00:13:54,580 --> 00:14:06,580`
Så frågan som slår mig är, är det här ett angrepp mot deras mjukvara, den som är publikpublicerad?



`273 00:14:06,580 --> 00:14:16,580`
Det vill säga att de som ska godkänna den här typen av transaktioner använder samma mjukvara som det publika internet gör?



`274 00:14:16,580 --> 00:14:18,580`
Just det.



`275 00:14:18,580 --> 00:14:22,580`
Jag hade ju spontant tänkt, ifall du nu sitter i en administratörsroll på det här bolaget.



`276 00:14:22,580 --> 00:14:26,580`
Och har möjlighet att överföra 1,5 miljarder dollar.



`277 00:14:26,580 --> 00:14:30,580`
Det kanske man gör i en intern process, i en intern mjukvara.



`278 00:14:30,580 --> 00:14:31,580`
Helst.



`279 00:14:31,580 --> 00:14:34,580`
Snarare än någonting som är publicerat på internet.



`280 00:14:34,580 --> 00:14:36,580`
Jag tänker att vi kommer in mer på tekniken sen.



`281 00:14:36,580 --> 00:14:39,580`
Jag tänker mer bara såhär generiskt.



`282 00:14:39,580 --> 00:14:42,580`
Det hade ju kunnat vara liksom ett bankgrån.



`283 00:14:42,580 --> 00:14:43,580`
Vad känner vi?



`284 00:14:43,580 --> 00:14:45,580`
Eller en insiderfaktor på det här.



`285 00:14:45,580 --> 00:14:46,580`
Ja men exakt såhär.



`286 00:14:46,580 --> 00:14:48,580`
Skulle det kunna vara en insiderfaktor?



`287 00:14:48,580 --> 00:14:50,580`
Försöker de dölja någonting?



`288 00:14:50,580 --> 00:14:53,580`
Jag tänker att nästa fas blir lite hypotesfas och såhär.



`289 00:14:53,580 --> 00:14:54,580`
Vad tror vi det är en teknisk...



`290 00:14:54,580 --> 00:14:57,580`
Du är ju lite inne på att de försöker göra en...



`291 00:14:57,580 --> 00:15:00,580`
De själva försöker göra någon form av skam här mot sina användare.



`292 00:15:00,580 --> 00:15:01,580`
Alltså kanske, vad vet jag.



`293 00:15:01,580 --> 00:15:05,580`
Vi har ju sett folk, ja men ta Mount Gox till exempel.



`294 00:15:05,580 --> 00:15:07,580`
Det är ju ganska tydligt att...



`295 00:15:07,580 --> 00:15:08,580`
Pump and dump.



`296 00:15:08,580 --> 00:15:12,580`
Ja men fast det sjuka är att de som hade kryptovaluta.



`297 00:15:12,580 --> 00:15:16,580`
Jag har en vän som har haft kryptovaluta i Mount Gox och blev av med den också.



`298 00:15:16,580 --> 00:15:19,580`
Vi är faktiskt tillbaka lite nu då för att alla tillgångar frös ju till slut.



`299 00:15:19,580 --> 00:15:21,580`
Och sen blev det ett legal case.



`300 00:15:21,580 --> 00:15:23,580`
Och under den tiden så har ju bitcoin bara fortsatt upp.



`301 00:15:23,580 --> 00:15:24,580`
Just det.



`302 00:15:24,580 --> 00:15:26,580`
Så att det blir en ganska anställd summa så att de...



`303 00:15:26,580 --> 00:15:27,580`
Jo, det är sant.



`304 00:15:27,580 --> 00:15:30,580`
En anställd summa som gjorde att de ändå kunde betala tillbaka en del utav...



`305 00:15:30,580 --> 00:15:35,580`
Ja, men det krävdes ju att någon typ av federal myndighet gick in och tog allting.



`306 00:15:35,580 --> 00:15:36,580`
Ja, helt sant.



`307 00:15:36,580 --> 00:15:40,580`
Och det vet vi ju inte ifall det har hänt utifrån den information vi har här i alla fall.



`308 00:15:40,580 --> 00:15:47,580`
Va Peter, har du någonting att tillänga i den första såhär snabba, första reflektionsfasen här?



`309 00:15:47,580 --> 00:15:48,580`
Alltså...



`310 00:15:48,580 --> 00:15:50,580`
Alltså jag har ju tänkt...



`311 00:15:50,580 --> 00:15:53,580`
Jag vet inte, fick jag lov att spekulera i attack?



`312 00:15:53,580 --> 00:15:55,580`
Nej, det får du göra på nästa steg.



`313 00:15:55,580 --> 00:15:56,580`
Okej, det får jag göra på nästa steg.



`314 00:15:56,580 --> 00:15:58,580`
För då tänker jag att jag ska ge lite mer också.



`315 00:15:58,580 --> 00:15:59,580`
Eller oss lite mer.



`316 00:15:59,580 --> 00:16:00,580`
Mm.



`317 00:16:02,580 --> 00:16:03,580`
För...



`318 00:16:03,580 --> 00:16:05,580`
Men jag tänker att vi kan ramla in på det här för vi har redan...



`319 00:16:05,580 --> 00:16:06,580`
Ni har redan...



`320 00:16:06,580 --> 00:16:07,580`
Ni är så snabba.



`321 00:16:07,580 --> 00:16:09,580`
Så ni har redan liksom varit där och lagt det där.



`322 00:16:09,580 --> 00:16:10,580`
Men om vi går över till...



`323 00:16:10,580 --> 00:16:13,580`
Till att vi börjar fråga oss hur kom de in?



`324 00:16:13,580 --> 00:16:14,580`
Mm.



`325 00:16:14,580 --> 00:16:15,580`
Vad tror vi?



`326 00:16:15,580 --> 00:16:17,580`
Vad är rimligt baserat på den informationen vi har fått?



`327 00:16:17,580 --> 00:16:23,580`
Mattias nämnde ganska snabbt att man försöker hoppa in någonstans i signeringsprocessen, vilket känns rimligt.



`328 00:16:23,580 --> 00:16:33,580`
Vi har pratat om spearfishing, det vill säga att man skapar någon form utav pretext där det känns rimligt för folk som signerar transaktioner att göra det.



`329 00:16:33,580 --> 00:16:35,580`
Fast det är då en fakesite.



`330 00:16:35,580 --> 00:16:37,580`
Den känns också såhär...



`331 00:16:37,580 --> 00:16:39,580`
Är det så, så blir man ju lite nervös.



`332 00:16:39,580 --> 00:16:40,580`
Ja.



`333 00:16:40,580 --> 00:16:41,580`
För att om det är någon...



`334 00:16:41,580 --> 00:16:43,580`
Då var du också lite inne på ju det här med att...



`335 00:16:43,580 --> 00:16:44,580`
Är det här verkligen publik?



`336 00:16:44,580 --> 00:16:46,580`
Ska det vara på internet och...



`337 00:16:46,580 --> 00:16:47,580`
Ja.



`338 00:16:47,580 --> 00:16:48,580`
Ja men precis.



`339 00:16:48,580 --> 00:16:52,580`
Och ska du då ha liksom klonat ett internt gränssnitt?



`340 00:16:52,580 --> 00:16:53,580`
Men...



`341 00:16:53,580 --> 00:16:54,580`
Det blir väldigt svårt.



`342 00:16:54,580 --> 00:16:55,580`
Precis.



`343 00:16:55,580 --> 00:16:58,580`
Och spännande fråga här är ju när man brukar prata om phishing resistant liksom.



`344 00:16:58,580 --> 00:16:59,580`
Är...



`345 00:16:59,580 --> 00:17:01,580`
Till exempel med FIDO2...



`346 00:17:01,580 --> 00:17:03,580`
Vad heter den här?



`347 00:17:03,580 --> 00:17:04,580`
Web...



`348 00:17:04,580 --> 00:17:05,580`
WebOF.



`349 00:17:05,580 --> 00:17:06,580`
WebOFen.



`350 00:17:06,580 --> 00:17:09,580`
Att liksom det finns med i signeringen.



`351 00:17:09,580 --> 00:17:10,580`
Finns det med...



`352 00:17:10,580 --> 00:17:12,580`
Vilken url var det gjord emot liksom?



`353 00:17:12,580 --> 00:17:13,580`
Alltså såhär...



`354 00:17:13,580 --> 00:17:15,580`
Själva tekniken de använder...



`355 00:17:15,580 --> 00:17:16,580`
Är den phishing resistant?



`356 00:17:16,580 --> 00:17:19,580`
Eller går det att lura över dem till en annan sajt?



`357 00:17:19,580 --> 00:17:20,580`
Ja exakt.



`358 00:17:20,580 --> 00:17:21,580`
Det är ju en spännande fråga.



`359 00:17:21,580 --> 00:17:23,580`
Vem var det som sa insiderhot?



`360 00:17:23,580 --> 00:17:25,580`
Ja jag nämnde det i alla fall som en idé.



`361 00:17:25,580 --> 00:17:26,580`
För det...



`362 00:17:26,580 --> 00:17:29,580`
Det tänker jag ju såhär att om man ger ett instick på insiderhotet så är det såhär...



`363 00:17:29,580 --> 00:17:30,580`
Det är ju multisignature.



`364 00:17:30,580 --> 00:17:31,580`
Det är ju liksom...



`365 00:17:31,580 --> 00:17:33,580`
Mer än en person som behöver vara med.



`366 00:17:33,580 --> 00:17:34,580`
Tre.



`367 00:17:34,580 --> 00:17:35,580`
När man har bestämt va?



`368 00:17:35,580 --> 00:17:37,580`
Och det är ju...



`369 00:17:37,580 --> 00:17:40,580`
Det är ju ändå en ansenlig kedja att försöka phisha tänker jag.



`370 00:17:40,580 --> 00:17:41,580`
Det känns ändå som att det...



`371 00:17:41,580 --> 00:17:44,580`
Det är även kopplat till det här med publik eller inte?



`372 00:17:44,580 --> 00:17:45,580`
Jag menar...



`373 00:17:45,580 --> 00:17:47,580`
Är det här en proprietär intern lösning?



`374 00:17:47,580 --> 00:17:50,580`
Hur fan ska någon extern lätt kunna lista ut det?



`375 00:17:50,580 --> 00:17:51,580`
Det kräver ju...



`376 00:17:51,580 --> 00:17:54,580`
Däremot om du har en intern person som sitter på insidan.



`377 00:17:54,580 --> 00:17:57,580`
Dels kommer åt den och dels vet du hur processen funkar.



`378 00:17:57,580 --> 00:17:59,580`
Då är det lättare...



`379 00:17:59,580 --> 00:18:03,580`
Om du då kan manipulera deras byggserver eller någonting för att...



`380 00:18:03,580 --> 00:18:05,580`
För att initiera dig i...



`381 00:18:05,580 --> 00:18:06,580`
Eller till och med hitta...



`382 00:18:06,580 --> 00:18:08,580`
Veta att det finns en flow i den.



`383 00:18:08,580 --> 00:18:11,580`
Just när du säger att du signerar en sak men den utför något annat.



`384 00:18:11,580 --> 00:18:14,580`
Jag har ju för övrigt identifierat en infoläcka.



`385 00:18:14,580 --> 00:18:16,580`
Jag vet inte om jag får släppa det nu.



`386 00:18:16,580 --> 00:18:21,580`
Jespers dokumentation läcker information som vi inte fått än.



`387 00:18:21,580 --> 00:18:25,580`
Det är nämligen i buzzwordkortet som jag hittat i Duelltime.



`388 00:18:25,580 --> 00:18:29,580`
Där beskrivs det att Duelltime var sjutton dagar.



`389 00:18:29,580 --> 00:18:31,580`
Så vi vet...



`390 00:18:31,580 --> 00:18:33,580`
Vi som har läst ordlistan...



`391 00:18:33,580 --> 00:18:35,580`
Det läcker alltid.



`392 00:18:35,580 --> 00:18:41,580`
Vi vet att från Initial Compromise så tog det sjutton dagar innan tackan genomfördes.



`393 00:18:41,580 --> 00:18:43,580`
Och vi vet dessutom att...



`394 00:18:43,580 --> 00:18:44,580`
Och jag tycker det här...



`395 00:18:44,580 --> 00:18:46,580`
Det är exakt det här som ska ske nu.



`396 00:18:46,580 --> 00:18:47,580`
För att jag...



`397 00:18:47,580 --> 00:18:50,580`
Ni som inte förstår det här så är det alla Dungeons & Dragons.



`398 00:18:50,580 --> 00:18:51,580`
Jag har...



`399 00:18:51,580 --> 00:18:52,580`
Jag...



`400 00:18:52,580 --> 00:18:55,580`
För att inte det här ska spåra ut fullständigt så har jag någon form av tågordning här.



`401 00:18:55,580 --> 00:18:59,580`
Och det kom jättelägligt att den här dök upp Peter.



`402 00:18:59,580 --> 00:19:02,580`
Men sjutton dagar innebär ju för mig att...



`403 00:19:02,580 --> 00:19:08,580`
Det är en attack som är i så pass enkelhet eller så pass...



`404 00:19:08,580 --> 00:19:11,580`
Nära hur andra attacker gått till tidigare.



`405 00:19:11,580 --> 00:19:12,580`
Att du har...



`406 00:19:12,580 --> 00:19:15,580`
Kunnat komma in i systemet och kunnat förstå det.



`407 00:19:15,580 --> 00:19:19,580`
Och du har kunnat bygga upp den här attacken...



`408 00:19:19,580 --> 00:19:21,580`
På rimlig tid.



`409 00:19:21,580 --> 00:19:23,580`
Det är liksom inte så att det har skett månader.



`410 00:19:23,580 --> 00:19:24,580`
Det är inte custom-kasten liksom.



`411 00:19:24,580 --> 00:19:25,580`
Precis.



`412 00:19:25,580 --> 00:19:28,580`
Eller så är det det men man kanske haft bra förkunskaper då.



`413 00:19:28,580 --> 00:19:29,580`
Ja, extremt bra förkunskaper.



`414 00:19:29,580 --> 00:19:30,580`
Ja, precis.



`415 00:19:30,580 --> 00:19:32,580`
Alltså vi kan ju ha antat att de här människorna hackar...



`416 00:19:32,580 --> 00:19:34,580`
Såna här grejer.



`417 00:19:34,580 --> 00:19:36,580`
Betydligt mer än vad vi gör.



`418 00:19:36,580 --> 00:19:38,580`
Vi har ju sett attacker mot...



`419 00:19:38,580 --> 00:19:40,580`
Typ Swift...



`420 00:19:40,580 --> 00:19:42,580`
Systemet heter det.



`421 00:19:42,580 --> 00:19:44,580`
Banköverföringssystemet.



`422 00:19:44,580 --> 00:19:46,580`
Som gick ut på att de hade en initial compromise.



`423 00:19:46,580 --> 00:19:49,580`
Och sen satt i bakgrunden och lärde sig exakt hur hela...



`424 00:19:49,580 --> 00:19:52,580`
Signerings- och transaktionsförflödet...



`425 00:19:52,580 --> 00:19:54,580`
Funkade innan de launchade själva attacken.



`426 00:19:54,580 --> 00:19:56,580`
Men det känns svårt att göra på sjutton dagar.



`427 00:19:56,580 --> 00:19:58,580`
Ja.



`428 00:19:58,580 --> 00:20:01,580`
Om inte den här banken funkar väldigt likt andra grejer...



`429 00:20:01,580 --> 00:20:03,580`
De har hackat på tidigare.



`430 00:20:03,580 --> 00:20:05,580`
Så kan det ju vara.



`431 00:20:05,580 --> 00:20:07,580`
Men på sjutton dagar...



`432 00:20:07,580 --> 00:20:09,580`
Så hade det ju definitivt gått att typ...



`433 00:20:09,580 --> 00:20:11,580`
Borka en webbserver och byta...



`434 00:20:11,580 --> 00:20:13,580`
Vilket gujje folk...



`435 00:20:13,580 --> 00:20:15,580`
Får se versus...



`436 00:20:15,580 --> 00:20:17,580`
Vad som händer.



`437 00:20:17,580 --> 00:20:19,580`
Sen...



`438 00:20:19,580 --> 00:20:21,580`
Racecondition och sånt förekommer väl...



`439 00:20:21,580 --> 00:20:23,580`
I såna här grejer.



`440 00:20:23,580 --> 00:20:25,580`
Även om jag inte har jättekoll på...



`441 00:20:25,580 --> 00:20:27,580`
Vad är våran initiala...



`442 00:20:27,580 --> 00:20:29,580`
Tack-vektor då?



`443 00:20:29,580 --> 00:20:31,580`
Ska jag summera lite...



`444 00:20:31,580 --> 00:20:33,580`
Vad jag har plockat upp i rummet då?



`445 00:20:33,580 --> 00:20:35,580`
Fishing har vi pratat om.



`446 00:20:35,580 --> 00:20:37,580`
Social engineering-aspekten i det.



`447 00:20:37,580 --> 00:20:39,580`
Det skulle kunna vara en tänkbar väg.



`448 00:20:39,580 --> 00:20:41,580`
Att man bygger en infrastruktur...



`449 00:20:41,580 --> 00:20:43,580`
Och försöker lura de här.



`450 00:20:43,580 --> 00:20:45,580`
Men vi har också samtidigt lite debunkat den.



`451 00:20:45,580 --> 00:20:47,580`
För att det verkar orimligt.



`452 00:20:47,580 --> 00:20:49,580`
Tre pers tar det ju inte samtidigt.



`453 00:20:49,580 --> 00:20:51,580`
Men däremot en av dem eller nåt.



`454 00:20:51,580 --> 00:20:53,580`
För att komma in i infran på nåt sätt.



`455 00:20:53,580 --> 00:20:55,580`
Och vi nämnde lite att...



`456 00:20:55,580 --> 00:20:57,580`
Skulle det kunna vara en komplementerad signeringsnyckel.



`457 00:20:57,580 --> 00:20:59,580`
Det avfärdas vi väl ändå lite i.



`458 00:20:59,580 --> 00:21:01,580`
I och med att vi behöver tre.



`459 00:21:01,580 --> 00:21:03,580`
Jag tänker att jag ska ge ett instyck...



`460 00:21:03,580 --> 00:21:05,580`
Till det här.



`461 00:21:05,580 --> 00:21:07,580`
Ska jag ge en liten bit information till.



`462 00:21:07,580 --> 00:21:09,580`
Som kommer hjälpa oss vidare i analysen kanske.



`463 00:21:09,580 --> 00:21:11,580`
Det är att Bybit.



`464 00:21:11,580 --> 00:21:13,580`
Byggde inte in sin plånbok själva.



`465 00:21:13,580 --> 00:21:15,580`
Utan de använde en tredjeparts mjukvara.



`466 00:21:15,580 --> 00:21:17,580`
Babybit.



`467 00:21:17,580 --> 00:21:19,580`
Ja förlåt. Babybit.



`468 00:21:19,580 --> 00:21:21,580`
De använde alltså.



`469 00:21:21,580 --> 00:21:23,580`
En tredjeparts mjukvara för plånböckerna.



`470 00:21:23,580 --> 00:21:25,580`
Det är någonting som vi.



`471 00:21:25,580 --> 00:21:27,580`
Kan spinna vidare på.



`472 00:21:27,580 --> 00:21:29,580`
Jag tänker ju spontant på.



`473 00:21:29,580 --> 00:21:31,580`
Skulle man kunna.



`474 00:21:31,580 --> 00:21:33,580`
Alltså vi har ju sett.



`475 00:21:33,580 --> 00:21:35,580`
Chalud.



`476 00:21:35,580 --> 00:21:37,580`
Alltså våran mask. Kan det vara någon supply chain idé.



`477 00:21:37,580 --> 00:21:39,580`
Bakom det här kanske.



`478 00:21:39,580 --> 00:21:41,580`
Jag menar att de har.



`479 00:21:41,580 --> 00:21:43,580`
Att det är en open source plånbok då på något sätt.



`480 00:21:43,580 --> 00:21:45,580`
Som de varit inne och mäcklat med.



`481 00:21:45,580 --> 00:21:47,580`
Ja eller bara det faktum.



`482 00:21:47,580 --> 00:21:49,580`
Att deras plattform.



`483 00:21:49,580 --> 00:21:51,580`
Vilar på tredjeparts mjukvara.



`484 00:21:51,580 --> 00:21:53,580`
Var hämtar man.



`485 00:21:53,580 --> 00:21:55,580`
Tredjeparts mjukvara ifrån.



`486 00:21:55,580 --> 00:21:57,580`
Ja exakt.



`487 00:21:57,580 --> 00:21:59,580`
Om man köper den kanske också som tjänst.



`488 00:21:59,580 --> 00:22:01,580`
Ja så kan det vara.



`489 00:22:01,580 --> 00:22:03,580`
Men det har vi varit inne på lite.



`490 00:22:03,580 --> 00:22:05,580`
Att det är en hostad miljö på något sätt.



`491 00:22:05,580 --> 00:22:07,580`
Och det är också så att.



`492 00:22:07,580 --> 00:22:09,580`
Om de är komplementerade med.



`493 00:22:09,580 --> 00:22:11,580`
Antingen phishing eller.



`494 00:22:11,580 --> 00:22:13,580`
Liksom någon.



`495 00:22:13,580 --> 00:22:15,580`
De hade en osäker SSO.



`496 00:22:15,580 --> 00:22:17,580`
Upp ut mot internet eller vad som helst.



`497 00:22:17,580 --> 00:22:19,580`
Men det har skett någon sorts kompromiss.



`498 00:22:19,580 --> 00:22:21,580`
Om de.



`499 00:22:21,580 --> 00:22:23,580`
Kör en standard mjukvara.



`500 00:22:23,580 --> 00:22:25,580`
Det stödjer ju också tesen att du på rimlig tid.



`501 00:22:25,580 --> 00:22:27,580`
Kan göra.



`502 00:22:27,580 --> 00:22:29,580`
En attack för att du har.



`503 00:22:29,580 --> 00:22:31,580`
Sett de här flöden och du har god.



`504 00:22:31,580 --> 00:22:33,580`
Tillgång till de här och har gjort.



`505 00:22:33,580 --> 00:22:35,580`
Attacken mot sådana grejer tidigare.



`506 00:22:35,580 --> 00:22:37,580`
Och den här attacken kan ju då gått.



`507 00:22:37,580 --> 00:22:39,580`
Även mot den.



`508 00:22:39,580 --> 00:22:41,580`
Systemet om det är en tredjeparts hostad.



`509 00:22:41,580 --> 00:22:43,580`
Alltså den SAS tjänsten någonting.



`510 00:22:43,580 --> 00:22:45,580`
Så kan attacken inte vara mot Bybit direkt.



`511 00:22:45,580 --> 00:22:47,580`
Utan till den till exempel.



`512 00:22:47,580 --> 00:22:49,580`
Men jag menar nu sitter vi och killgissar hårt.



`513 00:22:49,580 --> 00:22:51,580`
Det är det hela poängen.



`514 00:22:51,580 --> 00:22:53,580`
Att vi ska killgissa.



`515 00:22:53,580 --> 00:22:55,580`
För jag menar det.



`516 00:22:55,580 --> 00:22:57,580`
Jag tycker ändå vi har sagt.



`517 00:22:57,580 --> 00:22:59,580`
Mycket bra grejer där.



`518 00:22:59,580 --> 00:23:01,580`
Vi har ganska snabbt identifierat hur.



`519 00:23:01,580 --> 00:23:03,580`
Autorisation och åt borde fungera.



`520 00:23:03,580 --> 00:23:05,580`
Och att det inte har gjort det.



`521 00:23:05,580 --> 00:23:07,580`
Vi har kanske ändå.



`522 00:23:07,580 --> 00:23:09,580`
Summerat ihop oss till.



`523 00:23:09,580 --> 00:23:11,580`
Jag saknar däremot.



`524 00:23:11,580 --> 00:23:13,580`
Några grejer och.



`525 00:23:13,580 --> 00:23:15,580`
Ingen utav er har nämnt statsaktör.



`526 00:23:15,580 --> 00:23:17,580`
Till exempel.



`527 00:23:17,580 --> 00:23:19,580`
Varför skulle vi göra det?



`528 00:23:19,580 --> 00:23:21,580`
Det är jättebra.



`529 00:23:21,580 --> 00:23:23,580`
Vi har en annan.



`530 00:23:23,580 --> 00:23:25,580`
Det är också Red Herring.



`531 00:23:25,580 --> 00:23:27,580`
Som är i Buzzwords.



`532 00:23:27,580 --> 00:23:29,580`
Så jag håller med därför.



`533 00:23:29,580 --> 00:23:31,580`
Varför skulle det ändra attackbilden.



`534 00:23:31,580 --> 00:23:33,580`
Överhuvudtaget egentligen.



`535 00:23:33,580 --> 00:23:35,580`
Varför skulle de hålla på med det.



`536 00:23:35,580 --> 00:23:37,580`
Det är väl de.



`537 00:23:37,580 --> 00:23:39,580`
De är ju duktiga på det.



`538 00:23:39,580 --> 00:23:41,580`
Jag läste faktiskt en ganska kul bloggpost.



`539 00:23:41,580 --> 00:23:43,580`
På det ämnet.



`540 00:23:43,580 --> 00:23:45,580`
Det var en kille som sa det.



`541 00:23:45,580 --> 00:23:47,580`
Vi ska sluta använda nation state.



`542 00:23:47,580 --> 00:23:49,580`
Det är oviktigt om det är nation state.



`543 00:23:49,580 --> 00:23:51,580`
Och vilken nation state det är.



`544 00:23:51,580 --> 00:23:53,580`
Det är inte viktigt ur ett tekniskt perspektiv.



`545 00:23:53,580 --> 00:23:55,580`
Det här är en attack.



`546 00:23:55,580 --> 00:23:57,580`
Det är så uttjatat ord nu.



`547 00:23:57,580 --> 00:23:59,580`
Det betyder ingenting.



`548 00:23:59,580 --> 00:24:01,580`
Det var en sidospår.



`549 00:24:01,580 --> 00:24:03,580`
Nu måste jag kolla lite facit här.



`550 00:24:03,580 --> 00:24:05,580`
Eller inte facit. I min pretext.



`551 00:24:05,580 --> 00:24:07,580`
Det var.



`552 00:24:07,580 --> 00:24:09,580`
De nämnde.



`553 00:24:09,580 --> 00:24:11,580`
Inget om det var.



`554 00:24:11,580 --> 00:24:13,580`
Det gör de faktiskt inte.



`555 00:24:13,580 --> 00:24:15,580`
De nämnde inte om det är cold wallets eller inte.



`556 00:24:15,580 --> 00:24:17,580`
Jo cold wallets tror de.



`557 00:24:17,580 --> 00:24:19,580`
Eller det stod kanske.



`558 00:24:19,580 --> 00:24:21,580`
Överst i buzzword orden.



`559 00:24:21,580 --> 00:24:23,580`
Det är också en bra fråga.



`560 00:24:23,580 --> 00:24:25,580`
Vad betyder en cold wallet i det här fallet.



`561 00:24:25,580 --> 00:24:27,580`
Om den ändå är online på något sätt.



`562 00:24:27,580 --> 00:24:29,580`
Ja det är ju det den inte är då.



`563 00:24:29,580 --> 00:24:31,580`
En cold wallet är ju förmodligen.



`564 00:24:31,580 --> 00:24:33,580`
En hårdvarubaserad plånbok.



`565 00:24:33,580 --> 00:24:35,580`
En device som man då.



`566 00:24:35,580 --> 00:24:37,580`
Har i kombination med.



`567 00:24:37,580 --> 00:24:39,580`
En hot wallet.



`568 00:24:39,580 --> 00:24:41,580`
Alltså en lätt tillgänglig.



`569 00:24:41,580 --> 00:24:43,580`
En mjukvaruplånbok kanske.



`570 00:24:43,580 --> 00:24:45,580`
Och då kan man ju också kanske spekulera i.



`571 00:24:45,580 --> 00:24:47,580`
Men den kan ju inte vara helt cold.



`572 00:24:47,580 --> 00:24:49,580`
Om du kan göra operationer mot den.



`573 00:24:49,580 --> 00:24:51,580`
Nej men du kan ju ståra.



`574 00:24:51,580 --> 00:24:53,580`
Alla dina. Du kan ju ha flera plånböcker.



`575 00:24:53,580 --> 00:24:55,580`
Och du kan ha plånböcker i plånböcker.



`576 00:24:55,580 --> 00:24:57,580`
Som bara har vissa coins och delar med i 3D.



`577 00:24:57,580 --> 00:24:59,580`
Så det finns arkitektur. Wallet är wallet.



`578 00:24:59,580 --> 00:25:01,580`
Chilli wallet skulle jag vilja kalla den här.



`579 00:25:01,580 --> 00:25:03,580`
Den är ju uppenbar.



`580 00:25:03,580 --> 00:25:05,580`
Nej men dit jag vill komma då.



`581 00:25:05,580 --> 00:25:07,580`
Skulle man kunna tänka sig att det är en attack.



`582 00:25:07,580 --> 00:25:09,580`
Mot hårdvaran.



`583 00:25:09,580 --> 00:25:11,580`
Det skulle man kunna göra.



`584 00:25:11,580 --> 00:25:13,580`
Däremot så.



`585 00:25:13,580 --> 00:25:15,580`
Men återigen då måste hårdvaran.



`586 00:25:15,580 --> 00:25:17,580`
Vara uppkopplad på något sätt eller.



`587 00:25:17,580 --> 00:25:19,580`
Om det är en offline cold wallet.



`588 00:25:19,580 --> 00:25:21,580`
En fysisk pryl som jag har jämte med på skrivbordet.



`589 00:25:21,580 --> 00:25:23,580`
Då ser jag inte.



`590 00:25:23,580 --> 00:25:25,580`
Hur du ska kunna.



`591 00:25:25,580 --> 00:25:27,580`
Spara till det här för tre personer.



`592 00:25:27,580 --> 00:25:29,580`
Som på olika geografiska platser.



`593 00:25:29,580 --> 00:25:31,580`
Det blir ju svårt. Ja.



`594 00:25:31,580 --> 00:25:33,580`
Någonstans måste ju.



`595 00:25:33,580 --> 00:25:35,580`
Någonstans måste ju de här.



`596 00:25:35,580 --> 00:25:37,580`
Transaktionerna göras möjliga online.



`597 00:25:37,580 --> 00:25:39,580`
Okej om vi ser det här som ett sånt där.



`598 00:25:39,580 --> 00:25:41,580`
Typ smart token hör jag på att säga.



`599 00:25:41,580 --> 00:25:43,580`
En gammal klassisk RSA dos.



`600 00:25:43,580 --> 00:25:45,580`
Om det är en sådan.



`601 00:25:45,580 --> 00:25:47,580`
Hårdvarupryl vi har och det finns en flow.



`602 00:25:47,580 --> 00:25:49,580`
I den på något sätt.



`603 00:25:49,580 --> 00:25:51,580`
Då hade man ju.



`604 00:25:51,580 --> 00:25:53,580`
Lura oss.



`605 00:25:53,580 --> 00:25:55,580`
Och ja pass.



`606 00:25:55,580 --> 00:25:57,580`
Jag ser ju lite intressanta referenser.



`607 00:25:57,580 --> 00:25:59,580`
I vårt buzzword dokument.



`608 00:25:59,580 --> 00:26:01,580`
Tycker att det ska fortsätta.



`609 00:26:01,580 --> 00:26:03,580`
Nej men vi pratar ju.



`610 00:26:03,580 --> 00:26:05,580`
Det finns flera referenser.



`611 00:26:05,580 --> 00:26:07,580`
Här till.



`612 00:26:07,580 --> 00:26:09,580`
Javascript kod.



`613 00:26:09,580 --> 00:26:11,580`
Som har blivit utbytt på ett eller annat sätt.



`614 00:26:11,580 --> 00:26:13,580`
Ehm.



`615 00:26:13,580 --> 00:26:15,580`
Bland annat så pratar vi om.



`616 00:26:15,580 --> 00:26:17,580`
SRI alltså sub resource integrity.



`617 00:26:17,580 --> 00:26:19,580`
Som hade.



`618 00:26:19,580 --> 00:26:21,580`
Varnat för ifall en javascript kod.



`619 00:26:21,580 --> 00:26:23,580`
Hade modifierat.



`620 00:26:23,580 --> 00:26:25,580`
Det kanske man inte hade på plats då.



`621 00:26:25,580 --> 00:26:27,580`
Så nämns detta även också i.



`622 00:26:27,580 --> 00:26:29,580`
Men vi går vidare till nästa.



`623 00:26:29,580 --> 00:26:31,580`
Vi går vidare till nästa steg.



`624 00:26:31,580 --> 00:26:33,580`
För allt det ni säger tycker jag är asbra.



`625 00:26:33,580 --> 00:26:35,580`
Men nu kommer Johan in på.



`626 00:26:35,580 --> 00:26:37,580`
Egentligen steg sex skulle jag säga.



`627 00:26:37,580 --> 00:26:39,580`
Oj steg sex finns han.



`628 00:26:39,580 --> 00:26:41,580`
Vilket steg är vi på nu?



`629 00:26:41,580 --> 00:26:43,580`
Fem var detta.



`630 00:26:43,580 --> 00:26:45,580`
Men jag skulle då vilja att vi byter.



`631 00:26:45,580 --> 00:26:47,580`
Hatt nu.



`632 00:26:47,580 --> 00:26:49,580`
Så nu är vi antagonist.



`633 00:26:49,580 --> 00:26:51,580`
Om ni var angriparen.



`634 00:26:51,580 --> 00:26:53,580`
Var.



`635 00:26:53,580 --> 00:26:55,580`
Varför just Bybit.



`636 00:26:55,580 --> 00:26:57,580`
Jo för att det finns en jäkla massa pengar såklart.



`637 00:26:57,580 --> 00:26:59,580`
Och då attackerar man då dem.



`638 00:26:59,580 --> 00:27:01,580`
Men eftersom att det är 2025.



`639 00:27:01,580 --> 00:27:03,580`
Så måste det ju vara en supply chain attack.



`640 00:27:03,580 --> 00:27:05,580`
Kanske kanske.



`641 00:27:05,580 --> 00:27:07,580`
Men är det liksom opportunism.



`642 00:27:07,580 --> 00:27:09,580`
Eller är det en riktad attack.



`643 00:27:09,580 --> 00:27:11,580`
Har det här varit en lång process.



`644 00:27:11,580 --> 00:27:13,580`
Det känns ju som att den är ganska riktad.



`645 00:27:13,580 --> 00:27:15,580`
Ja det håller jag nog med om.



`646 00:27:15,580 --> 00:27:17,580`
Du nämnde ju det att dom körde med.



`647 00:27:17,580 --> 00:27:19,580`
En 3d parts mjukvara för sina wallet.



`648 00:27:19,580 --> 00:27:21,580`
Så en supply chain attack.



`649 00:27:21,580 --> 00:27:23,580`
Mot den mjukvaran.



`650 00:27:23,580 --> 00:27:25,580`
Det är typ som att du läser mina tankar nu.



`651 00:27:25,580 --> 00:27:27,580`
Vilken är då.



`652 00:27:27,580 --> 00:27:29,580`
Vilken är den svagaste länken här.



`653 00:27:29,580 --> 00:27:31,580`
I kryptobörsens infrastruktur.



`654 00:27:31,580 --> 00:27:33,580`
Och hur planerar man att tvätta.



`655 00:27:33,580 --> 00:27:35,580`
1,5 miljarder.



`656 00:27:35,580 --> 00:27:37,580`
I kryptovaluta.



`657 00:27:37,580 --> 00:27:39,580`
För er som inte har koll på kryptovaluta.



`658 00:27:39,580 --> 00:27:41,580`
Förr i tiden så var det typ.



`659 00:27:41,580 --> 00:27:43,580`
Fick man sina bitcoins så var det lugnt.



`660 00:27:43,580 --> 00:27:45,580`
Men nu för tiden.



`661 00:27:45,580 --> 00:27:47,580`
Så det är lite av en process att gömma.



`662 00:27:47,580 --> 00:27:49,580`
Det är ganska lätt.



`663 00:27:49,580 --> 00:27:51,580`
Det är ju väldigt öppet.



`664 00:27:51,580 --> 00:27:53,580`
Om man finns såklart kryptovaluta.



`665 00:27:53,580 --> 00:27:55,580`
Då är det lite svårare.



`666 00:27:55,580 --> 00:27:57,580`
Exakt att man kan tumla pengarna.



`667 00:27:57,580 --> 00:27:59,580`
Och så vidare och så vidare.



`668 00:27:59,580 --> 00:28:01,580`
Där tumblersna tar en katt.



`669 00:28:01,580 --> 00:28:03,580`
Där har inte jag någon koll på ethereum.



`670 00:28:03,580 --> 00:28:05,580`
Hur den ligger i den världen.



`671 00:28:05,580 --> 00:28:07,580`
Den är väl lika med bitcoin.



`672 00:28:07,580 --> 00:28:09,580`
Helt öppen.



`673 00:28:09,580 --> 00:28:11,580`
Den döljer inte.



`674 00:28:11,580 --> 00:28:13,580`
Du måste göra massa egen.



`675 00:28:13,580 --> 00:28:15,580`
Mixning och sånt.



`676 00:28:15,580 --> 00:28:17,580`
För att lägga till det här då.



`677 00:28:17,580 --> 00:28:19,580`
För att ge oss lite mer pretext.



`678 00:28:19,580 --> 00:28:21,580`
Pengarna var i rörelse.



`679 00:28:21,580 --> 00:28:23,580`
Inom 48 timmar.



`680 00:28:23,580 --> 00:28:25,580`
Efter det att de blev stulna.



`681 00:28:25,580 --> 00:28:27,580`
Det kräver ju också lite.



`682 00:28:27,580 --> 00:28:29,580`
Ja det kräver ju att man fan har förberett sig.



`683 00:28:29,580 --> 00:28:31,580`
Jag säger det.



`684 00:28:31,580 --> 00:28:33,580`
Nation state.



`685 00:28:33,580 --> 00:28:35,580`
Det tror jag vi kan ha för det här.



`686 00:28:35,580 --> 00:28:37,580`
Fullständigt nation state.



`687 00:28:37,580 --> 00:28:39,580`
Nej det tror jag inte.



`688 00:28:39,580 --> 00:28:41,580`
Om du hade varit en privatperson.



`689 00:28:41,580 --> 00:28:43,580`
Vilken twist.



`690 00:28:43,580 --> 00:28:45,580`
Om du är en privatperson.



`691 00:28:45,580 --> 00:28:47,580`
Och ska tvätta de här pengarna.



`692 00:28:47,580 --> 00:28:49,580`
Som är superenkla att spåra.



`693 00:28:49,580 --> 00:28:51,580`
Om du är ansträngd i dig.



`694 00:28:51,580 --> 00:28:53,580`
Det är svårt att gömma pengarna.



`695 00:28:53,580 --> 00:28:55,580`
Även via tumlare.



`696 00:28:55,580 --> 00:28:57,580`
Så om du befinner dig i ett laglydigt land.



`697 00:28:57,580 --> 00:28:59,580`
Så kommer du ha problem.



`698 00:28:59,580 --> 00:29:01,580`
Cashout blir.



`699 00:29:01,580 --> 00:29:03,580`
Det är väldigt många år snurr.



`700 00:29:03,580 --> 00:29:05,580`
Du ska hyra in för att få ut.



`701 00:29:05,580 --> 00:29:07,580`
Men om du är en skurkstat.



`702 00:29:07,580 --> 00:29:09,580`
Eller om du är.



`703 00:29:09,580 --> 00:29:11,580`
Iallafall employee av en skurkstat.



`704 00:29:11,580 --> 00:29:13,580`
Då vill jag nog.



`705 00:29:13,580 --> 00:29:15,580`
Räcka upp handen och säga.



`706 00:29:15,580 --> 00:29:17,580`
Alla medelbara grupperingar.



`707 00:29:17,580 --> 00:29:19,580`
Som är verksamma.



`708 00:29:19,580 --> 00:29:21,580`
Och revenue.



`709 00:29:21,580 --> 00:29:23,580`
De håller ju inte på med svenska kronor.



`710 00:29:23,580 --> 00:29:25,580`
Eller euro eller dollar.



`711 00:29:25,580 --> 00:29:27,580`
Det är ju kryptotungt.



`712 00:29:27,580 --> 00:29:29,580`
Så de har ju en infrastruktur för att ta ut pengar.



`713 00:29:29,580 --> 00:29:31,580`
Och de faller ju under.



`714 00:29:31,580 --> 00:29:33,580`
Många juristriktioner.



`715 00:29:33,580 --> 00:29:35,580`
De finns ju placerat på många orter i världen.



`716 00:29:35,580 --> 00:29:37,580`
Det är de.



`717 00:29:37,580 --> 00:29:39,580`
Men ganska ofta kopplade till juristriktioner.



`718 00:29:39,580 --> 00:29:41,580`
Där det inte är fullt så noga.



`719 00:29:41,580 --> 00:29:43,580`
Och då har det inte så mycket med nation state att göra.



`720 00:29:43,580 --> 00:29:45,580`
Nej det är sant.



`721 00:29:45,580 --> 00:29:47,580`
Det är inte nation state.



`722 00:29:47,580 --> 00:29:49,580`
Men är det sant att den kom tillbaka då?



`723 00:29:49,580 --> 00:29:51,580`
De är väl inte så.



`724 00:29:51,580 --> 00:29:53,580`
Nationerna är inte så.



`725 00:29:53,580 --> 00:29:55,580`
Tycker inte det är så noga det här.



`726 00:29:55,580 --> 00:29:57,580`
Eller kanske ta sin katt.



`727 00:29:57,580 --> 00:29:59,580`
Ja så kan det också vara.



`728 00:29:59,580 --> 00:30:01,580`
Återigen tillbaka till.



`729 00:30:01,580 --> 00:30:03,580`
Om vi var angripande.



`730 00:30:03,580 --> 00:30:05,580`
Vad hade vi gjort det här då?



`731 00:30:05,580 --> 00:30:07,580`
Det svåra steget i alla sådana här operationer.



`732 00:30:07,580 --> 00:30:09,580`
Är ju att få ut pengarna.



`733 00:30:09,580 --> 00:30:11,580`
Ja det är det ju.



`734 00:30:11,580 --> 00:30:13,580`
Men jag tänker mig att det är ju.



`735 00:30:13,580 --> 00:30:15,580`
Fler sex raket här ändå.



`736 00:30:15,580 --> 00:30:17,580`
Vilka hinder ser vi framför oss?



`737 00:30:17,580 --> 00:30:19,580`
Vi tar det som givet att.



`738 00:30:19,580 --> 00:30:21,580`
De använder sig av en 3D-part som är kvar.



`739 00:30:21,580 --> 00:30:23,580`
För att kontrollera sina wallets internt.



`740 00:30:23,580 --> 00:30:25,580`
Den här.



`741 00:30:25,580 --> 00:30:27,580`
Låt säga är.



`742 00:30:27,580 --> 00:30:29,580`
Ett open source projekt som ligger på Github.



`743 00:30:29,580 --> 00:30:31,580`
Det är ju ett högintressant mål.



`744 00:30:31,580 --> 00:30:33,580`
För mig att attackera som angripare.



`745 00:30:33,580 --> 00:30:35,580`
Kan jag få in en supply chain attack.



`746 00:30:35,580 --> 00:30:37,580`
På något av de sätt som vi har sett tidigare.



`747 00:30:37,580 --> 00:30:39,580`
Eller inte en flåd.



`748 00:30:39,580 --> 00:30:41,580`
Bli maintainer på något sätt.



`749 00:30:41,580 --> 00:30:43,580`
Eller någonting.



`750 00:30:43,580 --> 00:30:45,580`
Det är ju high reward.



`751 00:30:45,580 --> 00:30:47,580`
Om man kan göra det.



`752 00:30:47,580 --> 00:30:49,580`
Sen.



`753 00:30:49,580 --> 00:30:51,580`
När du väl är där inne.



`754 00:30:51,580 --> 00:30:53,580`
Så kan du ju då modifiera.



`755 00:30:53,580 --> 00:30:55,580`
Exempelvis klientens beteende.



`756 00:30:55,580 --> 00:30:57,580`
Under väldigt specifika förutsättningar.



`757 00:30:57,580 --> 00:30:59,580`
För att.



`758 00:30:59,580 --> 00:31:01,580`
Få en.



`759 00:31:01,580 --> 00:31:03,580`
Transaktion att se ut som en annan när den signeras.



`760 00:31:03,580 --> 00:31:05,580`
Men sen är ju då frågan hur du.



`761 00:31:05,580 --> 00:31:07,580`
Får ut cashen va?



`762 00:31:07,580 --> 00:31:09,580`
Exakt.



`763 00:31:09,580 --> 00:31:11,580`
Jag tänker att om man är tillräckligt duktig.



`764 00:31:11,580 --> 00:31:13,580`
Som Peter var inne på faktiskt.



`765 00:31:13,580 --> 00:31:15,580`
Världen där man exploaterar.



`766 00:31:15,580 --> 00:31:17,580`
Och specialiserar sig kanske på plånböcker.



`767 00:31:17,580 --> 00:31:19,580`
Då känns det som att man kanske har.



`768 00:31:19,580 --> 00:31:21,580`
Ett scheme klart.



`769 00:31:21,580 --> 00:31:23,580`
Men det som är intressant här.



`770 00:31:23,580 --> 00:31:25,580`
Så som jag upplever lite nu.



`771 00:31:25,580 --> 00:31:27,580`
Den svagaste länken i kryptobörsen.



`772 00:31:27,580 --> 00:31:29,580`
Är ju då signeringsförfarandet.



`773 00:31:29,580 --> 00:31:31,580`
Och plånboken egentligen.



`774 00:31:31,580 --> 00:31:33,580`
Vet vi inte egentligen.



`775 00:31:33,580 --> 00:31:35,580`
Men nyhetsartikeln antyder ju.



`776 00:31:35,580 --> 00:31:37,580`
Utan tvekan att det är något strul där.



`777 00:31:37,580 --> 00:31:39,580`
Ja exakt.



`778 00:31:39,580 --> 00:31:41,580`
Det känns inte som att det är kompromitterade personer.



`779 00:31:41,580 --> 00:31:43,580`
Nej.



`780 00:31:43,580 --> 00:31:45,580`
Det blir svårare liksom tre pers ändå.



`781 00:31:45,580 --> 00:31:47,580`
Eller hur. Det blir svårt att spearfisha dem.



`782 00:31:47,580 --> 00:31:49,580`
Till att göra det. Det är lättare att angripa.



`783 00:31:49,580 --> 00:31:51,580`
Mjukvaran de använder.



`784 00:31:51,580 --> 00:31:53,580`
Skulle jag säga.



`785 00:31:53,580 --> 00:31:55,580`
Men det kan ju vara någon form av spearfishing.



`786 00:31:55,580 --> 00:31:57,580`
Signaturlänken ska ju skickas ut i de här.



`787 00:31:57,580 --> 00:31:59,580`
Och andra sidan.



`788 00:31:59,580 --> 00:32:01,580`
Det kanske inte är spearfishing per sår.



`789 00:32:01,580 --> 00:32:03,580`
Utan det går automatiskt via systemet.



`790 00:32:03,580 --> 00:32:05,580`
Det här är ju jätteintressant ju.



`791 00:32:05,580 --> 00:32:07,580`
Det är kul.



`792 00:32:07,580 --> 00:32:09,580`
Jag tänker då att vi kör en sista runda.



`793 00:32:09,580 --> 00:32:11,580`
När vi byter hatt igen.



`794 00:32:11,580 --> 00:32:13,580`
Så den sista då.



`795 00:32:13,580 --> 00:32:15,580`
Givet är ju då.



`796 00:32:15,580 --> 00:32:17,580`
Om jag var Sison.



`797 00:32:17,580 --> 00:32:19,580`
Så då byter vi då hatten.



`798 00:32:19,580 --> 00:32:21,580`
Du är Sison på Bybit.



`799 00:32:21,580 --> 00:32:23,580`
Klockan är 03.47 på natten.



`800 00:32:23,580 --> 00:32:25,580`
Du har en dålig morgon.



`801 00:32:25,580 --> 00:32:27,580`
Och kollegan ringer och säger att 1,5 miljarder precis har lämnat plånboken.



`802 00:32:27,580 --> 00:32:29,580`
Vad gör du?



`803 00:32:29,580 --> 00:32:31,580`
Första timmen.



`804 00:32:31,580 --> 00:32:33,580`
Hoppa från nästa fönster.



`805 00:32:33,580 --> 00:32:35,580`
Vad stänger du av liksom?



`806 00:32:35,580 --> 00:32:37,580`
Jag stänger allt.



`807 00:32:37,580 --> 00:32:39,580`
Men så här.



`808 00:32:39,580 --> 00:32:41,580`
Det här är ju en PR fråga också.



`809 00:32:41,580 --> 00:32:43,580`
Precis.



`810 00:32:43,580 --> 00:32:45,580`
Inom någon timme så var de på Twitch och informerade kunderna.



`811 00:32:45,580 --> 00:32:47,580`
Det är ju faktiskt riktigt smart.



`812 00:32:47,580 --> 00:32:49,580`
Och det de måste se också är ju.



`813 00:32:49,580 --> 00:32:51,580`
Vi kan se att det här drabbade.



`814 00:32:51,580 --> 00:32:53,580`
En av våra interna överföringar.



`815 00:32:53,580 --> 00:32:55,580`
Som krävde våra tre signatursystem.



`816 00:32:55,580 --> 00:32:57,580`
Är det här potentiellt något.



`817 00:32:57,580 --> 00:32:59,580`
Som drabbar våra kunder också.



`818 00:32:59,580 --> 00:33:01,580`
I deras privata transaktioner.



`819 00:33:01,580 --> 00:33:03,580`
Det känns ju ganska centralt.



`820 00:33:03,580 --> 00:33:05,580`
Visst var det så att de hade blandat in advokater.



`821 00:33:05,580 --> 00:33:07,580`
Med en gång också.



`822 00:33:07,580 --> 00:33:09,580`
PR mässigt.



`823 00:33:09,580 --> 00:33:11,580`
Så har de gjort rätt här.



`824 00:33:11,580 --> 00:33:13,580`
De går ut supertidigt på Twitch.



`825 00:33:13,580 --> 00:33:15,580`
Som förmodligen är rätt kanal för deras kundsegment.



`826 00:33:15,580 --> 00:33:17,580`
Ja och även kommunicera då.



`827 00:33:17,580 --> 00:33:19,580`
Börsvärde och att det kommer ju falla som en sten.



`828 00:33:19,580 --> 00:33:21,580`
Tänker man sig när det öppnar.



`829 00:33:21,580 --> 00:33:23,580`
Och att vi är solventa.



`830 00:33:23,580 --> 00:33:25,580`
De har verkligen skött sin PR här.



`831 00:33:25,580 --> 00:33:27,580`
Du ser väl till att dina cold wallets.



`832 00:33:27,580 --> 00:33:29,580`
Faktiskt är cold wallets.



`833 00:33:29,580 --> 00:33:31,580`
Ganska tydligt.



`834 00:33:31,580 --> 00:33:33,580`
Sluta strömsätta.



`835 00:33:33,580 --> 00:33:35,580`
De hårdvaruenheterna.



`836 00:33:35,580 --> 00:33:37,580`
Och när du gör chatten på dem.



`837 00:33:37,580 --> 00:33:39,580`
Följ korrekt chatten.



`838 00:33:39,580 --> 00:33:41,580`
Du vet ju inte ens om det är dina hårdvaruenheter.



`839 00:33:41,580 --> 00:33:43,580`
Du vet ju inte ens om det är dina hårdvaruenheter.



`840 00:33:43,580 --> 00:33:45,580`
Du vet ju inte ens om det är dina hårdvaruenheter.



`841 00:33:45,580 --> 00:33:47,580`
Jag hade fan stängt alla tjänster.



`842 00:33:47,580 --> 00:33:49,580`
Banken sluta processa data. Punkt.



`843 00:33:49,580 --> 00:33:51,580`
Eftersom vi inte vet.



`844 00:33:51,580 --> 00:33:53,580`
Vi har ingen aning.



`845 00:33:53,580 --> 00:33:55,580`
Vi kan ju inte validera interna transaktioner.



`846 00:33:55,580 --> 00:33:57,580`
Dra sladden och behåll loggarna.



`847 00:33:57,580 --> 00:33:59,580`
Ta bort internetsladden men behåll sladden.



`848 00:33:59,580 --> 00:34:01,580`
Det är svårt ju.



`849 00:34:01,580 --> 00:34:03,580`
Men jag tycker också att han har gjort en bra.



`850 00:34:03,580 --> 00:34:05,580`
Sen vet vi ju inte.



`851 00:34:05,580 --> 00:34:07,580`
Om han stängde ner grejer.



`852 00:34:07,580 --> 00:34:09,580`
Varifrån skedde signeringarna?



`853 00:34:09,580 --> 00:34:11,580`
Varifrån skedde signeringarna?



`854 00:34:11,580 --> 00:34:13,580`
Är det deras laptops?



`855 00:34:13,580 --> 00:34:15,580`
Kan det vara dem som är drabbade?



`856 00:34:15,580 --> 00:34:17,580`
Ingen data på det alls.



`857 00:34:17,580 --> 00:34:19,580`
Men jag tycker också att det är coolt.



`858 00:34:19,580 --> 00:34:21,580`
Att man går ut på Twitch så snabbt.



`859 00:34:21,580 --> 00:34:23,580`
Och bara kommunicerar krisen.



`860 00:34:23,580 --> 00:34:25,580`
Oavsett om den är bra eller dålig.



`861 00:34:25,580 --> 00:34:27,580`
Om det här är sant det som står här.



`862 00:34:27,580 --> 00:34:29,580`
Inom timmar.



`863 00:34:29,580 --> 00:34:31,580`
Inom timmar gick live.



`864 00:34:31,580 --> 00:34:33,580`
Att vdn går live inom timmar.



`865 00:34:33,580 --> 00:34:35,580`
Att vdn går live inom timmar.



`866 00:34:35,580 --> 00:34:37,580`
Det är kudos.



`867 00:34:37,580 --> 00:34:39,580`
Det är inte alla organisationer som ens fattar.



`868 00:34:39,580 --> 00:34:41,580`
Vad som har hänt på den tiden.



`869 00:34:41,580 --> 00:34:43,580`
Och kopplar in förhoppningsvis.



`870 00:34:43,580 --> 00:34:45,580`
Betrodda tredjeparts.



`871 00:34:45,580 --> 00:34:47,580`
De säger ju att det var både it-säkerhetsbolag.



`872 00:34:47,580 --> 00:34:49,580`
Vuxna och annat.



`873 00:34:49,580 --> 00:34:51,580`
Exakt.



`874 00:34:51,580 --> 00:34:53,580`
Och även kryptobolag som börjar spara pengar direkt.



`875 00:34:53,580 --> 00:34:55,580`
Men om de är en sån här stor.



`876 00:34:55,580 --> 00:34:57,580`
Kryptobank så.



`877 00:34:57,580 --> 00:34:59,580`
Har de väl förmodligen.



`878 00:34:59,580 --> 00:35:01,580`
Tränat det här scenariot.



`879 00:35:01,580 --> 00:35:03,580`
Alltså inte.



`880 00:35:03,580 --> 00:35:05,580`
Men att de är stora på pengar betyder ju inte.



`881 00:35:05,580 --> 00:35:07,580`
Alltid att de är en stor organisation.



`882 00:35:07,580 --> 00:35:09,580`
Det är ju.



`883 00:35:09,580 --> 00:35:11,580`
Vad de borde ha.



`884 00:35:11,580 --> 00:35:13,580`
Är ju.



`885 00:35:13,580 --> 00:35:15,580`
Att vdn är på.



`886 00:35:15,580 --> 00:35:17,580`
Helt plötsligt.



`887 00:35:17,580 --> 00:35:19,580`
De har ju en hot wallet.



`888 00:35:19,580 --> 00:35:21,580`
Och så har de väl förmodligen en då.



`889 00:35:21,580 --> 00:35:23,580`
Som är då den större.



`890 00:35:23,580 --> 00:35:25,580`
Lite svalare walleten.



`891 00:35:25,580 --> 00:35:27,580`
Och ett antal verkligen cool på riktigt wallet.



`892 00:35:27,580 --> 00:35:29,580`
Så.



`893 00:35:29,580 --> 00:35:31,580`
De bör ju ha tränat.



`894 00:35:31,580 --> 00:35:33,580`
Scenariot.



`895 00:35:33,580 --> 00:35:35,580`
Massa pengar försvinner från vår chili wallet.



`896 00:35:35,580 --> 00:35:37,580`
Och vad gör vi då?



`897 00:35:37,580 --> 00:35:39,580`
Alltså gissningsvis.



`898 00:35:39,580 --> 00:35:41,580`
I samma stund som.



`899 00:35:41,580 --> 00:35:43,580`
Egentligen i samma stund som.



`900 00:35:43,580 --> 00:35:45,580`
Den konstiga transaktionen noteras.



`901 00:35:45,580 --> 00:35:47,580`
Så ringer man.



`902 00:35:47,580 --> 00:35:49,580`
Den kontaktpersonen man har och.



`903 00:35:49,580 --> 00:35:51,580`
Ja vad det nu är för.



`904 00:35:51,580 --> 00:35:53,580`
Stor forensik gäng man har.



`905 00:35:53,580 --> 00:35:55,580`
Börja välja in.



`906 00:35:55,580 --> 00:35:57,580`
Utredare.



`907 00:35:57,580 --> 00:35:59,580`
Riktigt riktigt fort.



`908 00:35:59,580 --> 00:36:01,580`
Om de har gjort sin hemmeläxa.



`909 00:36:01,580 --> 00:36:03,580`
De måste ju också ha någon slags övervakning.



`910 00:36:03,580 --> 00:36:05,580`
Det satte jag också för.



`911 00:36:05,580 --> 00:36:07,580`
Det är ju inte säkert.



`912 00:36:07,580 --> 00:36:09,580`
Under förutsättning att.



`913 00:36:09,580 --> 00:36:11,580`
Allting sker i samma system då.



`914 00:36:11,580 --> 00:36:13,580`
Coolt jag tycker vi ser bra saker.



`915 00:36:13,580 --> 00:36:15,580`
Jag antar att folk på internet.



`916 00:36:15,580 --> 00:36:17,580`
Märker det här direkt.



`917 00:36:17,580 --> 00:36:19,580`
Så kan det också vara.



`918 00:36:19,580 --> 00:36:21,580`
Eftersom det är publika.



`919 00:36:21,580 --> 00:36:23,580`
Det försvann 1,5.



`920 00:36:23,580 --> 00:36:25,580`
Alltså vad står det.



`921 00:36:25,580 --> 00:36:27,580`
1,5 miljoner.



`922 00:36:27,580 --> 00:36:29,580`
Det måste ju vara en.



`923 00:36:29,580 --> 00:36:31,580`
Väldigt ovanlig händelse.



`924 00:36:31,580 --> 00:36:33,580`
Det är som.



`925 00:36:33,580 --> 00:36:35,580`
2,30 i nätet tappar hatch liksom.



`926 00:36:35,580 --> 00:36:37,580`
Då är det många som reagerar.



`927 00:36:37,580 --> 00:36:39,580`
Mycket som går sönder.



`928 00:36:39,580 --> 00:36:41,580`
Men okej jag tänker att vi pausar där.



`929 00:36:41,580 --> 00:36:43,580`
Och nu tänker jag.



`930 00:36:43,580 --> 00:36:45,580`
Att vi går in i fasen.



`931 00:36:45,580 --> 00:36:47,580`
Där vi tittar på facit.



`932 00:36:47,580 --> 00:36:49,580`
Nej men det var en C-collection i en P&P.



`933 00:36:49,580 --> 00:36:51,580`
Det hade varit roligt.



`934 00:36:51,580 --> 00:36:53,580`
Så det har jag ändå haft.



`935 00:36:53,580 --> 00:36:55,580`
Nera teorier och jag tycker.



`936 00:36:55,580 --> 00:36:57,580`
Eller vi har haft några teorier.



`937 00:36:57,580 --> 00:36:59,580`
Jag tycker de har varit bra.



`938 00:36:59,580 --> 00:37:01,580`
Men kollar vi hur nära målet.



`939 00:37:01,580 --> 00:37:03,580`
Okej.



`940 00:37:03,580 --> 00:37:05,580`
Jag tänker att jag redogör.



`941 00:37:05,580 --> 00:37:07,580`
Vad som faktiskt hände.



`942 00:37:07,580 --> 00:37:09,580`
Så det är den korrekta attack kedjan.



`943 00:37:11,580 --> 00:37:13,580`
Attacken började inte.



`944 00:37:13,580 --> 00:37:15,580`
Hos Bybit.



`945 00:37:15,580 --> 00:37:17,580`
En anställd på.



`946 00:37:17,580 --> 00:37:19,580`
Safewallet.



`947 00:37:19,580 --> 00:37:21,580`
Leverantörerna av Bitbys.



`948 00:37:21,580 --> 00:37:23,580`
Plånboksprogramvara kontaktas.



`949 00:37:23,580 --> 00:37:25,580`
Via vad som ser ut som en legitimt jobberbjudande.



`950 00:37:25,580 --> 00:37:27,580`
Som del av.



`951 00:37:27,580 --> 00:37:29,580`
En teknisk intervjuprocess.



`952 00:37:29,580 --> 00:37:31,580`
Ombudspersonen laddar ner och kör ett kodprojekt.



`953 00:37:31,580 --> 00:37:33,580`
Från.



`954 00:37:33,580 --> 00:37:35,580`
Det är nära där.



`955 00:37:35,580 --> 00:37:37,580`
Projektet heter.



`956 00:37:37,580 --> 00:37:39,580`
MC Based Stock Invest Simulator Main.



`957 00:37:39,580 --> 00:37:41,580`
Detta är väldigt likt.



`958 00:37:41,580 --> 00:37:43,580`
En grej vi snackade om för bara någon månad sedan.



`959 00:37:43,580 --> 00:37:45,580`
Det är ett malware.



`960 00:37:45,580 --> 00:37:47,580`
Som installerar sig tyst.



`961 00:37:47,580 --> 00:37:49,580`
På utvecklarens MacBook.



`962 00:37:49,580 --> 00:37:51,580`
Själv aktiva AVS session tokens.



`963 00:37:51,580 --> 00:37:53,580`
Alltså tillfälliga åtnycklar.



`964 00:37:53,580 --> 00:37:55,580`
Till AVS infrastruktur.



`965 00:37:55,580 --> 00:37:57,580`
Avgörande här då.



`966 00:37:57,580 --> 00:37:59,580`
Det är att det är sessions tokens.



`967 00:37:59,580 --> 00:38:01,580`
Och sessions token i AVS.



`968 00:38:01,580 --> 00:38:03,580`
Som kringgår all form av MFA.



`969 00:38:03,580 --> 00:38:05,580`
För de är ju klara liksom.



`970 00:38:05,580 --> 00:38:07,580`
Exakt.



`971 00:38:07,580 --> 00:38:09,580`
Men de har ofta begränsat giltighet.



`972 00:38:09,580 --> 00:38:11,580`
Beroende på vad det är.



`973 00:38:11,580 --> 00:38:13,580`
Men de är i vart fall åtade då.



`974 00:38:13,580 --> 00:38:15,580`
Och det här hände då.



`975 00:38:15,580 --> 00:38:17,580`
17 dagar innan attacken.



`976 00:38:17,580 --> 00:38:19,580`
Japp.



`977 00:38:19,580 --> 00:38:21,580`
14-9 februari.



`978 00:38:21,580 --> 00:38:23,580`
Det är nu dwell time då.



`979 00:38:23,580 --> 00:38:25,580`
Det är nu det händer.



`980 00:38:25,580 --> 00:38:27,580`
Angriparna är inne i Safe Wallets infrastruktur.



`981 00:38:27,580 --> 00:38:29,580`
Med de stulna tokensen.



`982 00:38:29,580 --> 00:38:31,580`
Det hittade en S3 bucket.



`983 00:38:31,580 --> 00:38:33,580`
Där Safe Wallets JavaScript kod.



`984 00:38:33,580 --> 00:38:35,580`
Det som Johan var inne på.



`985 00:38:35,580 --> 00:38:37,580`
För webbgränssittet lagras.



`986 00:38:37,580 --> 00:38:39,580`
Den 19 februari.



`987 00:38:39,580 --> 00:38:41,580`
Två dagar innan stölden.



`988 00:38:41,580 --> 00:38:43,580`
Byter de ut de legitima JavaScript filerna.



`989 00:38:43,580 --> 00:38:45,580`
Mot en modifierad version.



`990 00:38:45,580 --> 00:38:47,580`
Koden är identiskt med ordinariet.



`991 00:38:47,580 --> 00:38:49,580`
Förutom ett specifikt scenario.



`992 00:38:49,580 --> 00:38:51,580`
När en Bybit-transaktion.



`993 00:38:51,580 --> 00:38:53,580`
Av en viss form signeras.



`994 00:38:53,580 --> 00:38:55,580`
Manipuleras koden.



`995 00:38:55,580 --> 00:38:57,580`
Vad användaren ser på skärmen.



`996 00:38:57,580 --> 00:38:59,580`
Ja men det var ju det vi var ute på.



`997 00:38:59,580 --> 00:39:01,580`
Så det är väldigt bra.



`998 00:39:01,580 --> 00:39:03,580`
Och då 21 februari.



`999 00:39:03,580 --> 00:39:05,580`
Dagen för stölden.



`1000 00:39:05,580 --> 00:39:07,580`
Tre signerande godkänner.



`1001 00:39:07,580 --> 00:39:09,580`
Utan att veta om vad de signerar.



`1002 00:39:09,580 --> 00:39:11,580`
Bybit-signerarna.



`1003 00:39:11,580 --> 00:39:13,580`
Inklusive vdn Benzao.



`1004 00:39:13,580 --> 00:39:15,580`
Granskar och godkänner transaktionen individuellt.



`1005 00:39:15,580 --> 00:39:17,580`
Det ser rätt.



`1006 00:39:17,580 --> 00:39:19,580`
Det ser rätt mottagandres.



`1007 00:39:19,580 --> 00:39:21,580`
Rätt belopp.



`1008 00:39:21,580 --> 00:39:23,580`
Rätt internetikett.



`1009 00:39:23,580 --> 00:39:25,580`
Det signerar faktiskt en transaktion.



`1010 00:39:25,580 --> 00:39:27,580`
Som överlåter ägandeskapet.



`1011 00:39:27,580 --> 00:39:29,580`
Av hela plånbokets kontrakt.



`1012 00:39:29,580 --> 00:39:31,580`
Angriparens adrett.



`1013 00:39:31,580 --> 00:39:33,580`
Multisignersystemet fungerar exakt som.



`1014 00:39:33,580 --> 00:39:35,580`
Det var designat.



`1015 00:39:35,580 --> 00:39:37,580`
Alla tre signerade.



`1016 00:39:37,580 --> 00:39:39,580`
Det signerade fel sak.



`1017 00:39:39,580 --> 00:39:41,580`
Inom minuter var 1,5 miljarder dollar borta.



`1018 00:39:41,580 --> 00:39:43,580`
De tar hela plånboken.



`1019 00:39:43,580 --> 00:39:45,580`
De ändrar ägandeskapet.



`1020 00:39:45,580 --> 00:39:47,580`
Istället för att byta transaktion.



`1021 00:39:47,580 --> 00:39:49,580`
Eller ja.



`1022 00:39:49,580 --> 00:39:51,580`
Och summeringen på det här då.



`1023 00:39:51,580 --> 00:39:53,580`
Ingen nyckel komplementeras.



`1024 00:39:53,580 --> 00:39:55,580`
Inga protokoll bröts.



`1025 00:39:55,580 --> 00:39:57,580`
Angriparen manipulerar vad signerarna såg.



`1026 00:39:57,580 --> 00:39:59,580`
Inte vad som faktiskt signerades.



`1027 00:39:59,580 --> 00:40:01,580`
Vi visste inte att Safe Wallets



`1028 00:40:01,580 --> 00:40:03,580`
Infrastruktur var ägd egentligen.



`1029 00:40:03,580 --> 00:40:05,580`
Ingen subresource



`1030 00:40:05,580 --> 00:40:07,580`
Integrity control som vi var inne på.



`1031 00:40:07,580 --> 00:40:09,580`
Fanns på plats för att verifiera att



`1032 00:40:09,580 --> 00:40:11,580`
Javascript-filen var omodifierad.



`1033 00:40:11,580 --> 00:40:13,580`
Du kan jämföra det med att



`1034 00:40:13,580 --> 00:40:15,580`
någon modifierar



`1035 00:40:15,580 --> 00:40:17,580`
frontendkoden för BankID.



`1036 00:40:17,580 --> 00:40:19,580`
Egentligen.



`1037 00:40:19,580 --> 00:40:21,580`
Så att när du står



`1038 00:40:21,580 --> 00:40:23,580`
Nu för du över 5 kronor till Peter.



`1039 00:40:23,580 --> 00:40:25,580`
Men i verkligheten så skickar jag 50 000 till Johan.



`1040 00:40:25,580 --> 00:40:27,580`
Precis. Eller nu.



`1041 00:40:27,580 --> 00:40:29,580`
Då lade du till en ny användare på ditt bankkonto.



`1042 00:40:29,580 --> 00:40:31,580`
Får någon av oss koll på den här



`1043 00:40:31,580 --> 00:40:33,580`
SRI hur det funkar?



`1044 00:40:33,580 --> 00:40:35,580`
Jag tänker väl att det är



`1045 00:40:35,580 --> 00:40:37,580`
Som att signera assets.



`1046 00:40:37,580 --> 00:40:39,580`
Det vill säga att du får en summa.



`1047 00:40:39,580 --> 00:40:41,580`
En kryptohash på innehåll.



`1048 00:40:41,580 --> 00:40:43,580`
Så hade man kört med SRI så hade det varit



`1049 00:40:43,580 --> 00:40:45,580`
Då hade inte summa matchat.



`1050 00:40:45,580 --> 00:40:47,580`
Då hade det varit en teknik



`1051 00:40:47,580 --> 00:40:49,580`
Teknik



`1052 00:40:49,580 --> 00:40:51,580`
Alltså en teknisk kontroll man behöver kringgå med.



`1053 00:40:51,580 --> 00:40:53,580`
Men jag satt och funderade på.



`1054 00:40:53,580 --> 00:40:55,580`
Hur ser signeringsmjukvaran ut?



`1055 00:40:55,580 --> 00:40:57,580`
Är det en browser-app



`1056 00:40:57,580 --> 00:40:59,580`
Är det javascript som snurrar i browsern?



`1057 00:40:59,580 --> 00:41:01,580`
Är det så de signerar?



`1058 00:41:01,580 --> 00:41:03,580`
Det kan ju vara mobil också.



`1059 00:41:03,580 --> 00:41:05,580`
Eller att det är en fröt.



`1060 00:41:05,580 --> 00:41:07,580`
Det är



`1061 00:41:07,580 --> 00:41:09,580`
Entropit eller det som ska signeras



`1062 00:41:09,580 --> 00:41:11,580`
Kommer sedan behöva köras igenom



`1063 00:41:11,580 --> 00:41:13,580`
En plånbok eller vad det nu är.



`1064 00:41:13,580 --> 00:41:15,580`
Det som kommer tillbaka sen blir innehållet.



`1065 00:41:15,580 --> 00:41:17,580`
Alltså man



`1066 00:41:17,580 --> 00:41:19,580`
Ska signera något.



`1067 00:41:19,580 --> 00:41:21,580`
Det är väl att de byter ut vad det är för transaktion



`1068 00:41:21,580 --> 00:41:23,580`
Som egentligen signeras.



`1069 00:41:23,580 --> 00:41:25,580`
Istället för att skicka den här.



`1070 00:41:25,580 --> 00:41:27,580`
Det var kontext när jag var ute.



`1071 00:41:27,580 --> 00:41:29,580`
Vi är i browsern nu när vi gör de här.



`1072 00:41:29,580 --> 00:41:31,580`
Det vill säga det javascriptet.



`1073 00:41:31,580 --> 00:41:33,580`
Jag tänker nog att vi är i browsern.



`1074 00:41:33,580 --> 00:41:35,580`
Och i en device.



`1075 00:41:35,580 --> 00:41:37,580`
I en appliance säkert.



`1076 00:41:37,580 --> 00:41:39,580`
Och de har ju möjlighet att kontrollera.



`1077 00:41:39,580 --> 00:41:41,580`
Du tror att det finns en dedikerad



`1078 00:41:41,580 --> 00:41:43,580`
Hårdvaruappliance som går till den här



`1079 00:41:43,580 --> 00:41:45,580`
Estribucket och hämtar javascriptet.



`1080 00:41:45,580 --> 00:41:47,580`
Det spelar ju ingen roll.



`1081 00:41:47,580 --> 00:41:49,580`
Jag försöker bara förstå.



`1082 00:41:49,580 --> 00:41:51,580`
Om det bara är en ren webapp.



`1083 00:41:51,580 --> 00:41:53,580`
Jag blir lite nervös om



`1084 00:41:53,580 --> 00:41:55,580`
1,5 miljarder hanteras



`1085 00:41:55,580 --> 00:41:57,580`
I browsern.



`1086 00:41:57,580 --> 00:41:59,580`
Men det är ju så att det är en



`1087 00:41:59,580 --> 00:42:01,580`
Egen kod man kör.



`1088 00:42:01,580 --> 00:42:03,580`
Men samtidigt.



`1089 00:42:03,580 --> 00:42:05,580`
Man köper det på kran.



`1090 00:42:05,580 --> 00:42:07,580`
Precis och det är ju deras wallet tjänst.



`1091 00:42:07,580 --> 00:42:09,580`
Det är ju per definition deras kod.



`1092 00:42:09,580 --> 00:42:11,580`
För det låter ju då som att



`1093 00:42:11,580 --> 00:42:13,580`
Den här walleten



`1094 00:42:13,580 --> 00:42:15,580`
Inte är särskilt cold.



`1095 00:42:15,580 --> 00:42:17,580`
Nej det här är ju jämförande med



`1096 00:42:17,580 --> 00:42:19,580`
Att jag loggar in på banken.



`1097 00:42:19,580 --> 00:42:21,580`
Och någon strular med



`1098 00:42:21,580 --> 00:42:23,580`
Mitt webbinterface liksom.



`1099 00:42:23,580 --> 00:42:25,580`
Så återigen jag tror att jag för över



`1100 00:42:25,580 --> 00:42:27,580`
Fem spänn till Peter.



`1101 00:42:27,580 --> 00:42:29,580`
Men istället är det



`1102 00:42:29,580 --> 00:42:31,580`
Johan som tar alla mina pengar.



`1103 00:42:31,580 --> 00:42:33,580`
Egentligen vad vi är



`1104 00:42:33,580 --> 00:42:35,580`
Egentligen ute efter det är ju att



`1105 00:42:35,580 --> 00:42:37,580`
Cold wallet är inte kall.



`1106 00:42:37,580 --> 00:42:39,580`
Utan vad de i praktiken menar med kall



`1107 00:42:39,580 --> 00:42:41,580`
Är att den kräver den här



`1108 00:42:41,580 --> 00:42:43,580`
Tre människor



`1109 00:42:43,580 --> 00:42:45,580`
Ett testflöde.



`1110 00:42:45,580 --> 00:42:47,580`
Den är ju på sin höjd chili som du säger.



`1111 00:42:47,580 --> 00:42:49,580`
Chili wallet är bättre term än cold wallet.



`1112 00:42:49,580 --> 00:42:51,580`
Jag hade ju velat se att



`1113 00:42:51,580 --> 00:42:53,580`
Om du nu har en wallet



`1114 00:42:53,580 --> 00:42:55,580`
Som ens ger dig möjligheten att föra över



`1115 00:42:55,580 --> 00:42:57,580`
Den här typ mängden cash.



`1116 00:42:57,580 --> 00:42:59,580`
Då skulle jag vilja ha den



`1117 00:42:59,580 --> 00:43:01,580`
Fysiskt separerad från nätet.



`1118 00:43:01,580 --> 00:43:03,580`
Alltså du ska behöva gå och plugga in en pryl.



`1119 00:43:03,580 --> 00:43:05,580`
För att godkänna en sån transaktion.



`1120 00:43:05,580 --> 00:43:07,580`
Men det hade ju inte hjälpt i det här fallet.



`1121 00:43:07,580 --> 00:43:09,580`
Nästa grej då är ju att om vi hade haft den



`1122 00:43:09,580 --> 00:43:11,580`
På en fysisk hosem eller någonting.



`1123 00:43:11,580 --> 00:43:13,580`
Den ska ju vara brandskyddad



`1124 00:43:13,580 --> 00:43:15,580`
Och sånt också liksom.



`1125 00:43:15,580 --> 00:43:17,580`
Men det kanske det är värt att ha den



`1126 00:43:17,580 --> 00:43:19,580`
Om det är 1,5 miljarder.



`1127 00:43:19,580 --> 00:43:21,580`
Om vi vänder på det.



`1128 00:43:21,580 --> 00:43:23,580`
Nu får du jobbet Johan att designa den här lösningen.



`1129 00:43:23,580 --> 00:43:25,580`
Det är ändå en bank.



`1130 00:43:25,580 --> 00:43:27,580`
För tidigt.



`1131 00:43:27,580 --> 00:43:29,580`
Men jag tycker det här har varit svin.



`1132 00:43:29,580 --> 00:43:31,580`
Bra diskussion so far.



`1133 00:43:31,580 --> 00:43:33,580`
Så jag tänker att



`1134 00:43:33,580 --> 00:43:35,580`
Vi går vidare till nästa steg.



`1135 00:43:35,580 --> 00:43:37,580`
I facit.



`1136 00:43:37,580 --> 00:43:39,580`
Det är fortfarande steg åtta.



`1137 00:43:39,580 --> 00:43:41,580`
Och då är ju vem som låg bakom det här.



`1138 00:43:41,580 --> 00:43:43,580`
Bängt.



`1139 00:43:43,580 --> 00:43:45,580`
Och då vet vi ju redan



`1140 00:43:45,580 --> 00:43:47,580`
För vi har ju läst nyhets...



`1141 00:43:47,580 --> 00:43:49,580`
Det hade varit 1,5 miljarder.



`1142 00:43:49,580 --> 00:43:51,580`
Det kanske jag hade.



`1143 00:43:51,580 --> 00:43:53,580`
Men FBI



`1144 00:43:53,580 --> 00:43:55,580`
Och flera sökerhetsföretag



`1145 00:43:55,580 --> 00:43:57,580`
Bland annat Archime Intelligence



`1146 00:43:57,580 --> 00:43:59,580`
XBT, Mandiant



`1147 00:43:59,580 --> 00:44:01,580`
Identifierade snabbt ett mönster



`1148 00:44:01,580 --> 00:44:03,580`
Utöver det stulna tillgångarna tvättades.



`1149 00:44:03,580 --> 00:44:05,580`
Hastigheten, strukturen, de specifika mixers



`1150 00:44:05,580 --> 00:44:07,580`
Och bridge-tjänsterna som användes



`1151 00:44:07,580 --> 00:44:09,580`
Matchades en välkänd profil.



`1152 00:44:09,580 --> 00:44:11,580`
Och det är alltså



`1153 00:44:11,580 --> 00:44:13,580`
Trader Trater heter



`1154 00:44:13,580 --> 00:44:15,580`
Den här gruppen



`1155 00:44:15,580 --> 00:44:17,580`
Och det skulle tydligen vara en underkategori till Lazarus Group.



`1156 00:44:17,580 --> 00:44:19,580`
Statssponsrad Nordkorea



`1157 00:44:19,580 --> 00:44:21,580`
Statssponsrad hackergrupp.



`1158 00:44:21,580 --> 00:44:23,580`
Samma hotaktör



`1159 00:44:23,580 --> 00:44:25,580`
Låg även bakom Ronin Network



`1160 00:44:25,580 --> 00:44:27,580`
2022



`1161 00:44:27,580 --> 00:44:29,580`
Harmony Horizon Bridge 2022 också



`1162 00:44:29,580 --> 00:44:31,580`
Och bara för att vi ska få lite kontext då



`1163 00:44:31,580 --> 00:44:33,580`
Så Ronin Network



`1164 00:44:33,580 --> 00:44:35,580`
2022, där kom de undan med



`1165 00:44:35,580 --> 00:44:37,580`
625 miljoner dollar



`1166 00:44:37,580 --> 00:44:39,580`
Harmony Horizon-bryggan



`1167 00:44:39,580 --> 00:44:41,580`
100 miljoner dollar



`1168 00:44:41,580 --> 00:44:43,580`
Atomic Wallet 35 miljoner dollar



`1169 00:44:43,580 --> 00:44:45,580`
Undrar du hur stor andel av Nordkoreas



`1170 00:44:45,580 --> 00:44:47,580`
Statsbudget är?



`1171 00:44:47,580 --> 00:44:49,580`
Nordkorea har under



`1172 00:44:49,580 --> 00:44:51,580`
En flerårsperiod



`1173 00:44:51,580 --> 00:44:53,580`
Stulit uppskattningsvis



`1174 00:44:53,580 --> 00:44:55,580`
Vi har inga specifika



`1175 00:44:55,580 --> 00:44:57,580`
Detaljer på detta



`1176 00:44:57,580 --> 00:44:59,580`
3-6 miljarder i kryptovaluta



`1177 00:44:59,580 --> 00:45:01,580`
Pengarna finansierar landets



`1178 00:45:01,580 --> 00:45:03,580`
Vapenutveckling inklusive missilprogrammet



`1179 00:45:03,580 --> 00:45:05,580`
Jobbannonsen



`1180 00:45:05,580 --> 00:45:07,580`
Som de använder i den här kampanjen



`1181 00:45:07,580 --> 00:45:09,580`
Kallades för Dreamjob



`1182 00:45:09,580 --> 00:45:11,580`
Och hör och häpna



`1183 00:45:11,580 --> 00:45:13,580`
Har varit aktiv sedan 2019



`1184 00:45:13,580 --> 00:45:15,580`
Riktat specifikt mot krypto



`1185 00:45:15,580 --> 00:45:17,580`
Och techbranschen



`1186 00:45:17,580 --> 00:45:19,580`
Men jag tänker



`1187 00:45:19,580 --> 00:45:21,580`
Det avsnittet har pågått ganska länge



`1188 00:45:21,580 --> 00:45:23,580`
Så jag tänker att vi slår på



`1189 00:45:23,580 --> 00:45:25,580`
En liten god twist på det här då



`1190 00:45:25,580 --> 00:45:27,580`
För vi har faktiskt



`1191 00:45:27,580 --> 00:45:29,580`
Sagt väldigt många bra saker här nu



`1192 00:45:31,580 --> 00:45:33,580`
Bybit hade ju



`1193 00:45:33,580 --> 00:45:35,580`
Ett ganska robust system ändå



`1194 00:45:35,580 --> 00:45:37,580`
Multisignatur



`1195 00:45:37,580 --> 00:45:39,580`
Med cold wallets



`1196 00:45:39,580 --> 00:45:41,580`
Med separata signerare



`1197 00:45:41,580 --> 00:45:43,580`
Och det var ju egentligen ingenting



`1198 00:45:43,580 --> 00:45:45,580`
I signatursystemet



`1199 00:45:45,580 --> 00:45:47,580`
Förfarandet



`1200 00:45:47,580 --> 00:45:49,580`
Som bröts



`1201 00:45:49,580 --> 00:45:51,580`
Det var ju inte protokollet som åkte på det



`1202 00:45:51,580 --> 00:45:53,580`
För det som hände egentligen var ju att den här



`1203 00:45:53,580 --> 00:45:55,580`
Stackars utvecklarens



`1204 00:45:55,580 --> 00:45:57,580`
Macbook pro blev liksom dödsägd



`1205 00:45:57,580 --> 00:45:59,580`
17 dagar innan stölden



`1206 00:45:59,580 --> 00:46:01,580`
Och



`1207 00:46:01,580 --> 00:46:03,580`
Och de enda angriparna



`1208 00:46:03,580 --> 00:46:05,580`
Gjorde var ju att de



`1209 00:46:05,580 --> 00:46:07,580`
Ja alltså han hoppade in i ett fejkat



`1210 00:46:07,580 --> 00:46:09,580`
Github repo och sen så väntade de



`1211 00:46:09,580 --> 00:46:11,580`
Tålmodigt i 17 dagar



`1212 00:46:11,580 --> 00:46:13,580`
Och sen körde de



`1213 00:46:13,580 --> 00:46:15,580`
Frågan är om de väntar



`1214 00:46:15,580 --> 00:46:17,580`
De måste ju suttit och tänkt under den perioden och grävt runt



`1215 00:46:17,580 --> 00:46:19,580`
Försöka se hur det funkar



`1216 00:46:19,580 --> 00:46:21,580`
Ja men hittat SD-bucket



`1217 00:46:21,580 --> 00:46:23,580`
Ja men exakt



`1218 00:46:23,580 --> 00:46:25,580`
Men tålamod det kommer man ju inte från



`1219 00:46:25,580 --> 00:46:27,580`
Förmodligen rätt mycket jobb under den perioden



`1220 00:46:27,580 --> 00:46:29,580`
De sov nog inte så mycket på de dagarna



`1221 00:46:29,580 --> 00:46:31,580`
Men för att summera så är det liksom



`1222 00:46:31,580 --> 00:46:33,580`
En fejkad jobbannons



`1223 00:46:33,580 --> 00:46:35,580`
Ett falskt github repo med malware



`1224 00:46:35,580 --> 00:46:37,580`
Stulna sektionstoken



`1225 00:46:37,580 --> 00:46:39,580`
Som kringgick MFAs



`1226 00:46:39,580 --> 00:46:41,580`
Liksom kravet



`1227 00:46:41,580 --> 00:46:43,580`
Och sen en ren manipulation



`1228 00:46:43,580 --> 00:46:45,580`
Vad som renderades i browsen



`1229 00:46:45,580 --> 00:46:47,580`
Så det var ju ingen attack mot liksom deras



`1230 00:46:47,580 --> 00:46:49,580`
Faktiska protokoll utan det var ju frontend kod



`1231 00:46:49,580 --> 00:46:51,580`
Det är precis det ni sa



`1232 00:46:51,580 --> 00:46:53,580`
Med att jag tror att jag ska skicka 5 spänn till Mattias



`1233 00:46:53,580 --> 00:46:55,580`
Men jag skickar alla pengar till Johan



`1234 00:46:55,580 --> 00:46:57,580`
Frågan är om den här SD-bucketen var unik



`1235 00:46:57,580 --> 00:46:59,580`
För den här kunden



`1236 00:46:59,580 --> 00:47:01,580`
Det vet man ju inte



`1237 00:47:01,580 --> 00:47:03,580`
Den enda tekniska svagheten som faktiskt utnyttjades



`1238 00:47:03,580 --> 00:47:05,580`
Var att en utvecklare laddade ner och körde okänd kod



`1239 00:47:05,580 --> 00:47:07,580`
Och tappade bort ett token



`1240 00:47:07,580 --> 00:47:09,580`
Ja och förmodligen är detta



`1241 00:47:09,580 --> 00:47:11,580`
Det här låter ju inte som att det är någonting



`1242 00:47:11,580 --> 00:47:13,580`
Som de köper och sen hostar om prem



`1243 00:47:13,580 --> 00:47:15,580`
För det hade ju då krävt



`1244 00:47:15,580 --> 00:47:17,580`
Att de sen gjorde en uppdatering



`1245 00:47:17,580 --> 00:47:19,580`
Nej nej det här var en SaaS-tjänst



`1246 00:47:19,580 --> 00:47:21,580`
Ja



`1247 00:47:21,580 --> 00:47:23,580`
Och där skulle



`1248 00:47:23,580 --> 00:47:25,580`
Där är väl ett stort problem



`1249 00:47:25,580 --> 00:47:27,580`
Skulle jag säga



`1250 00:47:27,580 --> 00:47:29,580`
Ja men exakt men



`1251 00:47:29,580 --> 00:47:31,580`
Om vi nu då går in på Mattias lessons learned



`1252 00:47:31,580 --> 00:47:33,580`
Vad tar ni med er



`1253 00:47:33,580 --> 00:47:35,580`
Vad konkret, vad skulle vi gjort annorlunda



`1254 00:47:35,580 --> 00:47:37,580`
Om vi fick liksom ratta



`1255 00:47:37,580 --> 00:47:39,580`
Bybit här i det här fallet



`1256 00:47:39,580 --> 00:47:41,580`
Vad borde vi lära oss ifrån det här



`1257 00:47:41,580 --> 00:47:43,580`
Jag kan ju inte så mycket om banker



`1258 00:47:43,580 --> 00:47:45,580`
Men om det nu är så att fler



`1259 00:47:45,580 --> 00:47:47,580`
Vi har ett multisign



`1260 00:47:47,580 --> 00:47:49,580`
Setup



`1261 00:47:49,580 --> 00:47:51,580`
Hur ska du bygga en sådan setup



`1262 00:47:51,580 --> 00:47:53,580`
Den kan ju inte vara fysisk



`1263 00:47:53,580 --> 00:47:55,580`
Vi kan inte fysiskt träffas



`1264 00:47:55,580 --> 00:47:57,580`
Varje gång vi ska föra över pengar



`1265 00:47:57,580 --> 00:47:59,580`
Multisign det är ju gold standard nu



`1266 00:47:59,580 --> 00:48:01,580`
Men är ni det sen



`1267 00:48:01,580 --> 00:48:03,580`
Efter det här



`1268 00:48:03,580 --> 00:48:05,580`
Ja det vet jag inte



`1269 00:48:05,580 --> 00:48:07,580`
Om vi nu kallar det multisign eller något annat



`1270 00:48:07,580 --> 00:48:09,580`
Alltså flera personer ska godkänna transaktionen



`1271 00:48:09,580 --> 00:48:11,580`
Ser ni exakt hur vi gör det



`1272 00:48:11,580 --> 00:48:13,580`
Det låter jag vara osagt



`1273 00:48:13,580 --> 00:48:15,580`
Det jag är ute efter är att



`1274 00:48:15,580 --> 00:48:17,580`
Det är inte lokala grejer bara



`1275 00:48:17,580 --> 00:48:19,580`
Utan det måste ju vara



`1276 00:48:19,580 --> 00:48:21,580`
Nätbaserat på något sätt



`1277 00:48:21,580 --> 00:48:23,580`
Eftersom vi kan inte sätta upp en organisation



`1278 00:48:23,580 --> 00:48:25,580`
Som bara funkar när tre personer träffas i ett rum



`1279 00:48:25,580 --> 00:48:27,580`
Det lirar ju inte



`1280 00:48:27,580 --> 00:48:29,580`
Så det måste ju vara remote på något sätt



`1281 00:48:29,580 --> 00:48:31,580`
Därför förstår jag deras approach lite grann här



`1282 00:48:31,580 --> 00:48:33,580`
Att de har en sådan nätbaserad



`1283 00:48:33,580 --> 00:48:35,580`
Chickitygrej



`1284 00:48:35,580 --> 00:48:37,580`
Och svagheten i den här var väl då att



`1285 00:48:37,580 --> 00:48:39,580`
Just det att



`1286 00:48:39,580 --> 00:48:41,580`
Det vi ser



`1287 00:48:41,580 --> 00:48:43,580`
Kan vi inte lita på



`1288 00:48:43,580 --> 00:48:45,580`
Jag hade inte velat ha det som en SaaS lösning



`1289 00:48:45,580 --> 00:48:47,580`
Nej



`1290 00:48:47,580 --> 00:48:49,580`
Men om det är en SaaS kanske inte är grundproblemet



`1291 00:48:49,580 --> 00:48:51,580`
Utan problemet är återigen att vi kan inte lita på det vi ser



`1292 00:48:51,580 --> 00:48:53,580`
Sen om det är en SaaS



`1293 00:48:53,580 --> 00:48:55,580`
Om det hade varit en intern lösning



`1294 00:48:55,580 --> 00:48:57,580`
Den är ju inte säkrare för det



`1295 00:48:57,580 --> 00:48:59,580`
Det hade ju kunnat vara en intern medarbetare som åker på det istället



`1296 00:48:59,580 --> 00:49:01,580`
Så hade det kunnat vara men då kan du



`1297 00:49:01,580 --> 00:49:03,580`
Hade du i alla fall större möjligheter att göra verifiering



`1298 00:49:03,580 --> 00:49:05,580`
Formell verifiering



`1299 00:49:05,580 --> 00:49:07,580`
Hade vi haft SRI så hade det ju blivit blockat direkt



`1300 00:49:07,580 --> 00:49:09,580`
Jag hade velat ha en delay på transaktionerna



`1301 00:49:09,580 --> 00:49:11,580`
Ja



`1302 00:49:11,580 --> 00:49:13,580`
Det är en bra eller escrow på något sätt



`1303 00:49:13,580 --> 00:49:15,580`
Men frågan är ju om det är genomförbart



`1304 00:49:15,580 --> 00:49:17,580`
Jag kan inte bankprocesser liksom



`1305 00:49:17,580 --> 00:49:19,580`
Är det okej att sitta och vänta på saker



`1306 00:49:19,580 --> 00:49:21,580`
Och vad hade förändrats då menar du



`1307 00:49:21,580 --> 00:49:23,580`
Ja men eftersom att



`1308 00:49:23,580 --> 00:49:25,580`
Där hade vi bara upptäckt det tre timmar senare



`1309 00:49:25,580 --> 00:49:27,580`
Det är sant



`1310 00:49:27,580 --> 00:49:29,580`
Ja fast du hade kunnat se att



`1311 00:49:29,580 --> 00:49:31,580`
Den här transaktionen är pending



`1312 00:49:31,580 --> 00:49:33,580`
Du hade haft ett window



`1313 00:49:33,580 --> 00:49:35,580`
Lite Swift grejer att man bankar



`1314 00:49:35,580 --> 00:49:37,580`
Ja det är sant



`1315 00:49:37,580 --> 00:49:39,580`
Du hade kunnat ha lite fraudsystem som säger



`1316 00:49:39,580 --> 00:49:41,580`
Vad är det här för jävla transaktion



`1317 00:49:41,580 --> 00:49:43,580`
Jag tänker att vi missar en viktig grej



`1318 00:49:43,580 --> 00:49:45,580`
Hur kommer det sig att



`1319 00:49:45,580 --> 00:49:47,580`
En utvecklare



`1320 00:49:47,580 --> 00:49:49,580`
Har accessen till



`1321 00:49:49,580 --> 00:49:51,580`
Ja men det är ju en tredje parter å andra sidan



`1322 00:49:51,580 --> 00:49:53,580`
Jo fast det



`1323 00:49:53,580 --> 00:49:55,580`
Det ska ju vara fan hängslen och livren



`1324 00:49:55,580 --> 00:49:57,580`
Jo det håller jag med om



`1325 00:49:57,580 --> 00:49:59,580`
Man kan ju hävda att de hade kunnat



`1326 00:49:59,580 --> 00:50:01,580`
Haft en bättre driftsetup



`1327 00:50:01,580 --> 00:50:03,580`
På safe wallet eller vad det heter



`1328 00:50:03,580 --> 00:50:05,580`
Du ska inte bara kunna gå in och ändra publika S3 filer



`1329 00:50:05,580 --> 00:50:07,580`
Utan det här måste gå igenom en byggserver



`1330 00:50:07,580 --> 00:50:09,580`
Så som jag förstår det så serveras



`1331 00:50:09,580 --> 00:50:11,580`
Den här bucketen till alla kunder



`1332 00:50:11,580 --> 00:50:13,580`
Det är liksom alla kunder



`1333 00:50:13,580 --> 00:50:15,580`
Hämtar sin fronten här i



`1334 00:50:15,580 --> 00:50:17,580`
Och att inte ha SRI och att då låta utvecklaren



`1335 00:50:17,580 --> 00:50:19,580`
Ha full access till det här



`1336 00:50:19,580 --> 00:50:21,580`
Att man kan byta ut



`1337 00:50:21,580 --> 00:50:23,580`
Det är inte okej liksom



`1338 00:50:23,580 --> 00:50:25,580`
Precis innan du kan gå in och ändra någonting



`1339 00:50:25,580 --> 00:50:27,580`
I de här filerna så bör du



`1340 00:50:27,580 --> 00:50:29,580`
Det ska inte gå att vara nåbart helt enkelt



`1341 00:50:29,580 --> 00:50:31,580`
Från en enskild utvecklare



`1342 00:50:31,580 --> 00:50:33,580`
Ja deploy om produktion för det här safe wallet



`1343 00:50:33,580 --> 00:50:35,580`
Borde du ju ha kontroll på



`1344 00:50:35,580 --> 00:50:37,580`
Men okej nu tänker jag att vi summerar lite



`1345 00:50:37,580 --> 00:50:39,580`
Hur nära kom vi då



`1346 00:50:39,580 --> 00:50:41,580`
Men vänta en annan sak som är intressant är



`1347 00:50:41,580 --> 00:50:43,580`
Jag undrar hur signaturprocessen går till



`1348 00:50:43,580 --> 00:50:45,580`
För



`1349 00:50:45,580 --> 00:50:47,580`
Egentligen borde det vara så att det man ser



`1350 00:50:47,580 --> 00:50:49,580`
Är ju garanterat det man signerar



`1351 00:50:49,580 --> 00:50:51,580`
Men i det här fallet



`1352 00:50:51,580 --> 00:50:53,580`
Så har de alltså



`1353 00:50:53,580 --> 00:50:55,580`
För att så andra säga en javascript är allt du ser



`1354 00:50:55,580 --> 00:50:57,580`
Det är ju hela din applikation



`1355 00:50:57,580 --> 00:50:59,580`
Du är ju kokt där



`1356 00:50:59,580 --> 00:51:01,580`
Men vad de gör



`1357 00:51:01,580 --> 00:51:03,580`
För länge sedan



`1358 00:51:03,580 --> 00:51:05,580`
När jag hjälpte en bank



`1359 00:51:05,580 --> 00:51:07,580`
Då hade du ju alltså att



`1360 00:51:07,580 --> 00:51:09,580`
Med



`1361 00:51:09,580 --> 00:51:11,580`
Javascript och så på något sätt



`1362 00:51:11,580 --> 00:51:13,580`
Motivera du någon bank i det liknande



`1363 00:51:13,580 --> 00:51:15,580`
Grej som dyker upp



`1364 00:51:15,580 --> 00:51:17,580`
Och så sker signeringen



`1365 00:51:17,580 --> 00:51:19,580`
Själva signeringen sker ju inte



`1366 00:51:19,580 --> 00:51:21,580`
I webbläsaren



`1367 00:51:21,580 --> 00:51:23,580`
Du kan inte byta ut



`1368 00:51:23,580 --> 00:51:25,580`
Du kan inte byta det gujet hur som helst



`1369 00:51:25,580 --> 00:51:27,580`
Det viktiga distinktionen är ju att



`1370 00:51:27,580 --> 00:51:29,580`
Multisig i det här fallet



`1371 00:51:29,580 --> 00:51:31,580`
Det skyddar ju mot



`1372 00:51:31,580 --> 00:51:33,580`
Kompromitterade nycklar



`1373 00:51:33,580 --> 00:51:35,580`
Men det skyddar ju inte mot



`1374 00:51:35,580 --> 00:51:37,580`
Den som ska signera ser



`1375 00:51:37,580 --> 00:51:39,580`
Det som renderas



`1376 00:51:39,580 --> 00:51:41,580`
Så det är ju ett frontend laget Johan var inne på det



`1377 00:51:41,580 --> 00:51:43,580`
För tidigt



`1378 00:51:43,580 --> 00:51:45,580`
Frontend laget är ju det som ändras



`1379 00:51:45,580 --> 00:51:47,580`
Användaren tror jag att man gör någonting helt legitimt



`1380 00:51:47,580 --> 00:51:49,580`
Men det är ju att



`1381 00:51:49,580 --> 00:51:51,580`
Vi bryter ju inte in och grejar i



`1382 00:51:51,580 --> 00:51:53,580`
Signeringsprocessen i huvud taget



`1383 00:51:53,580 --> 00:51:55,580`
Den är ju fortfarande intakt



`1384 00:51:55,580 --> 00:51:57,580`
Den är ju helt legitim



`1385 00:51:57,580 --> 00:51:59,580`
De gör ju signaturen



`1386 00:51:59,580 --> 00:52:01,580`
Den stämmer kryptografiskt



`1387 00:52:01,580 --> 00:52:03,580`
Allting är bra



`1388 00:52:03,580 --> 00:52:05,580`
Det är bara det att vi har ingen kontroll på



`1389 00:52:05,580 --> 00:52:07,580`
Vilken frontend kod som körs



`1390 00:52:07,580 --> 00:52:09,580`
Vi har liksom lagt massa tid på



`1391 00:52:09,580 --> 00:52:11,580`
Jag menar det för att



`1392 00:52:11,580 --> 00:52:13,580`
Du hade haft någon form av övervakning



`1393 00:52:13,580 --> 00:52:15,580`
På vilka transaktioner som faktiskt sker



`1394 00:52:15,580 --> 00:52:17,580`
De borde monitoreras



`1395 00:52:17,580 --> 00:52:19,580`
Oberoende av varandra kan jag tycka



`1396 00:52:19,580 --> 00:52:21,580`
Där hade du ju kunnat ha en



`1397 00:52:21,580 --> 00:52:23,580`
Canary eller någonting



`1398 00:52:23,580 --> 00:52:25,580`
Ja exakt



`1399 00:52:25,580 --> 00:52:27,580`
Om det är omöjligt att stoppa den



`1400 00:52:27,580 --> 00:52:29,580`
När väl transaktionen är igång



`1401 00:52:29,580 --> 00:52:31,580`
Så hade man kunnat ha



`1402 00:52:31,580 --> 00:52:33,580`
Om signeringsflödet ändå är



`1403 00:52:33,580 --> 00:52:35,580`
Kontrollerat i någon nivå



`1404 00:52:35,580 --> 00:52:37,580`
Så hade man kunnat ha ett regelverk



`1405 00:52:37,580 --> 00:52:39,580`
Av minst så här många timmar



`1406 00:52:39,580 --> 00:52:41,580`
Mellan person 1, person 2 och person 3



`1407 00:52:41,580 --> 00:52:43,580`
För då skulle du ju kunna få



`1408 00:52:43,580 --> 00:52:45,580`
Att aktiveringen av kryptonycken



`1409 00:52:45,580 --> 00:52:47,580`
Kan ske



`1410 00:52:47,580 --> 00:52:49,580`
Först efter att en viss



`1411 00:52:49,580 --> 00:52:51,580`
Tidsintervall har skett



`1412 00:52:51,580 --> 00:52:53,580`
Precis och då kan du ju se vilken transaktion det är



`1413 00:52:53,580 --> 00:52:55,580`
Som kommer genomföras i ett annat system



`1414 00:52:55,580 --> 00:52:57,580`
Och man skulle ju även kunna ha anomalier



`1415 00:52:57,580 --> 00:52:59,580`
När det är jävligt höga belopp



`1416 00:52:59,580 --> 00:53:01,580`
Då är det någon speciell process



`1417 00:53:01,580 --> 00:53:03,580`
Men dels att fundera på



`1418 00:53:03,580 --> 00:53:05,580`
Förr i tiden då



`1419 00:53:05,580 --> 00:53:07,580`
Man hade ju telefonen



`1420 00:53:07,580 --> 00:53:09,580`
Så då är ju allting på en device



`1421 00:53:09,580 --> 00:53:11,580`
Men förr när man kanske hade BankID som en separat dosa



`1422 00:53:11,580 --> 00:53:13,580`
Och man var på webben



`1423 00:53:13,580 --> 00:53:15,580`
Det är ett jävligt dåligt exempel



`1424 00:53:15,580 --> 00:53:17,580`
Men man hade BankID appen iallafall



`1425 00:53:17,580 --> 00:53:19,580`
Och var på webben



`1426 00:53:19,580 --> 00:53:21,580`
Så var det ju så att då kunde man ju faktiskt



`1427 00:53:21,580 --> 00:53:23,580`
Begära transaktionen i webappen



`1428 00:53:23,580 --> 00:53:25,580`
Och sen så signerar man den i mobilappen



`1429 00:53:25,580 --> 00:53:27,580`
Och de skulle ju stämma då där



`1430 00:53:27,580 --> 00:53:29,580`
Det vill säga då hade angripan varit tvungen



`1431 00:53:29,580 --> 00:53:31,580`
Att fejka två miljöer



`1432 00:53:31,580 --> 00:53:33,580`
Fronten i två miljöer



`1433 00:53:33,580 --> 00:53:35,580`
Precis och då hade du ju kunnat ta



`1434 00:53:35,580 --> 00:53:37,580`
Den direkt från



`1435 00:53:37,580 --> 00:53:39,580`
Blockkedjan egentligen



`1436 00:53:39,580 --> 00:53:41,580`
Och se vilken transaktion är det som faktiskt försöker genomföra



`1437 00:53:41,580 --> 00:53:43,580`
Men det är mycket svårare att fejka



`1438 00:53:43,580 --> 00:53:45,580`
Det en användare ser menar jag på två olika ställen



`1439 00:53:45,580 --> 00:53:47,580`
Nu kommer det här bara som



`1440 00:53:47,580 --> 00:53:49,580`
Det är inte de som initierar processen



`1441 00:53:49,580 --> 00:53:51,580`
Utan de bara reagerar, de ska ju bara signera



`1442 00:53:51,580 --> 00:53:53,580`
De får bara ett signeringsuppdrag



`1443 00:53:53,580 --> 00:53:55,580`
De kan ju inte kontexten



`1444 00:53:55,580 --> 00:53:57,580`
Och de ser ju en kontext som är okej



`1445 00:53:57,580 --> 00:53:59,580`
Och det ser ut precis som vanligt



`1446 00:53:59,580 --> 00:54:01,580`
Det är verkligen såhär the perfect storm setup



`1447 00:54:01,580 --> 00:54:03,580`
Om vi summerar lite här nu då innan vi går in på liksom



`1448 00:54:03,580 --> 00:54:05,580`
Avslutningen då



`1449 00:54:05,580 --> 00:54:07,580`
Eller opportunistisk attack



`1450 00:54:07,580 --> 00:54:09,580`
Det löste vi ganska snabbt va



`1451 00:54:09,580 --> 00:54:11,580`
Att det var en riktad attack eller



`1452 00:54:11,580 --> 00:54:13,580`
Ja



`1453 00:54:13,580 --> 00:54:15,580`
Och vi kom också fram till att förberedelsetiden var ganska lång



`1454 00:54:15,580 --> 00:54:17,580`
Alltså att de har haft månader på sig liksom



`1455 00:54:17,580 --> 00:54:19,580`
17 dagar innan de faktiskt gjorde något



`1456 00:54:19,580 --> 00:54:21,580`
De måste ju kartlägga det här företaget och vilka kunderna är



`1457 00:54:21,580 --> 00:54:23,580`
Och vem som jobbar där och göra hela den grejen



`1458 00:54:23,580 --> 00:54:25,580`
Sen insider var det det



`1459 00:54:25,580 --> 00:54:27,580`
Nej



`1460 00:54:27,580 --> 00:54:29,580`
Inte en medveten insider



`1461 00:54:29,580 --> 00:54:31,580`
Nej exakt ganska oavsiktlig insider exakt



`1462 00:54:31,580 --> 00:54:33,580`
Och phishing



`1463 00:54:33,580 --> 00:54:35,580`
Ja som är första steg där



`1464 00:54:35,580 --> 00:54:37,580`
Om man jobbar någons grejen liksom



`1465 00:54:37,580 --> 00:54:39,580`
Supply chain



`1466 00:54:39,580 --> 00:54:41,580`
Definitivt



`1467 00:54:41,580 --> 00:54:43,580`
Jo men det är det ju



`1468 00:54:43,580 --> 00:54:45,580`
Supply chain för banken



`1469 00:54:45,580 --> 00:54:47,580`
Ja exakt och det är ju banken som vi



`1470 00:54:47,580 --> 00:54:49,580`
Det är liksom inte en



`1471 00:54:49,580 --> 00:54:51,580`
Det är inte en traditionell supply chain attack



`1472 00:54:51,580 --> 00:54:53,580`
Så som vi brukar mena



`1473 00:54:53,580 --> 00:54:55,580`
Men likväl en supply chain för banken



`1474 00:54:55,580 --> 00:54:57,580`
Precis



`1475 00:54:57,580 --> 00:54:59,580`
Det är så jävla mycket



`1476 00:54:59,580 --> 00:55:01,580`
Alla sas leverantörer



`1477 00:55:01,580 --> 00:55:03,580`
Supply chain i en kedjelänk



`1478 00:55:03,580 --> 00:55:07,580`
Kunde vi komma fram till om det var komplementerade signeringsnycklar



`1479 00:55:07,580 --> 00:55:09,580`
Eller signeringsprocess



`1480 00:55:09,580 --> 00:55:11,580`
Det trodde vi ju inte utan vi trodde ju att det var processen



`1481 00:55:11,580 --> 00:55:13,580`
Någonting som var strulat där liksom



`1482 00:55:13,580 --> 00:55:15,580`
MFA bypass det pratade vi lite om



`1483 00:55:15,580 --> 00:55:17,580`
Men det tog vi faktiskt inte



`1484 00:55:17,580 --> 00:55:19,580`
Just det här med avs



`1485 00:55:19,580 --> 00:55:21,580`
Den missade vi



`1486 00:55:21,580 --> 00:55:23,580`
Nation state Mattias



`1487 00:55:23,580 --> 00:55:25,580`
Vi nosade lite på det



`1488 00:55:25,580 --> 00:55:27,580`
Lämnade och sen så



`1489 00:55:27,580 --> 00:55:29,580`
Fick Mattias nytt mod



`1490 00:55:29,580 --> 00:55:31,580`
Vilket var bra



`1491 00:55:31,580 --> 00:55:33,580`
Men bortsett från att vi har



`1492 00:55:33,580 --> 00:55:35,580`
AVSS3 nämnt här



`1493 00:55:35,580 --> 00:55:37,580`
Så vet jag inte hur vi ens skulle veta



`1494 00:55:37,580 --> 00:55:39,580`
Att det var avs liksom



`1495 00:55:39,580 --> 00:55:41,580`
Men jag tycker ändå



`1496 00:55:41,580 --> 00:55:43,580`
Alltså av de här så vi tog ändå



`1497 00:55:43,580 --> 00:55:45,580`
Ganska många procent



`1498 00:55:45,580 --> 00:55:47,580`
Av 1,2,3,4,5,6,7,8



`1499 00:55:47,580 --> 00:55:49,580`
Olika indikationer



`1500 00:55:49,580 --> 00:55:51,580`
Så tog vi ändå 6



`1501 00:55:51,580 --> 00:55:53,580`
Klockrent vilket är roligt



`1502 00:55:53,580 --> 00:55:55,580`
Men det var inte så mycket här egentligen



`1503 00:55:55,580 --> 00:55:57,580`
Om vi bortsett från att det snodde hysteriskt mycket



`1504 00:55:57,580 --> 00:55:59,580`
Inferium och sånt



`1505 00:55:59,580 --> 00:56:01,580`
Så var det ju inte



`1506 00:56:01,580 --> 00:56:03,580`
Det var inte så mycket blockchain teknik



`1507 00:56:03,580 --> 00:56:05,580`
Egentligen bakom attacken



`1508 00:56:05,580 --> 00:56:07,580`
Utan det var ganska enkelt



`1509 00:56:07,580 --> 00:56:09,580`
Och en av de svåraste delarna



`1510 00:56:09,580 --> 00:56:11,580`
Här är ju förmodligen att



`1511 00:56:11,580 --> 00:56:13,580`
De måste ha infrastrukturen för cashout



`1512 00:56:13,580 --> 00:56:15,580`
Där liksom



`1513 00:56:15,580 --> 00:56:17,580`
Ja men jag fick 1,5 miljarder



`1514 00:56:17,580 --> 00:56:19,580`
I ethereum till min



`1515 00:56:19,580 --> 00:56:21,580`
Wallet så



`1516 00:56:21,580 --> 00:56:23,580`
Jag hade inte kunnat göra så himla mycket med det tror jag



`1517 00:56:23,580 --> 00:56:25,580`
Nej alltså



`1518 00:56:25,580 --> 00:56:27,580`
Jag hade fått flytta till Nordkorea



`1519 00:56:27,580 --> 00:56:29,580`
Men jag hade kunnat nöja mig med att hitta



`1520 00:56:29,580 --> 00:56:31,580`
Hur cashar vi 10 miljoner



`1521 00:56:31,580 --> 00:56:33,580`
De här miljarderna



`1522 00:56:33,580 --> 00:56:35,580`
Vad ska jag göra med dem



`1523 00:56:35,580 --> 00:56:37,580`
Det finns ju en gräns för hur många båtar jag kan stapla



`1524 00:56:37,580 --> 00:56:39,580`
Ovanpå varandra



`1525 00:56:39,580 --> 00:56:41,580`
Men det kan ju vara så Anders



`1526 00:56:41,580 --> 00:56:43,580`
Om du tjänar 1,5 miljard dollar



`1527 00:56:43,580 --> 00:56:45,580`
Så kanske det finns någon som är villig att ta hand om hälften



`1528 00:56:45,580 --> 00:56:47,580`
Mot en liten avgift



`1529 00:56:47,580 --> 00:56:49,580`
De tar hälften



`1530 00:56:49,580 --> 00:56:51,580`
Och så får du resten vid sidan av



`1531 00:56:51,580 --> 00:56:53,580`
Utan att det finns några spår till dig



`1532 00:56:53,580 --> 00:56:55,580`
Jag kan lösa röda korsets finansiering



`1533 00:56:55,580 --> 00:56:57,580`
På någon framtida åren



`1534 00:56:57,580 --> 00:56:59,580`
Men okej



`1535 00:56:59,580 --> 00:57:01,580`
Innan vi går in på avslutningen



`1536 00:57:01,580 --> 00:57:03,580`
Så får vi göra en grej nu då



`1537 00:57:03,580 --> 00:57:05,580`
För det här är ju ändå säkerhetspodcasten



`1538 00:57:05,580 --> 00:57:07,580`
Och det har varit alldeles för strukturerat



`1539 00:57:07,580 --> 00:57:09,580`
Så vems fel är det här



`1540 00:57:09,580 --> 00:57:11,580`
Ni får välja mellan



`1541 00:57:11,580 --> 00:57:13,580`
Vem bär mest skuld



`1542 00:57:13,580 --> 00:57:15,580`
Är det Bybit



`1543 00:57:15,580 --> 00:57:17,580`
För att de använder 3D-portsmjukvara utan granskning



`1544 00:57:17,580 --> 00:57:19,580`
Är det Safewallet leverantören



`1545 00:57:19,580 --> 00:57:21,580`
För att de har utvecklare med alla nycklar till alltihop



`1546 00:57:21,580 --> 00:57:23,580`
Är det den stackars utvecklare



`1547 00:57:23,580 --> 00:57:25,580`
Vars dator blev dödsägd



`1548 00:57:25,580 --> 00:57:27,580`
Är det kryptobranchen i stort



`1549 00:57:27,580 --> 00:57:29,580`
Eller är det lagstiftare som inte reglerar



`1550 00:57:29,580 --> 00:57:31,580`
Kryptobörs tillräckligt



`1551 00:57:31,580 --> 00:57:33,580`
Avgå alla



`1552 00:57:33,580 --> 00:57:35,580`
Peter



`1553 00:57:35,580 --> 00:57:37,580`
Det känns ju som att Safewallet som organisation



`1554 00:57:37,580 --> 00:57:39,580`
Börjar göra ett väldigt stort ansvar



`1555 00:57:39,580 --> 00:57:41,580`
Det skulle jag tycka



`1556 00:57:41,580 --> 00:57:43,580`
Sen är det väl formellt



`1557 00:57:43,580 --> 00:57:45,580`
Jag är väl alltid banken ansvarig



`1558 00:57:45,580 --> 00:57:47,580`
Men



`1559 00:57:47,580 --> 00:57:49,580`
Någonting verkar ju inte



`1560 00:57:49,580 --> 00:57:51,580`
Fryst på Safewallet



`1561 00:57:51,580 --> 00:57:53,580`
Hade de haft bättre processer



`1562 00:57:53,580 --> 00:57:55,580`
Så hade det behövts fler



`1563 00:57:55,580 --> 00:57:57,580`
Personer komplementerade



`1564 00:57:57,580 --> 00:57:59,580`
På det bolaget



`1565 00:57:59,580 --> 00:58:01,580`
Om man lyckas med attacken



`1566 00:58:01,580 --> 00:58:03,580`
Jag är nog villig att hålla med Peter



`1567 00:58:03,580 --> 00:58:05,580`
Safewallet är nog den stora boven



`1568 00:58:05,580 --> 00:58:07,580`
Utvecklaren är den minsta



`1569 00:58:07,580 --> 00:58:09,580`
Ansvarig här



`1570 00:58:09,580 --> 00:58:11,580`
Man ska kunna köra kod på sin dator



`1571 00:58:11,580 --> 00:58:13,580`
Utan att det kostar 1,5 miljarder



`1572 00:58:13,580 --> 00:58:15,580`
Men kanske inte sin jobbdator



`1573 00:58:15,580 --> 00:58:17,580`
Om man jobbar med de här grejerna



`1574 00:58:17,580 --> 00:58:19,580`
Alltså bättre processer



`1575 00:58:19,580 --> 00:58:21,580`
Men det är inte där skulden börjar ligga



`1576 00:58:21,580 --> 00:58:23,580`
Så det är Safewallet



`1577 00:58:23,580 --> 00:58:25,580`
Jag tycker också banken



`1578 00:58:25,580 --> 00:58:27,580`
Och när man pratar om banken



`1579 00:58:27,580 --> 00:58:29,580`
Och har en avdelning



`1580 00:58:29,580 --> 00:58:31,580`
Så de tre



`1581 00:58:31,580 --> 00:58:33,580`
Jättebra



`1582 00:58:33,580 --> 00:58:35,580`
Det var det jag menade med att avgå alla



`1583 00:58:35,580 --> 00:58:37,580`
Alla bär del av skuld här



`1584 00:58:37,580 --> 00:58:39,580`
Så jag säger att det här



`1585 00:58:39,580 --> 00:58:41,580`
Nu summerar vi



`1586 00:58:41,580 --> 00:58:43,580`
Det här var cold case i Säkerhetspodcasten



`1587 00:58:43,580 --> 00:58:45,580`
Om ni gillade det här och vill höra mer



`1588 00:58:45,580 --> 00:58:47,580`
Så hör av er på kontaktet



`1589 00:58:47,580 --> 00:58:49,580`
Skicka gärna in ett cold case till oss



`1590 00:58:49,580 --> 00:58:51,580`
Jättegärna



`1591 00:58:51,580 --> 00:58:53,580`
Om ni tyckte det var kul såklart



`1592 00:58:53,580 --> 00:58:55,580`
Har du en template som folk kan använda



`1593 00:58:55,580 --> 00:58:57,580`
Ett cold format



`1594 00:58:57,580 --> 00:58:59,580`
Jag kan fixa det



`1595 00:58:59,580 --> 00:59:01,580`
Skicka in den skills.md



`1596 00:59:01,580 --> 00:59:03,580`
Så får Jesper bara köra den



`1597 00:59:03,580 --> 00:59:05,580`
Jag kan dela den



`1598 00:59:05,580 --> 00:59:07,580`
SmodX och allting ni skickar in



`1599 00:59:07,580 --> 00:59:09,580`
Men vi kan väl lägga upp de här pappren



`1600 00:59:09,580 --> 00:59:11,580`
Som vi har fått av dig på våran sajt



`1601 00:59:11,580 --> 00:59:13,580`
Ja det kan vi göra



`1602 00:59:13,580 --> 00:59:15,580`
Så kan ni se vad vi fick framför oss



`1603 00:59:15,580 --> 00:59:17,580`
Kul



`1604 00:59:17,580 --> 00:59:19,580`
Och Johan take it away



`1605 00:59:19,580 --> 00:59:21,580`
Jag tyckte det här var jätteroligt



`1606 00:59:21,580 --> 00:59:23,580`
Och med de orden får vi tacka för oss den här gången



`1607 00:59:23,580 --> 00:59:25,580`
Jag som pratade rätt och Johan du bemöller mig



`1608 00:59:25,580 --> 00:59:27,580`
Det här är jag Peter Magnusson



`1609 00:59:27,580 --> 00:59:29,580`
Gudsaposten



`1610 00:59:29,580 --> 00:59:31,580`
Espelardo



`1611 00:59:31,580 --> 00:59:33,580`
Multisignaturen



`1612 00:59:33,580 --> 00:59:35,580`
Skål och välkommen



`1613 00:59:35,580 --> 00:59:37,580`
Det är faktiskt så roligt att vi har



`1614 00:59:37,580 --> 00:59:39,580`
Kommit upp i vår 300 avsnitt



`1615 00:59:39,580 --> 00:59:41,580`
Lite beroende på hur man räknar



`1616 00:59:41,580 --> 00:59:43,580`
Så kan det vara mer eller mindre



`1617 00:59:43,580 --> 00:59:45,580`
Men vi har bestämt oss för att det är 300 avsnitt



`1618 00:59:45,580 --> 00:59:47,580`
Som ska spelas in den 24 mars



`1619 00:59:47,580 --> 00:59:49,580`
Exakt



`1620 00:59:49,580 --> 00:59:51,580`
Och det tänkte vi att vi skulle fira



`1621 00:59:51,580 --> 00:59:53,580`
Med de lyssnare som vill och kan



`1622 00:59:53,580 --> 00:59:55,580`
Exakt



`1623 00:59:55,580 --> 00:59:57,580`
Vi pratar lite gamla goa minnen



`1624 00:59:57,580 --> 00:59:59,580`
Och sen så kommer vi gå och träffa de som vill



`1625 00:59:59,580 --> 01:00:01,580`
För att ta en öl



`1626 01:00:01,580 --> 01:00:03,580`
Så höj volymen



`1627 01:00:03,580 --> 01:00:05,580`
Vart träffas vi?



`1628 01:00:05,580 --> 01:00:07,580`
Vi träffas på Bishops Arms på Avenyn



`1629 01:00:07,580 --> 01:00:09,580`
Park Avenue tror jag lokalen heter



`1630 01:00:09,580 --> 01:00:11,580`
Det ligger alltså i samma ut som



`1631 01:00:11,580 --> 01:00:13,580`
Security Fest brukar vara



`1632 01:00:13,580 --> 01:00:15,580`
Men högst upp på Avenyn på vänster sida



`1633 01:00:15,580 --> 01:00:17,580`
Och det tänkte vi göra från klockan 18



`1634 01:00:17,580 --> 01:00:19,580`
Den 24 mars



`1635 01:00:19,580 --> 01:00:21,580`
Och vi tänker vara så bold



`1636 01:00:21,580 --> 01:00:23,580`
Och säga att kom bara



`1637 01:00:23,580 --> 01:00:25,580`
Ni behöver inte anmäla er



`1638 01:00:25,580 --> 01:00:27,580`
Ni behöver bara dyka upp



`1639 01:00:27,580 --> 01:00:29,580`
Ni fem som lyssnar kom



`1640 01:00:29,580 --> 01:00:31,580`
Så ordnar det sig



`1641 01:00:31,580 --> 01:00:33,580`
Om ni vill ta reda på hur populär vi egentligen är



`1642 01:00:33,580 --> 01:00:35,580`
Det är roligt att dyka upp



`1643 01:00:35,580 --> 01:00:37,580`
Ni får titta efter oss



`1644 01:00:37,580 --> 01:00:39,580`
Vi kommer väl inte vara anmälda



`1645 01:00:39,580 --> 01:00:41,580`
Och om vi mot all förmoden



`1646 01:00:41,580 --> 01:00:43,580`
Har mejlat eller ändrat



`1647 01:00:43,580 --> 01:00:45,580`
Våra planer



`1648 01:00:45,580 --> 01:00:47,580`
Så håll koll på vår blogg på sky



`1649 01:00:47,580 --> 01:00:49,580`
Om vi fuckar upp det här



`1650 01:00:49,580 --> 01:00:51,580`
Så ska vi säga till att vi har fuckat upp



`1651 01:00:51,580 --> 01:00:53,580`
Det lovar vi att göra i de kanaler vi har



`1652 01:00:53,580 --> 01:00:55,580`
Exakt


