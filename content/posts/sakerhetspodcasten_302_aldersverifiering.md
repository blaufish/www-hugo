---
date: '2026-05-04T10:28:00'
tags:
- tema
title: 'Säkerhetspodcasten #302 - Åldersverifiering'
---

Åldersverifiering på Internet är just nu hett i hela världen
   -- EU, UK, Australien, USA, ...
Risker, fördelar, designval runt åldersverifiering,
  vi diskuterar igenom, med primärt fokus på EU.

Vi spelade in strax innan Paul Moore påtalade en drös fel och brister i
  EU's Android app och EU's system/biljettformat för åldersbevis.

## Lyssna
* [mp3](https://traffic.libsyn.com/secure/sakerhetspodcasten/2026-04-15_AgeID.mp3?dest-id=117848), längd: 53:33

## EU's lösning för åldersverifiering

EU vill rulla ut en lösning där man då och då måste autentisera sig,
  men får ett integritetsskyddat (engelska _privacy-preserving_)
  bevis för sin ålder.

Länkar:
* [Shaping Europe’s digital future: The EU approach to age verification](https://digital-strategy.ec.europa.eu/en/policies/eu-age-verification)
* [Overall architecture - European Age Verification Solution](https://ageverification.dev/av-doc-technical-specification/docs/architecture-and-technical-specifications/#131-definitions)
* [GitHub - eu-digital-identity-wallet/av-app-android-wallet-ui · GitHub](https://github.com/eu-digital-identity-wallet/av-app-android-wallet-ui)
* [YouTube/ Europe Echo: Ursula von der Leyen Unveils EU Age Verification App](https://www.youtube.com/watch?v=4VRRriyDKKk) `video`
* [YouTube/ DigitalEU: Blueprint for an age verification solution to help protect minors online](https://www.youtube.com/watch?v=ULFTrTznG7Y) `video`

Nyhetsartiklar om EU's åldersverifiering:
* [Macron Pushes EU Leaders for Coordinated Social Media Ban](https://www.globalbankingandfinance.com/macron-host-call-eu-leaders-social-media-ban-minors/)
* [Göteborgs-Posten: EU - App redo för ålderskoll på nätet](https://www.gp.se/nyheter/varlden/eu-app-redo-for-alderskoll-pa-natet.9e3d2c70-a5a2-5b39-88c3-57266bcea5a9)
* [Göteborgs-Posten: EU:s nya app ska verifiera barns ålder på sociala medier](https://www.gp.se/nyheter/varlden/eus-nya-app-ska-verifiera-barns-alder-pa-sociala-medier.d4895635-20b5-40c3-a591-fe74ea478af4)

## Kritik mot åldersverifiering

Det finns en hel del invändningar mot att begränsa åtkomsten till internet,
  och att träna folk i att onödan autentisera sig mot staten eller tredje
  part.

Åldersverifiering får flera negativa konsekvenser,
  EFF's lista fritt översatt till svenska:

> 1. Vuxna utan ID-kort blir utelåsta
> 2. Färgade grupper möter högre felfrekvenser
> 3. Personer med funktionsnedsättning möter fler hinder
> 4. Transpersoner och icke-binära personer utsätts för risk
> 5. Anonymitet blir ett offer
> 6. Ungdomar förlorar tillgång till viktig information
> 7. HBTQ+-ungdomar nekas viktiga livlinor
> 8. Ungdomar i fosterhemssystem lämnas helt utanför
> 9. Våra personuppgifter utsätts för risk
> 10. Våra rättigheter till yttrandefrihet trampas på

Länkar:
* [European Digital Rights (EDRi): Why age verification misses the mark and puts everyone at risk - Age verification is a short-sighted, ineffective and dangerous way to protect young people form online harms.](https://edri.org/our-work/why-age-verification-misses-the-mark-and-puts-everyone-at-risk/)
* [Electronic Frontier Foundation: 10 (Not So) Hidden Dangers of Age Verification](https://www.eff.org/deeplinks/2025/12/10-not-so-hidden-dangers-age-verification)

## Säkerhetshål i EU's åldersverifieringsapp

[Paul Moore](https://x.com/Paul_Reviews) påtalade en bunt problem efter att
  vi spelat in:

- Använda en och samma åldersverifiering om och om igen.
  Svårt att bygga bort om man vill ha kvar
  integritetsskyddat (engelska _privacy-preserving_)
  bevis för ålder.
  De flesta enkla motmedel skulle göra ens bevis mer spårbart, lättare att
  koppla till person/enhet.
- Android app bister:
  - PIN bypass.
    Åldersbeviset på telefonen är inte krypterat/kopplat till ens PIN.
  - Tar inte bort PII data som den skall
  - Krypterar inte PII data den sparar ner
  - 2026.04-2 härdning:
    La till utdaterade beroenden, använder krypto-bibliotek som är
    `@Deprecated` sedan flera år.
  - 2026.04-2 härdning:
    La till `PBKDF2` kryptering med svag konfiguration (hash/iterationer)...
    och om ens hemlighet hur som helst är ett kort svagt PIN,
    är ens en stark konfiguration bra nog?

Länkar, artiklar:
* [Proton: EU age verification app hacked in 2 minutes – now what?](https://proton.me/blog/eu-age-verification-app-hacked)
* [YouTube/ Deep Humor: Age Verification App Got Hacked...](https://www.youtube.com/watch?v=1hfDOhrNx1I) `video`
* [YouTube/ Deep Humor: Age Verification App Hacked AGAIN!](https://www.youtube.com/watch?v=EcR4Ldg-ATU) `video`

### Krypteringsproblemen

[Några av krypteringsproblemen](https://x.com/Paul_Reviews/status/2044723123287666921):

- PIN inte kopplat till ditt data.
- Du kan byta PIN utan att veta gamla PIN och behålla ditt data.
  i.e. en annan användare kan sno någons åldersverifiering.
- Du kan testa PIN i appen hur många gånger som helst, om du modifierar en fil.

> During setup, the app asks you to create a PIN.
>  After entry, the app *encrypts* it and saves it in the `shared_prefs` directory.
>
> 1.  It shouldn't be encrypted at all - that's a really poor design.
> 2. It's not cryptographically tied to the vault which contains the identity data.
>
> So, an attacker can simply remove the `PinEnc`/`PinIV` values from the
>   `shared_prefs` file and restart the app.
>
> After choosing a different PIN, the app presents credentials created under
>   the old profile and let's the attacker present them as valid.
>
> Other issues:
> 1.  Rate limiting is an incrementing number in the same config file. Just reset it to 0 and keep trying.
> 2.  "UseBiometricAuth" is a boolean, also in the same file. Set it to false and it just skips that step.

### Kringgå begränsningar med egen kod

[En egen Chrome Extension](https://twitter.com/Paul_Reviews/status/2044784814289523093):

> I've ported the Android app logic to a Chrome extension -
>   stripping out the pesky step of handing over biometric data which they can
>   leak... and pass verification instantly.
>
> Step 1: Install the extension \
> Step 2: Register an identity (just once) \
> Step 3: Continue using the web as normal
>
> The extension detects the QR code, generates a cryptographically identical
>   payload and tells the verifier I'm over 18, which it "fully trusts".
>
> This isn't a bug... it's a fundamental design flaw they can't solve without
>   irrevocably tying a key to you personally; which then allows
>   tracking/monitoring.

### Brister i bildkryptering, filborttagning

[Om problem med bildkryptering, ta bort bilder](https://x.com/Paul_Reviews/status/2044436001611801072):

> The app goes to great lengths to protect the AV data AFTER collection
>  (`is_over_18`: true is AES-GCM'd); it does so pretty well.
>
> But, the source image used to collect that data is written to disk without
>   encryption and not deleted correctly.

NFC bilder:

> It pulls DG2 and writes a lossless PNG to the filesystem.
> It's only deleted on success.
> If it fails for any reason (user clicks back, scan fails & retries, app
>   crashes etc), the full biometric image remains on the device in cache.

Selfie bilder:

> These images are written to external storage in lossless PNG format,
>   but they're never deleted.  Not a cache... long-term storage.


### Första härdningen, release 2026.04-2

eu-digital-identity-wallet uppdatering
  [Release 2026.04-2](https://github.com/eu-digital-identity-wallet/av-app-android-wallet-ui/releases/tag/2026.04-2)
  första svaret på påtalade brister:

> This release hardens the Age Verification Blueprint App across several layers.
>
> * On-device data: database and settings encrypted at rest, with keys protected
>   by the device’s hardware-backed key store.
> * Runtime: the app checks device integrity on startup and refuses to run on
>   rooted or jailbroken devices. Production deployments should complement it
>   with stronger device-attestation mechanisms appropriate to their
>   infrastructure and compliance requirements.
> * Passport onboarding: more stable scanning; the passport photo is stored
>   privately and deleted as soon as it’s no longer needed.
> * PIN: stricter rules block easy-to-guess PINs; PINs are salted and hashed,
>   never stored in plain form.
>
> First hardening step — more to come.

[Paul Moore om deras uppdateringar, 1](https://twitter.com/Paul_Reviews/status/2047288336511897632):

> If we ignore the fact they've used a 6 year old deprecated library,
>  they haven't actually solved the problem at all.  An attacker can just
>   as easily delete ciphertext as plain text.

[Paul Moore om deras uppdateringar, 2](https://twitter.com/Paul_Reviews/status/2047043703173513635):

> They introduced `androidx.security:security-crypto`, deprecated in 2025.
> Also `androidx.security.crypto.EncryptedSharedPreferences`, deprecated in 2025.
> Finally, `androidx.security.crypto.MasterKeys`, which were deprecated in 2020.

> They salt correctly (a true CSPRNG), then use PBKDF2-SHA256 -
>  which is outdated and only recommended where FIPS compliance
>  is required, which doesn't apply here.
>
> To make matters worse, they use just 210,000 iterations.
> For those of a NISTy disposition, you're likely already shaking your head.
> 210,000 seems oddly specific.
> It is. It's the @owasp minimum for PBKDF2-SHA512, not SHA256.
> Right number, wrong algorithm.
> In reality, OWASP recommended 600,000 iterations as a minimum in 2023.
>
> Worse still, 600,000 is the baseline minimum for passwords, not PINs
>   with 1 million permutations.
> You could use 1B iterations,
>   you're not measurably increasing security when there are so few
>   attempts required to break it.  At the very least, use a modern
>   hash with reasonable brute-force resistance against a 2026 threat model.


## Feedback

**Thomas** hörde av sig:

> Lyssnade på avsnittet om åldersverifiering.
>
> Funderar lite och borde man inte kunna sätta upp det såhär:
>
> Hemsidor pratat bara med appen. De ger en sträng som måste
> komma tillbaka signerad av rätt auktoritet. Appen tar strängen
> och får den signerad och ger den till hemsidan. Förutsatt att
> strängen inte läcker data så borde väl nu inte auktorieteten
> få reda på vilken hemsida det är?

Knåpade ihop detta svar:


> Mmm, Din design ide är inte helt kass.
>
> Oavsiktliga läckage: Som du beskriver den så skulle dock
> ”cornhub-123456” läcka mellan Rp relying party och
> autentisering backend. Men man skulle kunna blinda detta
> på lite olika sätt, typ

``` plain
SHA256(
  concat(
    SHA256(app-nonce),
    SHA256(domännamn),
    SHA256(sträng-från-sajten)
  )
)
```

> och sen ge sajten vad den behöver för att verifiera ens åldersbevis rör deras challenge.
>
> Missbruk: Din modell förhindrar inte missbruk, t.ex. att tusentals
>   enheter delar ett och samma åldersbevis.
>
> Om du kollar i FIDO spec:ar finns mer seriöst vad de tänkt på och
>   vilka delar av FIDO lösningen som skall skydda mot vad. Det är
>   nog det mest väldokumenterade, genomtänkta autentiseringsramverket
>   med massvis med olika privacy-avvägningar gjorda. De har en bunt
>   designade motmedel mot oavsiktliga läckage.
>
> Det är mycket som hamnar i ”vad är vår hotmodell”. \
> T.ex. litar vi på att appen gör vad den skall? \
> T.ex. litar vi på att auth-backend och relying party
>   inte samarbetar för att korrelera vem man är.
>   Säg t.ex. att rp och auth-backend anser att ett
>   åldersbevis är inblandat i ett brott, kommer de
>   då samarbeta för spåra vilket ID som begick ett brott?
>
> Appen behöver egentligen inte prata med autentiseringsbackend.
> Behöver inte finnas någon kontakt mellan Rp relying party och
>   Auth-infran utöver t.ex.
> - vilka signing keys som är betrodda
> - eventuella blacklist som gäller
>
> EU’s lösning skall funka typ så.
>
> Det intressanta är vilken modell man väljer och vad den skall skydda mot.
>
> Vi spelade ju in före Paul Moore’s analys, han påvisade precis den typen
>   av attack mot EUs nuvarande lösning.
> Problembilden är att privacy preserving ligger i konflikt med andra mål.
>
> Om man vill skydda detta ”på riktigt” kommer man t.ex. vilja förhindra att åldersbevis:
> - är giltiga mer än X tid
> - kopieras mellan olika enheter
> - användas mer än X gånger
> - används i ej godkänd mjukvara
>
> Den senaste releasen de gjorde nyss gör ett antal saker för att förhindra att
>  appen kan starta i jailbreak’ade telefoner.
> (Se t.ex. FIDO / passkeys som är äldre och mer moget, för en del tillämpningar -
>   bank m.m. - tillåter man bara betrodda signerade enheter)
>
> Så frågan är hur man balanserar äkthet på åldersbeviset med
>   privacy/integritetsskydd. Skall man ha full äkthet vill man att backend
>   skall se allt och bara låta ens egen app få lov att jobba med lösningen.
> Vill man ha full privacy preserving gör man så lite inskränkning som
>   möjligt och så lite insyn som möjligt.
>
> Det vore inte orimligt att man på sikt skulle vilja ha en helt annan
>  lösning än det man har idag… vill rulla ut en rätt annorlunda
>  version 2 som är mer robust mot attacker; ergo mindre privacy fokuserad.
>
> Jag har en stark misstanke om att Paul Moore’s chrome extension inte
>   kommer tillåtas publicering, att EU kommer bli jättesura på alla som
>   gör konkurrerande appar där de saknar kontroll/insyn.
> EU har redan börjat prata om att förbjuda VPN som ett sätt att stoppa
>   att lagen kringgås.
>
> Så allt är teknisk lösbart det är bara frågan om vilken hotmodell man
>   väljer, vad man litar på, vem man litar på.
>
> EFF m.fl. har en del andra invändningar som inte är lika
>   teknik/ säkerhet/ privacy orienterade.
> Tillgänglighet för funktionshindrade, papperslösa, HBTQ+, färgade.
>
> Typ så, tillit, privacy och tillgänglighet i en go röra :)

## AI transkribering

_AI försöker förstå oss... Ha överseende med galna feltranskriberingar._

`1 00:00:00,000 --> 00:00:04,540`
Hej och välkomna till Säkerhetspodcasten. Jag som pratar heter Johan Ryberg-Möller, med mig har jag Mattias Hidrager.



`2 00:00:05,520 --> 00:00:07,380`
Japp, det här är jag.



`3 00:00:08,220 --> 00:00:10,580`
Hej och välkommen. Peter Magnusson är också här.



`4 00:00:10,800 --> 00:00:11,280`
Dave.



`5 00:00:11,900 --> 00:00:13,120`
Och Jesper Larsson.



`6 00:00:13,540 --> 00:00:14,260`
Jag tror det.



`7 00:00:14,860 --> 00:00:15,940`
Jespers konstant.



`8 00:00:16,100 --> 00:00:18,460`
Ja, Blanks konstant har vi precis pratat om.



`9 00:00:18,580 --> 00:00:20,500`
Rickard är inte här, men förhoppningsvis snart med oss igen.



`10 00:00:21,220 --> 00:00:21,820`
Så är det faktiskt.



`11 00:00:22,420 --> 00:00:26,360`
Innan vi börjar så ska vi nämna att det är den 15 april när vi spelar in.



`12 00:00:26,360 --> 00:00:30,340`
Och vi är sponsrade av Shored som finns på Shored.se.



`13 00:00:30,480 --> 00:00:35,020`
Så även av 0x4A som finns på 0x4A.se och Bortfors som finns på Bortfors.se.



`14 00:00:35,820 --> 00:00:36,640`
Där har vi alla dem.



`15 00:00:36,760 --> 00:00:39,620`
Jesper, Securityfest är en grej som vi håller på med.



`16 00:00:40,160 --> 00:00:40,720`
Några av oss.



`17 00:00:41,040 --> 00:00:43,120`
Ja, jag hörde att det var en liten explosion bakgrund.



`18 00:00:43,300 --> 00:00:43,820`
Det är ju Göteborg.



`19 00:00:44,020 --> 00:00:45,660`
Ja, den kom jättebra.



`20 00:00:47,860 --> 00:00:50,180`
Securityfest är ju GoAfsApen och ni som inte har köpt biljett,



`21 00:00:50,960 --> 00:00:52,540`
ställ er i kö för det finns inga biljetter.



`22 00:00:52,540 --> 00:00:54,280`
Men, exakt.



`23 00:00:54,980 --> 00:00:56,060`
Det finns en möjlighet.



`24 00:00:56,360 --> 00:00:58,180`
Att komma in på konferensen.



`25 00:00:58,320 --> 00:00:59,460`
Huta mig eller Jesper.



`26 00:00:59,940 --> 00:01:00,600`
Det går alltid.



`27 00:01:01,580 --> 00:01:02,740`
Men det är svårt att göra nu.



`28 00:01:03,140 --> 00:01:04,640`
Men vad man kan göra faktiskt.



`29 00:01:04,780 --> 00:01:07,260`
Vi har en biljett kvar till en av våra trainings.



`30 00:01:07,960 --> 00:01:10,740`
Som är fullstack pentesting laboratory.



`31 00:01:13,680 --> 00:01:14,860`
Man lär sig allt.



`32 00:01:15,000 --> 00:01:16,260`
Jag har läst innehållet här.



`33 00:01:16,380 --> 00:01:17,060`
Så den är bra att gå.



`34 00:01:18,360 --> 00:01:19,980`
Det är verkligen högt och lågt.



`35 00:01:21,320 --> 00:01:24,060`
Men om man då går training med Dave.



`36 00:01:24,880 --> 00:01:25,760`
Eller David.



`37 00:01:26,360 --> 00:01:29,120`
Så får man faktiskt access till konferensen också.



`38 00:01:29,120 --> 00:01:35,120`
Så det är inte nog med att man får massa cool kunskap som man kan lägga i sin verktygslåda av saker.



`39 00:01:35,120 --> 00:01:39,920`
Så får man också komma på konferensen och hänga där och träffa oss.



`40 00:01:39,920 --> 00:01:41,120`
Det brukar vara väldigt roligt.



`41 00:01:41,120 --> 00:01:46,120`
Ja, det finns inte jättemånga sådana trainings kvar men hej, köp dem.



`42 00:01:46,120 --> 00:01:48,620`
Medans hjärnet är varmt.



`43 00:01:48,620 --> 00:01:50,620`
Ja, eller någon form av metall.



`44 00:01:50,620 --> 00:01:51,820`
Ska man svida.



`45 00:01:51,820 --> 00:01:53,020`
Hackegebegej.



`46 00:01:53,020 --> 00:01:55,700`
QueerLGBTQ\+.



`47 00:01:55,700 --> 00:01:57,500`
IT-säkerhetskonferens.



`48 00:01:57,500 --> 00:01:58,700`
Den 30 maj.



`49 00:01:58,700 --> 00:02:00,500`
Regnbokshuset i Göteborg.



`50 00:02:00,500 --> 00:02:02,500`
Kom ihåg att registrera er för att få plats.



`51 00:02:02,500 --> 00:02:06,500`
Jag fick ihop en bloggpost om RSA som jag skickade ut.



`52 00:02:06,500 --> 00:02:08,500`
Till webbgården.



`53 00:02:08,500 --> 00:02:10,500`
Ja, RSA-konferensen.



`54 00:02:10,500 --> 00:02:13,500`
Nej, alltså bara kryptot RSA.



`55 00:02:13,500 --> 00:02:19,500`
Lite lagom för folk som är typ CTF-intresserade.



`56 00:02:19,500 --> 00:02:25,500`
De lite enklare, lättexploitade RSA-problemen tar den upp.



`57 00:02:25,500 --> 00:02:26,300`
Okej, nice.



`58 00:02:26,300 --> 00:02:28,300`
Vad kan man läsa mer om dem?



`59 00:02:28,300 --> 00:02:29,300`
På iShownotes.



`60 00:02:29,300 --> 00:02:32,300`
Ja, iShownotes är det blowfish.blogg.



`61 00:02:32,300 --> 00:02:37,300`
Nej, blowfish.github.com tror jag kanske.



`62 00:02:37,300 --> 00:02:40,300`
Gå in på sakenspodcast.se på iShownotes.



`63 00:02:40,300 --> 00:02:42,300`
Ja, på iShownotes kommer det stå en riktig ura.



`64 00:02:42,300 --> 00:02:46,300`
Om Arit hinner tolka den på ett korrekt sätt. Annars googla.



`65 00:02:46,300 --> 00:02:48,300`
Det här är ett strukturerat avsnitt.



`66 00:02:48,300 --> 00:02:50,300`
Ja, det har alla redan förstått.



`67 00:02:50,300 --> 00:02:52,300`
Vad ska vi prata om idag, Johan?



`68 00:02:52,300 --> 00:02:53,300`
Idag ska vi prata om någonting som är högre.



`69 00:02:53,300 --> 00:02:54,500`
Idag ska vi prata om någonting som är högre.



`70 00:02:54,500 --> 00:02:55,500`
Idag ska vi prata om någonting som är högre.



`71 00:02:55,500 --> 00:02:56,500`
Idag ska vi prata om någonting som är högre.



`72 00:02:56,500 --> 00:02:57,500`
Idag ska vi prata om någonting som är högre.



`73 00:02:57,500 --> 00:03:04,500`
När vi precis drog igång detta så sa du, Mattias, att du hade sett två artiklar i GP om detta bara idag.



`74 00:03:04,500 --> 00:03:08,500`
Så det är fingret på pulsen som alltid är här i Säkerhetspodcast-stugan.



`75 00:03:08,500 --> 00:03:16,500`
Jag tror det var igår så stod Macron på någon scen och basonerade ut åsikter.



`76 00:03:16,500 --> 00:03:18,500`
Men nu ska vi inte hålla lyssnarna på halter för länge.



`77 00:03:18,500 --> 00:03:20,500`
Vad är det vi ska prata om?



`78 00:03:20,500 --> 00:03:22,500`
Vi ska prata om något så roligt som...



`79 00:03:22,500 --> 00:03:23,500`
Vi ska prata om något så roligt som...



`80 00:03:23,500 --> 00:03:24,500`
Vi ska prata om något så roligt som...



`81 00:03:24,500 --> 00:03:26,500`
Vi ska prata om något som...



`82 00:03:26,500 --> 00:03:28,500`
Vi ska prata om något som...



`83 00:03:28,500 --> 00:03:30,500`
recession hittills, och om det t ex.



`84 00:03:30,500 --> 00:03:32,500`
anim funciona...



`85 00:03:32,500 --> 00:03:34,700`
Vi ska prata om något som åldersverifiering.



`86 00:03:34,700 --> 00:03:36,700`
Vi ska prata om något som åldersverifiering.



`87 00:03:36,700 --> 00:03:38,500`
Olika metoder för begränsad access till olika resurser.



`88 00:03:38,500 --> 00:03:40,500`
Olika metoder för begränsad access till olika resurser.



`89 00:03:40,500 --> 00:03:42,500`
Olika metoder för begränsad access till olika resurser.



`90 00:03:42,500 --> 00:03:44,500`
Resurser som sociala medier eller pornografi eller andra sådana.



`91 00:03:44,500 --> 00:03:46,500`
Resurser som sociala medier eller pornografi eller andra sådana.



`92 00:03:46,500 --> 00:03:48,500`
Resurser som sociala medier eller pornografi eller andra sådana.



`93 00:03:48,500 --> 00:03:50,500`
Resurser som sociala medier eller pornografi eller andra sådana.



`94 00:03:50,500 --> 00:03:52,500`
Gaming.



`95 00:03:52,500 --> 00:03:53,500`
Gaming. Alkohol och betting.



`96 00:03:53,500 --> 00:03:55,040`
När man ska gå in på barer och sådana saker.



`97 00:03:55,380 --> 00:03:57,080`
Men det är i en mer analog form.



`98 00:03:57,360 --> 00:03:59,140`
Ja, då får man visa sitt plastkort.



`99 00:03:59,560 --> 00:04:01,160`
Precis, men vi har ju sett det senaste.



`100 00:04:01,360 --> 00:04:03,660`
Jag vet inte exakt när den här trenden egentligen började.



`101 00:04:03,780 --> 00:04:05,200`
Men det är de senaste åren.



`102 00:04:05,860 --> 00:04:07,400`
Senaste typ två åren skulle jag säga.



`103 00:04:07,740 --> 00:04:09,440`
Som man har sett väldigt mycket om det här.



`104 00:04:10,440 --> 00:04:16,240`
Australien gick ut och lagstiftade om att begränsa tillgången till sociala medier.



`105 00:04:16,240 --> 00:04:20,400`
För barn under 15 eller 16 år.



`106 00:04:20,620 --> 00:04:21,200`
Ja, något sånt.



`107 00:04:21,500 --> 00:04:23,440`
Och det var väl för några månader sedan om jag minns rätt.



`108 00:04:23,500 --> 00:04:28,460`
Sen var det ju rejäla protester från diverse ungdomar i Australien.



`109 00:04:28,620 --> 00:04:29,260`
Som man kan tänka sig.



`110 00:04:30,640 --> 00:04:32,240`
Tror du inte det är en bra sak alltså?



`111 00:04:32,560 --> 00:04:36,400`
Ängland har gått ut och gjort liknande manövrar.



`112 00:04:36,500 --> 00:04:38,560`
Även för pornografi.



`113 00:04:39,120 --> 00:04:41,240`
De har ju det här kända DNS-filtret.



`114 00:04:41,460 --> 00:04:44,560`
Vilket det kommer vi komma in på under dagens avsnitt.



`115 00:04:44,680 --> 00:04:46,960`
Hur effektivt det faktiskt egentligen inte är.



`116 00:04:47,500 --> 00:04:48,760`
Precis, även i USA.



`117 00:04:48,760 --> 00:04:52,760`
I vissa delstater så är det begränsat framförallt just pornografi.



`118 00:04:53,500 --> 00:04:57,800`
Men i UK så är det väl bredare än så.



`119 00:04:57,900 --> 00:05:00,520`
För jag läste någonstans, det var för en månad sedan eller någonting.



`120 00:05:00,700 --> 00:05:06,780`
Så var det Reddit som fick 14,5 miljoner pound i böter.



`121 00:05:06,900 --> 00:05:09,500`
För att de då inte hade implementerat åldersverifiering.



`122 00:05:10,340 --> 00:05:11,660`
På ett tillräckligt bra sätt.



`123 00:05:12,340 --> 00:05:18,500`
Jag vet ju att X har väl också det för framförallt pornografi.



`124 00:05:18,500 --> 00:05:23,480`
Men också, vad kallar man det när det är gory stuff.



`125 00:05:23,500 --> 00:05:25,000`
Adult content.



`126 00:05:25,420 --> 00:05:25,980`
Ja, är det det?



`127 00:05:27,780 --> 00:05:28,780`
Sensitive content.



`128 00:05:28,860 --> 00:05:30,660`
Ja, men exakt. Det är ju en sån soptipp på X.



`129 00:05:30,760 --> 00:05:34,520`
Du ska ju se allt ifrån alla bottar och det dåliga på internet.



`130 00:05:34,940 --> 00:05:38,300`
Men för där vet jag att jag var inne och tittade på mitt Twitterkonto.



`131 00:05:38,460 --> 00:05:40,720`
Och då var det ju såhär, det blöras ju liksom.



`132 00:05:40,840 --> 00:05:42,280`
Och då måste du age verification.



`133 00:05:42,820 --> 00:05:44,020`
För att få lov att se dem.



`134 00:05:44,840 --> 00:05:46,460`
Så det är en tydlig trend i alla fall.



`135 00:05:46,680 --> 00:05:48,240`
Som vi märker.



`136 00:05:48,340 --> 00:05:52,900`
Nu har ju EU också gått ut och börjat arbeta på lagstiftning.



`137 00:05:52,900 --> 00:05:53,840`
Kring de här delarna.



`138 00:05:54,120 --> 00:05:58,620`
Och även försöka att införa någon form av central lösning.



`139 00:05:58,720 --> 00:06:02,000`
För att hantera identitet och åldersverifiering för EU-länderna.



`140 00:06:02,500 --> 00:06:05,760`
Ja, det som var i nyheterna idag då i GP2-artiklar.



`141 00:06:05,840 --> 00:06:07,440`
Det var ju just att EUs app.



`142 00:06:07,980 --> 00:06:09,880`
Den som ska vara så jävla bra, säger de.



`143 00:06:11,720 --> 00:06:14,740`
Highest level of integrity eller något sånt där.



`144 00:06:15,980 --> 00:06:19,320`
Den har nu testats, om jag fattar det hela rätt, i ett par länder.



`145 00:06:19,320 --> 00:06:22,700`
Och nu känner de att den börjar bli redo för att användas.



`146 00:06:22,700 --> 00:06:23,080`
På riktigt.



`147 00:06:23,440 --> 00:06:28,440`
Och det är väl det som jag tror länkas med Macron då igen.



`148 00:06:28,560 --> 00:06:32,720`
För att han och jag tror det var Spaniens premiärminister och någon till.



`149 00:06:32,860 --> 00:06:34,600`
De går nu upp på barrikaderna.



`150 00:06:34,820 --> 00:06:37,220`
Nu jävlar så inför vi det här i EU typ.



`151 00:06:38,040 --> 00:06:40,560`
Och vad är det här? Ska det här vara någon bank-ID-grej typ?



`152 00:06:40,800 --> 00:06:41,380`
Nej, det är det som är.



`153 00:06:41,500 --> 00:06:45,120`
Jag försökte googla runt det här hur det funkar.



`154 00:06:45,220 --> 00:06:46,940`
Men jag hade velat hitta appen liksom.



`155 00:06:47,040 --> 00:06:47,620`
Men jag hittade ingen.



`156 00:06:47,620 --> 00:06:49,860`
Jag kan försöka.



`157 00:06:50,400 --> 00:06:52,620`
Det är ju skillnaden mellan EU och...



`158 00:06:52,700 --> 00:06:56,920`
Till exempel UK är att det faktiskt finns en lösning så att säga.



`159 00:06:57,120 --> 00:07:01,480`
Som är tillhandahålls av staten, om vi nu kallar EU.



`160 00:07:02,040 --> 00:07:06,880`
För UK menar jag så har de bara lagstiftat och lämnat ut problembilden till operatörerna.



`161 00:07:07,080 --> 00:07:07,600`
Eller leverantörerna.



`162 00:07:07,940 --> 00:07:09,360`
Det funkar väl sådär.



`163 00:07:10,080 --> 00:07:18,040`
Men jag har ju inte hunnit hundra procent sätta mig in i exakt detaljerna när den funkar.



`164 00:07:18,040 --> 00:07:18,480`
Men?



`165 00:07:20,740 --> 00:07:22,040`
De försöker...



`166 00:07:22,700 --> 00:07:27,360`
De försöker splitta problembilden i ett antal olika frågor då.



`167 00:07:30,080 --> 00:07:35,940`
Du får alltså en EU Age Verification-app på din mobiltelefon.



`168 00:07:37,940 --> 00:07:40,940`
Påminner lite grann om hur vi använder bank-ID.



`169 00:07:41,940 --> 00:07:49,940`
Så att om du är inne på en sajt som kräver ID-verifiering eller åldersverifiering.



`170 00:07:50,580 --> 00:07:52,580`
Så kan du alltså hoppa över till appen.



`171 00:07:52,700 --> 00:07:55,100`
Och sen tillbaks när du har gjort verifieringen.



`172 00:07:56,940 --> 00:08:03,020`
Och de skryter ju med att den här ska vara Privacy Preserving.



`173 00:08:03,460 --> 00:08:15,080`
Så att målsättningen är ju att din identitet ska vara skyddad i den här operationen.



`174 00:08:16,260 --> 00:08:19,060`
Och det tror jag är under vissa antaganden.



`175 00:08:20,060 --> 00:08:22,500`
Till exempel att man typ litar.



`176 00:08:22,700 --> 00:08:26,140`
På att Age Verification-appen är god.



`177 00:08:26,880 --> 00:08:31,160`
Så i slutändan vad Relying Party.



`178 00:08:31,160 --> 00:08:35,640`
Det vill säga den tjänstleverantör som vill veta att du uppfyller ålderskraven.



`179 00:08:36,220 --> 00:08:39,300`
Så får den över ett signerat attest.



`180 00:08:39,440 --> 00:08:41,440`
Alltså typ tänk motsvarande en OOF-token.



`181 00:08:41,540 --> 00:08:42,960`
Eller en samhällsbiljett eller så.



`182 00:08:45,100 --> 00:08:51,260`
Och du får inte så mycket mer än att det är bundet till den session eller händelse som du är i.



`183 00:08:51,620 --> 00:08:52,160`
Och det får...



`184 00:08:52,700 --> 00:08:58,340`
Det ska finnas en utsaga då om att du är över age 16.



`185 00:08:58,520 --> 00:08:59,420`
Har de smätt till exempel då.



`186 00:08:59,420 --> 00:09:07,600`
Och du ska också kunna spara i den här appen lite olika test.



`187 00:09:07,980 --> 00:09:10,600`
Typ att du vill ha olika identifieringar.



`188 00:09:10,660 --> 00:09:14,660`
Så att du kan ha en identifiering där du säger att du är över 18.



`189 00:09:15,020 --> 00:09:17,020`
Och så ska du kunna välja att du har två stycken.



`190 00:09:17,100 --> 00:09:20,260`
Och ha en där du säger att du är över 23 och så.



`191 00:09:20,940 --> 00:09:22,420`
Så att du ska kunna...



`192 00:09:22,700 --> 00:09:26,380`
Vad är det jag inte fattar i...



`193 00:09:26,380 --> 00:09:31,920`
Vad är kopplingen mellan appen och sajten?



`194 00:09:32,220 --> 00:09:33,340`
Alltså hur...



`195 00:09:33,340 --> 00:09:34,440`
Om du fattar vad jag menar.



`196 00:09:34,500 --> 00:09:35,240`
Hur får jag...



`197 00:09:35,240 --> 00:09:36,520`
Hur kopplar jag...



`198 00:09:36,520 --> 00:09:38,140`
Om jag nu som användare.



`199 00:09:38,340 --> 00:09:39,140`
Som mot appen.



`200 00:09:40,020 --> 00:09:41,140`
Jag bryr mig inte om hur det går till.



`201 00:09:41,200 --> 00:09:43,060`
Men på något sätt så är det verifierad vem jag är.



`202 00:09:43,160 --> 00:09:44,680`
Förmodligen bank-ID liknande.



`203 00:09:45,100 --> 00:09:47,020`
Det vill säga det är koppling till mitt ID på något jävla sätt.



`204 00:09:47,140 --> 00:09:47,820`
In the back-end.



`205 00:09:49,240 --> 00:09:50,460`
Men jag måste...



`206 00:09:50,460 --> 00:09:52,520`
Hur kopplar du sajten och appen?



`207 00:09:52,520 --> 00:09:53,460`
Vem på ett rimligt sätt?



`208 00:09:53,760 --> 00:09:55,140`
Och så ska det vara privacy-preservive.



`209 00:09:55,340 --> 00:09:58,000`
Jag menar i de andra fall så är det ju typ...



`210 00:09:58,000 --> 00:09:59,560`
QR-kod-grejen då.



`211 00:09:59,600 --> 00:10:00,740`
Är det något sånt man kör då kanske?



`212 00:10:01,140 --> 00:10:02,780`
Ja QR-koden kan du ha om du vill.



`213 00:10:03,080 --> 00:10:04,760`
Alltså om du har ett annat...



`214 00:10:04,760 --> 00:10:05,720`
Alltså det går ju att göra det här.



`215 00:10:05,720 --> 00:10:08,740`
En identifierings-device och en...



`216 00:10:08,740 --> 00:10:09,260`
Ja.



`217 00:10:09,480 --> 00:10:11,760`
Och en website på en dator.



`218 00:10:11,860 --> 00:10:12,780`
Då använder du det.



`219 00:10:12,840 --> 00:10:14,000`
Då kan du scanna QR-koder och sånt.



`220 00:10:14,000 --> 00:10:16,040`
Annars kan du ju poppa appen lokalt.



`221 00:10:16,220 --> 00:10:16,660`
Ja just det.



`222 00:10:16,700 --> 00:10:17,200`
Det är så du gör.



`223 00:10:17,300 --> 00:10:17,960`
Ja men då är jag med.



`224 00:10:18,140 --> 00:10:20,360`
Det enda som är läskigt här är att man...



`225 00:10:20,360 --> 00:10:22,360`
Måste ju lita på de tjänsterna som...



`226 00:10:22,520 --> 00:10:23,680`
Som man konsumerar då.



`227 00:10:24,100 --> 00:10:25,940`
Att de sköter det här på ett bra sätt.



`228 00:10:27,320 --> 00:10:29,400`
Och du måste ju lita på båda...



`229 00:10:29,400 --> 00:10:30,580`
Båda leverantörerna.



`230 00:10:30,680 --> 00:10:30,860`
Exakt.



`231 00:10:30,940 --> 00:10:33,380`
Dels identitets...



`232 00:10:33,380 --> 00:10:34,540`
Identitets...



`233 00:10:34,540 --> 00:10:36,520`
Identitetsverifieringstjänsten.



`234 00:10:36,700 --> 00:10:38,560`
Och det är tjänsten som du vill komma åt.



`235 00:10:39,100 --> 00:10:40,360`
Och det vet man ju...



`236 00:10:40,360 --> 00:10:41,920`
Men grejen här med den...



`237 00:10:41,920 --> 00:10:43,780`
Med den kopplingen de har gjort där då.



`238 00:10:43,840 --> 00:10:46,220`
Det är ju det som skiljer sig från...



`239 00:10:46,220 --> 00:10:48,240`
Många UK-tjänster och sånt.



`240 00:10:48,240 --> 00:10:50,400`
Det är alltså att du har ju splittat...



`241 00:10:50,400 --> 00:10:52,240`
Identifiering...



`242 00:10:52,240 --> 00:10:52,500`
Från...



`243 00:10:52,520 --> 00:10:53,440`
En age-verification.



`244 00:10:53,780 --> 00:10:56,520`
Så att det finns ju en mellanlagning här där...



`245 00:10:57,820 --> 00:11:00,520`
Du bevisar för appen...



`246 00:11:01,280 --> 00:11:02,720`
Att du...



`247 00:11:02,720 --> 00:11:03,640`
Har din ålder och så.



`248 00:11:03,740 --> 00:11:05,700`
Och så får du någon sorts...



`249 00:11:05,700 --> 00:11:08,420`
Förmodligen inte egentligen för all framtid.



`250 00:11:08,560 --> 00:11:10,520`
Men du gör ett antal...



`251 00:11:11,160 --> 00:11:12,540`
En dans där du kan då...



`252 00:11:12,540 --> 00:11:14,500`
Du kan visa...



`253 00:11:14,500 --> 00:11:16,240`
Du kan till exempel använda ett pass.



`254 00:11:16,800 --> 00:11:18,660`
Och så kan du filma dig själv...



`255 00:11:18,660 --> 00:11:19,120`
För att visa.



`256 00:11:19,120 --> 00:11:21,120`
Och så kan jag jämföra att du är typ lik...



`257 00:11:21,120 --> 00:11:22,120`
Den bilden som finns på passet.



`258 00:11:22,520 --> 00:11:25,520`
Och så kan du...



`259 00:11:25,520 --> 00:11:27,620`
I någon sorts övning då...



`260 00:11:27,620 --> 00:11:28,840`
Så kan du få...



`261 00:11:28,840 --> 00:11:31,900`
Kan du få att ett age-bevis...



`262 00:11:31,900 --> 00:11:33,360`
Ligger på din mobiltelefon...



`263 00:11:33,360 --> 00:11:34,500`
Över en längre tid då.



`264 00:11:34,760 --> 00:11:36,980`
Det är också bra att flika in här.



`265 00:11:37,240 --> 00:11:39,520`
Det är ju inte så många EU-länder som har samma...



`266 00:11:40,960 --> 00:11:41,780`
Ja men...



`267 00:11:41,780 --> 00:11:43,720`
Aggregerad identitet som vi har här.



`268 00:11:43,820 --> 00:11:44,780`
Som med BankID till exempel.



`269 00:11:44,900 --> 00:11:47,260`
Som har blivit en de facto standard i Sverige på något sätt.



`270 00:11:47,380 --> 00:11:48,580`
För identifiering online.



`271 00:11:49,240 --> 00:11:51,280`
Det är ju väldigt vanligt som Peter säger här nu.



`272 00:11:51,280 --> 00:11:51,780`
Att man...



`273 00:11:51,780 --> 00:11:53,200`
Sätter sig vid webbkameran.



`274 00:11:53,280 --> 00:11:54,140`
Viker upp passet.



`275 00:11:54,260 --> 00:11:57,020`
Och så ler man lite snyggt in i en tjänst.



`276 00:11:57,120 --> 00:11:59,140`
Och så skickas det iväg.



`277 00:11:59,260 --> 00:12:01,660`
Och så är det en algoritm kanske då som...



`278 00:12:01,660 --> 00:12:02,420`
Validerar det vidare.



`279 00:12:02,560 --> 00:12:03,480`
Det ser det på riktigt ut.



`280 00:12:03,900 --> 00:12:04,080`
Mm.



`281 00:12:04,540 --> 00:12:07,520`
Och grejen är att det här ska kunna göras...



`282 00:12:07,520 --> 00:12:09,280`
På något sätt då...



`283 00:12:10,360 --> 00:12:14,280`
I och med att du har...



`284 00:12:15,160 --> 00:12:16,060`
Liksom...



`285 00:12:16,060 --> 00:12:17,820`
Det där finns ju flera bolag som gör idag.



`286 00:12:18,120 --> 00:12:20,280`
Ja men din mobiltelefon kan ju läsa koden...



`287 00:12:20,420 --> 00:12:21,280`
För att prata...



`288 00:12:21,780 --> 00:12:23,600`
Om NFC på ditt pass och sånt.



`289 00:12:23,680 --> 00:12:25,880`
Så kan du aktivera det.



`290 00:12:26,640 --> 00:12:27,860`
Och då kan du bildmatcha.



`291 00:12:28,080 --> 00:12:29,920`
Och du ska också kunna på något sätt...



`292 00:12:30,700 --> 00:12:33,920`
Använda andra leverantörer.



`293 00:12:34,540 --> 00:12:35,560`
För det är...



`294 00:12:35,560 --> 00:12:38,420`
För den lösningen är nog bättre än många av de här.



`295 00:12:38,900 --> 00:12:39,860`
För dels är ju då...



`296 00:12:39,860 --> 00:12:42,160`
Att man har en fotokopia på ett pass eller ett körkort.



`297 00:12:42,680 --> 00:12:44,440`
Men det kan ju också vara såna här diffusa grejer.



`298 00:12:44,560 --> 00:12:46,560`
Som att vi vill ha en e-utility-bild.



`299 00:12:46,680 --> 00:12:47,760`
Alltså typ elräkningen.



`300 00:12:47,880 --> 00:12:49,260`
Spanien vet jag har ett sånt flöde.



`301 00:12:49,460 --> 00:12:51,280`
Där man visar proof of address.



`302 00:12:51,280 --> 00:12:53,480`
Och proof of origin med...



`303 00:12:53,480 --> 00:12:55,640`
En räkning på någonting man har köpt.



`304 00:12:56,260 --> 00:12:57,780`
Vilket det också är...



`305 00:12:57,780 --> 00:12:59,020`
Ja...



`306 00:12:59,020 --> 00:12:59,980`
Lite läskigt.



`307 00:13:00,000 --> 00:13:00,860`
Inte superexakt.



`308 00:13:01,400 --> 00:13:03,020`
Då är det som Peter säger här.



`309 00:13:03,180 --> 00:13:04,320`
10 000 nivåer bättre.



`310 00:13:04,460 --> 00:13:05,240`
Det vill säga...



`311 00:13:05,240 --> 00:13:06,920`
NFC-delen i ditt pass.



`312 00:13:07,040 --> 00:13:08,180`
Det är ju en PKI-infrastruktur.



`313 00:13:08,280 --> 00:13:09,480`
Det är ju en jättebra grej.



`314 00:13:09,560 --> 00:13:10,140`
Men vet du Peter.



`315 00:13:10,260 --> 00:13:11,760`
Är det här...



`316 00:13:11,760 --> 00:13:13,060`
När de nu ändå bygger den här appen.



`317 00:13:13,320 --> 00:13:16,180`
Kommer det vara så att den bara gör de här...



`318 00:13:16,180 --> 00:13:17,280`
Ganska vaga...



`319 00:13:18,200 --> 00:13:19,760`
Åldersattesteringarna då?



`320 00:13:19,800 --> 00:13:20,840`
Eller kommer man passa på?



`321 00:13:20,840 --> 00:13:21,240`
Och även...



`322 00:13:21,240 --> 00:13:22,740`
Att man bygger en identitetsfunktion här?



`323 00:13:25,680 --> 00:13:28,640`
Det här kommer ju med...



`324 00:13:28,640 --> 00:13:31,240`
Det hänger ihop med...



`325 00:13:31,240 --> 00:13:33,240`
Den här EID...



`326 00:13:33,240 --> 00:13:34,120`
Vad heter den?



`327 00:13:34,380 --> 00:13:35,020`
EIDAS?



`328 00:13:35,200 --> 00:13:36,400`
Eller någonting...



`329 00:13:36,400 --> 00:13:39,380`
Någon sorts EU-lag-framework.



`330 00:13:39,400 --> 00:13:41,520`
Kring hur identitetshandlingar ska funka.



`331 00:13:42,260 --> 00:13:43,340`
Så att...



`332 00:13:43,340 --> 00:13:45,280`
Jag tror mycket väl att man långsiktigt...



`333 00:13:45,280 --> 00:13:47,240`
Vill ha en typ...



`334 00:13:48,040 --> 00:13:50,460`
En bank-ID-liknande funktion för EU.



`335 00:13:50,460 --> 00:13:51,220`
Vill man säkert.



`336 00:13:51,240 --> 00:13:52,820`
Det finns ju även en...



`337 00:13:52,820 --> 00:13:55,400`
Money-grunka.



`338 00:13:55,580 --> 00:13:56,340`
Som EU jobbar på också.



`339 00:13:57,000 --> 00:13:58,720`
Men specifikt Age Verification.



`340 00:13:59,420 --> 00:14:01,000`
Ska vara sin egen app.



`341 00:14:01,520 --> 00:14:02,880`
Och ska...



`342 00:14:02,880 --> 00:14:05,380`
Den appen ska inte behöva veta...



`343 00:14:05,380 --> 00:14:05,780`
Vem du är.



`344 00:14:06,140 --> 00:14:08,500`
Utan den ska bara behöva veta att...



`345 00:14:08,500 --> 00:14:11,160`
Den här nuvarande användaren på telefonen.



`346 00:14:12,200 --> 00:14:13,960`
Den vet ju att den får använda...



`347 00:14:13,960 --> 00:14:15,120`
Det här utsagan.



`348 00:14:15,120 --> 00:14:16,120`
Om hur gammal den är.



`349 00:14:16,380 --> 00:14:19,400`
Och den är godkänd någon gång tidigare.



`350 00:14:19,400 --> 00:14:21,100`
Men appen kommer väl typiskt...



`351 00:14:21,100 --> 00:14:22,060`
Att veta hur gammal du är.



`352 00:14:22,140 --> 00:14:22,800`
Och exakt vem du är.



`353 00:14:23,080 --> 00:14:26,360`
Om du blippar den mot NFC.



`354 00:14:26,760 --> 00:14:28,220`
Jo, precis.



`355 00:14:28,560 --> 00:14:30,000`
Du har två frågor där.



`356 00:14:30,060 --> 00:14:31,280`
Det ena är...



`357 00:14:31,280 --> 00:14:33,040`
Vad den faktiskt vet.



`358 00:14:33,120 --> 00:14:34,900`
Versus vad den kan veta.



`359 00:14:36,280 --> 00:14:38,540`
Jag är så jävla nojig för det här.



`360 00:14:38,740 --> 00:14:41,140`
För det är ju absolut så...



`361 00:14:41,140 --> 00:14:43,000`
Jag gillar idén konceptuellt.



`362 00:14:43,060 --> 00:14:44,220`
Det vill säga att vi kan ha en...



`363 00:14:44,220 --> 00:14:45,600`
Out of bound-idé då.



`364 00:14:45,600 --> 00:14:46,860`
Där vi kan skapa en...



`365 00:14:46,860 --> 00:14:48,680`
En session.



`366 00:14:49,160 --> 00:14:50,780`
En signerad grunka.



`367 00:14:51,100 --> 00:14:52,500`
Och någonting med någonting att göra.



`368 00:14:52,920 --> 00:14:55,240`
I ett kontext där den inte är byggd för att vara.



`369 00:14:55,820 --> 00:14:58,680`
Men det finns ju ingenting som säger att den informationen inte kan...



`370 00:14:58,680 --> 00:15:00,360`
Ta vägen någonstans.



`371 00:15:01,000 --> 00:15:01,280`
Precis.



`372 00:15:01,460 --> 00:15:05,640`
För grejen är att om vi väljer att vi inte litar på EU-infrastrukturen.



`373 00:15:05,740 --> 00:15:07,080`
Och vi inte litar på appen.



`374 00:15:07,700 --> 00:15:10,180`
Så kommer en massa...



`375 00:15:10,180 --> 00:15:12,720`
Då tror jag att många av de här privacy-lufterna inte håller.



`376 00:15:13,020 --> 00:15:14,160`
Men...



`377 00:15:14,160 --> 00:15:16,460`
Jag tror att den är privacy-preserving.



`378 00:15:16,560 --> 00:15:18,880`
Under antagandet att...



`379 00:15:18,880 --> 00:15:20,020`
Appen inte är ond.



`380 00:15:20,220 --> 00:15:20,680`
Och infrastrukturen...



`381 00:15:21,100 --> 00:15:22,640`
Infrastrukturen runt den inte är ond.



`382 00:15:22,700 --> 00:15:24,500`
Det är nog med i grundantagandet.



`383 00:15:24,620 --> 00:15:26,480`
Den ska inte läcka några...



`384 00:15:26,480 --> 00:15:29,520`
Privacy-detaljer till sajterna du ska logga in på.



`385 00:15:29,520 --> 00:15:31,060`
Men vad de säger är ju liksom till exempel att...



`386 00:15:31,060 --> 00:15:34,140`
När du identifierar med pass för att skapa en...



`387 00:15:34,140 --> 00:15:36,420`
En edge i den här edge-appen.



`388 00:15:37,820 --> 00:15:40,300`
Så ska den ju kasta bort...



`389 00:15:40,300 --> 00:15:42,000`
Allting som stod på passet.



`390 00:15:42,120 --> 00:15:42,780`
Ditt foto.



`391 00:15:43,400 --> 00:15:45,920`
Den videon som du tog för att bevisa att...



`392 00:15:45,920 --> 00:15:48,100`
Du var den personen som du hade passet till.



`393 00:15:48,260 --> 00:15:49,820`
Det ska ju tydligt inte vara med i...



`394 00:15:49,820 --> 00:15:50,820`
I resultatet.



`395 00:15:51,100 --> 00:15:53,140`
Nej, så om...



`396 00:15:53,140 --> 00:15:54,340`
Metadatat ska ju vara borta.



`397 00:15:54,700 --> 00:15:56,480`
Om appen funkar som den ska.



`398 00:15:56,740 --> 00:15:58,720`
Så ska liksom...



`399 00:15:58,720 --> 00:16:00,620`
De här passinformationen och sånt ska försvinna.



`400 00:16:00,620 --> 00:16:02,540`
Ja, för jag får ju kalla kårar direkt så här.



`401 00:16:02,660 --> 00:16:04,420`
Jag menar...



`402 00:16:04,420 --> 00:16:05,820`
Ja, men en VPN-tunnel då.



`403 00:16:06,820 --> 00:16:07,760`
Så här...



`404 00:16:07,760 --> 00:16:10,760`
De associationerna kommer ju att korreleras och aggregeras



`405 00:16:10,760 --> 00:16:12,040`
på ett och samma ställe alltid.



`406 00:16:12,720 --> 00:16:14,900`
För jag kommer ju gå och fråga tjänsten



`407 00:16:14,900 --> 00:16:15,900`
efter mitt lilla frö då.



`408 00:16:15,980 --> 00:16:19,340`
Eller om jag behöver göra den signeringsvalsen



`409 00:16:19,340 --> 00:16:20,540`
varje gång jag besöker en sajt.



`410 00:16:21,100 --> 00:16:22,140`
Nej, men det var nog det Peter sa.



`411 00:16:22,280 --> 00:16:25,400`
Det där gör man one time och sen gäller den...



`412 00:16:25,400 --> 00:16:26,660`
Jag hoppas man ju inte...



`413 00:16:26,660 --> 00:16:29,400`
För då funkar det ju inte riktigt som bank i det då egentligen.



`414 00:16:29,540 --> 00:16:30,740`
Utan då har man liksom en...



`415 00:16:30,740 --> 00:16:33,840`
Det blir som en passkey som gäller tills den är revokad på något sätt.



`416 00:16:34,680 --> 00:16:35,200`
Men då...



`417 00:16:35,200 --> 00:16:36,640`
Frågan är hur...



`418 00:16:36,640 --> 00:16:37,520`
Men det är läskigt då.



`419 00:16:38,440 --> 00:16:40,760`
Säger du att man är på en sajt, den som trackar dig.



`420 00:16:41,280 --> 00:16:44,220`
Och så säger den, ja men ange din lilla sektion här då.



`421 00:16:44,280 --> 00:16:47,060`
Även om den då ligger inom kaka, inom en store state



`422 00:16:47,060 --> 00:16:49,660`
eller om jag behöver ange någon siffer, kombination.



`423 00:16:50,220 --> 00:16:50,940`
Så är det ju...



`424 00:16:50,940 --> 00:16:53,360`
Det är ju väldigt enkelt att göra korrelationsanalys



`425 00:16:53,360 --> 00:16:54,640`
för vad jag är och var jag kommer ifrån.



`426 00:16:55,740 --> 00:16:57,760`
Ja, man kan ju säga så här, du trackar en perspektiv



`427 00:16:57,760 --> 00:16:59,540`
så ger du...



`428 00:16:59,540 --> 00:17:01,300`
Du ger tjänsten



`429 00:17:01,300 --> 00:17:03,080`
mer information än den hade tidigare.



`430 00:17:03,360 --> 00:17:03,840`
Mycket mer.



`431 00:17:05,060 --> 00:17:07,320`
Potentiellt väldigt känslig information om man nu lyckas



`432 00:17:07,320 --> 00:17:08,600`
korrelera de här sakerna på rätt sätt.



`433 00:17:08,600 --> 00:17:10,480`
Eller om du har en läcka på någon...



`434 00:17:10,480 --> 00:17:12,620`
Jag tänker bara så här, nästa steg blir ju att



`435 00:17:12,620 --> 00:17:14,280`
det kommer ju finnas en jävla plugin i någon browser



`436 00:17:14,280 --> 00:17:15,920`
och så den browsern



`437 00:17:15,920 --> 00:17:18,280`
surfar på internet på många olika sätt.



`438 00:17:19,220 --> 00:17:20,600`
Och det känns ju också läskigt.



`439 00:17:20,940 --> 00:17:21,720`
Läckigt som fasiken.



`440 00:17:22,040 --> 00:17:24,240`
Jag skulle bara vilja gå tillbaka lite till



`441 00:17:24,240 --> 00:17:25,460`
de här olika lösningarna vi har sett.



`442 00:17:25,540 --> 00:17:28,580`
För vi har diskuterat den som eventuellt är på gång inom EU



`443 00:17:28,580 --> 00:17:30,200`
eller det som är på gång inom EU och Sverige.



`444 00:17:31,020 --> 00:17:33,160`
Sen har vi ju sett det som har...



`445 00:17:33,160 --> 00:17:34,960`
Jag vet inte exakt hur Australien har gjort.



`446 00:17:36,020 --> 00:17:37,360`
De har väl contentfilter, va?



`447 00:17:37,400 --> 00:17:37,860`
Har de inte det?



`448 00:17:38,380 --> 00:17:39,280`
Jag misstänker att det är något sånt.



`449 00:17:39,380 --> 00:17:41,740`
I USA vet jag att jag har hört att...



`450 00:17:41,740 --> 00:17:45,080`
Där hade det väl varit lite mer att de har lagt ansvaret på tjänsterna.



`451 00:17:45,080 --> 00:17:45,220`
Ja.



`452 00:17:45,900 --> 00:17:47,440`
Lite som i England då, misstänker jag.



`453 00:17:48,840 --> 00:17:50,440`
England har väl det rätt av, tror jag.



`454 00:17:50,580 --> 00:17:50,900`
Det är...



`455 00:17:50,940 --> 00:17:52,860`
Vilket är ganska problematiskt för att



`456 00:17:52,860 --> 00:17:56,180`
då har det ju helt plötsligt en massa företag som säger



`457 00:17:56,180 --> 00:17:58,980`
vi gör åldersverifiering utifrån



`458 00:17:58,980 --> 00:18:02,100`
bilder på användaren och sådana här saker som...



`459 00:18:02,100 --> 00:18:04,280`
Ja, bilder på användaren eller origin av användaren.



`460 00:18:04,880 --> 00:18:07,840`
Egentligen inte knutet till en central identitet.



`461 00:18:07,920 --> 00:18:08,320`
Alls.



`462 00:18:08,740 --> 00:18:11,960`
Utan ta ett bild på ditt ansikte så avgör vi



`463 00:18:11,960 --> 00:18:13,700`
ifall du är gammal nog, exempelvis.



`464 00:18:14,060 --> 00:18:14,900`
Sådana här saker.



`465 00:18:15,160 --> 00:18:18,860`
Och det är ju bara upplagt för katastrof.



`466 00:18:19,300 --> 00:18:20,820`
Och det kommer det ju vara också.



`467 00:18:20,940 --> 00:18:23,100`
Dels att folk kan kringgå det, det är ju relativt enkelt.



`468 00:18:23,320 --> 00:18:25,440`
Men dels också att du har en massa 3D-parts-företag



`469 00:18:25,440 --> 00:18:27,860`
som nu sitter på känslig data, inklusive



`470 00:18:27,860 --> 00:18:29,540`
biometri och sådana här saker



`471 00:18:29,540 --> 00:18:31,680`
om användare som försöker komma åt



`472 00:18:31,680 --> 00:18:33,120`
potentiellt känslig information.



`473 00:18:33,640 --> 00:18:33,820`
Ja.



`474 00:18:35,160 --> 00:18:37,280`
Så från det perspektivet så är ju



`475 00:18:37,280 --> 00:18:39,320`
åtminstone ur ett tekniskt



`476 00:18:39,320 --> 00:18:41,860`
synpunkt den EU-modellen



`477 00:18:41,860 --> 00:18:43,980`
med en central ID-infrastruktur



`478 00:18:43,980 --> 00:18:44,740`
bättre.



`479 00:18:45,540 --> 00:18:47,720`
Du har i alla fall möjligheten att göra det mer anonymt.



`480 00:18:48,040 --> 00:18:50,720`
Sen är väl frågan om den större problembilden



`481 00:18:50,940 --> 00:18:52,780`
är det här någonting vi egentligen



`482 00:18:52,780 --> 00:18:53,960`
vill ha överhuvudtaget?



`483 00:18:54,020 --> 00:18:56,460`
Det var lite det jag satt och funderade på initialt



`484 00:18:56,460 --> 00:18:58,000`
när jag tänkte på det här.



`485 00:18:59,720 --> 00:19:01,060`
Varför är det här ens



`486 00:19:01,060 --> 00:19:01,980`
en bra idé?



`487 00:19:03,020 --> 00:19:04,620`
Jag menar, jag köper att



`488 00:19:04,620 --> 00:19:07,100`
det blir ett cirkel



`489 00:19:07,100 --> 00:19:08,620`
som många hör. För jag tänker såhär



`490 00:19:08,620 --> 00:19:10,960`
är det skrivet i lag att vissa saker



`491 00:19:10,960 --> 00:19:12,420`
är åldersgräns på.



`492 00:19:12,700 --> 00:19:13,940`
Då måste det ju verifieras på något.



`493 00:19:14,080 --> 00:19:16,940`
Och det brukar man göra med ett ID, typ köpa sprit på bolaget



`494 00:19:16,940 --> 00:19:17,700`
och sådana grejer.



`495 00:19:19,460 --> 00:19:20,640`
Så det är väl där vi måste



`496 00:19:20,940 --> 00:19:23,020`
börja på något sätt. Inte implementationen



`497 00:19:23,020 --> 00:19:24,180`
utan är det



`498 00:19:24,180 --> 00:19:27,120`
i det här fallet då så är det ju social media



`499 00:19:27,120 --> 00:19:28,120`
primärt, tror jag va?



`500 00:19:28,540 --> 00:19:31,200`
Är det rimligt att lagstifta



`501 00:19:31,200 --> 00:19:33,260`
att 15-



`502 00:19:33,260 --> 00:19:34,780`
eller 16-åringar inte



`503 00:19:34,780 --> 00:19:36,360`
får använda social media?



`504 00:19:36,880 --> 00:19:39,040`
Och hur drar man gränsen kan man ju också



`505 00:19:39,040 --> 00:19:40,440`
fråga sig. Vad är social media då?



`506 00:19:40,640 --> 00:19:42,600`
Vad är det vi inkluderar i det?



`507 00:19:43,240 --> 00:19:44,980`
För med så här långt då så har det ju



`508 00:19:44,980 --> 00:19:47,180`
nu ramlar vi snabbt in i hur det är fördelar



`509 00:19:47,180 --> 00:19:48,840`
och risker och problembild.



`510 00:19:48,840 --> 00:19:50,860`
Men så här långt har det varit föräldrar



`511 00:19:50,860 --> 00:19:51,860`
ansvar att styra det här.



`512 00:19:53,740 --> 00:19:54,840`
Vissa frågor bestämmer



`513 00:19:54,840 --> 00:19:56,100`
staten om, det vill säga



`514 00:19:56,100 --> 00:19:58,340`
köra bil, rösta, dricka sprit.



`515 00:19:59,780 --> 00:20:00,880`
Men här



`516 00:20:00,880 --> 00:20:02,600`
är det då föräldrarna som bestämmer om



`517 00:20:02,600 --> 00:20:04,340`
om han får social media och mobiltelefoner eller inte.



`518 00:20:05,100 --> 00:20:06,700`
Jag kan ju hävda att i viss mån så har ju föräldrarna



`519 00:20:06,700 --> 00:20:08,840`
failat. Alltså okej,



`520 00:20:09,040 --> 00:20:10,820`
människor har ju inte dött i partiet men ut kanske



`521 00:20:10,820 --> 00:20:12,500`
så att så jävla mycket kanske de inte har failat.



`522 00:20:12,960 --> 00:20:14,740`
Men konsumtionen av



`523 00:20:14,740 --> 00:20:16,960`
social media bland ungdomar är ju rätt hög.



`524 00:20:17,740 --> 00:20:18,640`
Och det är ju inte



`525 00:20:18,640 --> 00:20:20,400`
enbart positivt.



`526 00:20:20,860 --> 00:20:22,980`
Men det är ju också en produkt av tiden. Man får tänka



`527 00:20:22,980 --> 00:20:25,160`
på det här. Tittar man historiskt



`528 00:20:25,160 --> 00:20:26,780`
så finns det ju andra saker och ting som har varit



`529 00:20:26,780 --> 00:20:29,220`
väldigt hemska. Rockmusik.



`530 00:20:29,420 --> 00:20:29,760`
Ja, exakt.



`531 00:20:31,640 --> 00:20:34,340`
Man får vara försiktig här.



`532 00:20:34,480 --> 00:20:36,660`
Jag är ju en väldigt



`533 00:20:36,660 --> 00:20:38,880`
jag vurmar ju jättemycket för privacy men framförallt



`534 00:20:38,880 --> 00:20:40,920`
yttrandefrihet. Och här är ju då



`535 00:20:40,920 --> 00:20:42,940`
så här, vi ändrar våran



`536 00:20:42,940 --> 00:20:45,200`
vad man säger här då, media idag.



`537 00:20:46,160 --> 00:20:46,700`
Publik, alltså



`538 00:20:46,700 --> 00:20:48,820`
tidningar och så. Vi konsumerar



`539 00:20:48,820 --> 00:20:50,740`
nyheter om en



`540 00:20:50,740 --> 00:20:52,860`
nationssponsrade, höger-vänstervridet



`541 00:20:52,860 --> 00:20:53,500`
hur det än är.



`542 00:20:54,560 --> 00:20:56,680`
Alltså, funktionen



`543 00:20:56,680 --> 00:20:58,680`
eller produkten tidning, den ser ju inte



`544 00:20:58,680 --> 00:21:00,600`
likadan ut idag. Så det är så



`545 00:21:00,600 --> 00:21:02,480`
att vi kan konsumera opinion



`546 00:21:02,480 --> 00:21:04,740`
och så vidare. Det finns ju inte



`547 00:21:04,740 --> 00:21:06,540`
på samma sätt. Det görs ju via



`548 00:21:06,540 --> 00:21:08,580`
sociala medier. Så frågan är



`549 00:21:08,580 --> 00:21:10,720`
om ska man förbjuda



`550 00:21:10,720 --> 00:21:12,540`
eller ska man moderera eller ska man



`551 00:21:12,540 --> 00:21:14,700`
göra någon kombination? Vi kan väl också



`552 00:21:14,700 --> 00:21:16,540`
konstatera. Är förbud rätt väg liksom?



`553 00:21:16,880 --> 00:21:18,920`
En direkt effekt av



`554 00:21:18,920 --> 00:21:20,680`
att man börjar göra



`555 00:21:20,740 --> 00:21:22,500`
sånt här inom EU och sånt



`556 00:21:22,500 --> 00:21:23,300`
det är ju att



`557 00:21:23,300 --> 00:21:26,560`
det kommer ju finnas en marknad för



`558 00:21:26,560 --> 00:21:28,640`
social media-sajter med



`559 00:21:28,640 --> 00:21:30,480`
mera som tillåter ungar



`560 00:21:30,480 --> 00:21:32,300`
som inte gör de här kollarna.



`561 00:21:32,520 --> 00:21:34,340`
Alltså, det kommer ju ske med en gång.



`562 00:21:35,200 --> 00:21:36,760`
Alltså, det är ju liksom inget



`563 00:21:36,760 --> 00:21:38,340`
The dark youth web.



`564 00:21:38,680 --> 00:21:40,600`
Men så är det ju. Om du begränsar du



`565 00:21:40,600 --> 00:21:42,500`
någonting så kommer ju en uppsjö av alternativ



`566 00:21:42,500 --> 00:21:44,580`
dyka upp. När vi var 15 år



`567 00:21:44,580 --> 00:21:46,020`
så hade ju inte vi accepterat att



`568 00:21:46,020 --> 00:21:47,740`
någonting inte lät oss använda.



`569 00:21:47,740 --> 00:21:49,820`
Nej, folk kommer ju ta sig runt



`570 00:21:49,820 --> 00:21:50,620`
att det är ingen särskild sak.



`571 00:21:50,740 --> 00:21:53,280`
Vi kan ju bara vända på det och säga, ja men alla runt det här bordet



`572 00:21:53,280 --> 00:21:55,620`
laddade ju ner både musik och film



`573 00:21:55,620 --> 00:21:57,460`
för det var så man konsumerade för att



`574 00:21:57,460 --> 00:21:59,600`
alternativet var bakom en



`575 00:21:59,600 --> 00:22:01,660`
paywall liksom. Men nu



`576 00:22:01,660 --> 00:22:03,620`
så ändrar man hela konsumtionsmöstret så nu



`577 00:22:03,620 --> 00:22:05,700`
har alla här runt det här bordet streaming för att



`578 00:22:05,700 --> 00:22:07,800`
det blir mycket lättare att konsumera saker.



`579 00:22:08,380 --> 00:22:09,820`
Så vi ändrade affärsmodellen lite.



`580 00:22:10,460 --> 00:22:11,600`
Och nu tillämpar man det



`581 00:22:11,600 --> 00:22:14,080`
då att man ska förbjuda folk att använda teknik.



`582 00:22:14,620 --> 00:22:15,680`
Det tycker jag inte



`583 00:22:15,680 --> 00:22:17,120`
är rätt väg att gå.



`584 00:22:17,520 --> 00:22:19,700`
Sen så håller jag med om att det finns jättemycket studier



`585 00:22:19,700 --> 00:22:20,700`
på hur skadligt



`586 00:22:20,740 --> 00:22:23,560`
mitt missbruk också är. Inte bara kidsen.



`587 00:22:23,920 --> 00:22:25,720`
Alltså jag har också ett jättemissbruk



`588 00:22:25,720 --> 00:22:26,980`
där man kan sitta liksom och bara så här



`589 00:22:26,980 --> 00:22:29,900`
vad fan är det som händer nu? Här har jag suttit i 20 minuter och kollat på



`590 00:22:29,900 --> 00:22:31,080`
katter.



`591 00:22:32,120 --> 00:22:34,220`
Det är en av de bättre



`592 00:22:34,220 --> 00:22:35,360`
dåliga sakerna idag.



`593 00:22:36,180 --> 00:22:37,540`
Det kan jag säga



`594 00:22:37,540 --> 00:22:39,120`
att samhället konstaterar att



`595 00:22:39,120 --> 00:22:41,800`
vi har en problem att tekniknivå



`596 00:22:41,800 --> 00:22:42,840`
och kompetensen



`597 00:22:42,840 --> 00:22:45,200`
sjunker de yngre generationerna.



`598 00:22:45,340 --> 00:22:47,100`
Så nu gör vi den här satsningen



`599 00:22:47,100 --> 00:22:49,660`
för att tvinga ungdomarna att lära sig teknik.



`600 00:22:50,080 --> 00:22:50,580`
Det kommer att vara så.



`601 00:22:50,740 --> 00:22:52,960`
Det kommer att bli så jävla mycket



`602 00:22:52,960 --> 00:22:55,120`
duxiga unga när de börjar



`603 00:22:55,120 --> 00:22:56,740`
leka den här dansen med



`604 00:22:56,740 --> 00:22:59,180`
banivation och grejer.



`605 00:23:00,140 --> 00:23:00,880`
Det är ju så smart.



`606 00:23:00,960 --> 00:23:02,620`
Det är så vi kommer att få nästa generations hackers.



`607 00:23:03,140 --> 00:23:04,560`
Men är det någon som har tittat på det? Hur



`608 00:23:04,560 --> 00:23:06,520`
motiveras de här förbuden?



`609 00:23:06,900 --> 00:23:08,280`
Vi måste tänka på de små barnen.



`610 00:23:09,180 --> 00:23:10,500`
Man får vara lite mer



`611 00:23:10,500 --> 00:23:12,920`
granulära och nyanserade än så.



`612 00:23:13,080 --> 00:23:14,240`
Inte om man heter Ylva.



`613 00:23:14,240 --> 00:23:15,540`
Grejen är att det får mig



`614 00:23:15,540 --> 00:23:18,220`
det här ger mig smaken



`615 00:23:18,220 --> 00:23:19,260`
av chat-control.



`616 00:23:20,740 --> 00:23:22,960`
Jag känner lite likadant



`617 00:23:22,960 --> 00:23:24,980`
för att det finns ingenting som säger att man inte bygger



`618 00:23:24,980 --> 00:23:26,300`
funktionalitet uppe på det här.



`619 00:23:27,300 --> 00:23:29,120`
Jag tog i någon av artiklarna som jag



`620 00:23:29,120 --> 00:23:30,980`
läste kring detta där de



`621 00:23:30,980 --> 00:23:33,060`
om det var Electronic



`622 00:23:33,060 --> 00:23:34,880`
Frontier Foundation



`623 00:23:34,880 --> 00:23:37,060`
Men mental murbräcka



`624 00:23:37,060 --> 00:23:38,520`
är väl en av



`625 00:23:38,520 --> 00:23:40,880`
anklagelserna. Vi börjar



`626 00:23:40,880 --> 00:23:42,860`
med att lära sig folk att acceptera



`627 00:23:42,860 --> 00:23:45,080`
internet är inte längre



`628 00:23:45,080 --> 00:23:46,960`
fritt utan du måste identifiera dig



`629 00:23:46,960 --> 00:23:48,580`
verifiera dig för att komma åt det.



`630 00:23:49,020 --> 00:23:50,700`
Och det har det ju inte varit på länge men



`631 00:23:50,740 --> 00:23:52,280`
men alltså fingerprinting och tracking.



`632 00:23:52,300 --> 00:23:54,420`
Har vi de här sakerna på plats?



`633 00:23:54,840 --> 00:23:56,560`
Det är någon artikel som jag läste som



`634 00:23:56,560 --> 00:23:58,940`
har åldrats lite nu då med tanke på



`635 00:23:58,940 --> 00:24:00,560`
det senaste valet i Ungern



`636 00:24:00,560 --> 00:24:03,020`
som ju faktiskt gick åt rätt håll



`637 00:24:03,020 --> 00:24:04,640`
för en gång så det är första gången på 16 år.



`638 00:24:04,900 --> 00:24:06,740`
Ja, väldigt bra. Inte om du frågar



`639 00:24:06,740 --> 00:24:08,700`
den rumänska taxichauffören som körde mig igår.



`640 00:24:09,220 --> 00:24:10,360`
Han följer inte med.



`641 00:24:10,820 --> 00:24:12,960`
Nej men vi kan inte ta alla våra åsikter från honom.



`642 00:24:14,800 --> 00:24:16,880`
Nej men i den artikeln jag läste här så stod de bara upp



`643 00:24:16,880 --> 00:24:18,880`
som ett exempel om vi nu stiftar den här



`644 00:24:18,880 --> 00:24:20,560`
infrastrukturen i EU. Vad skulle



`645 00:24:20,560 --> 00:24:22,600`
stoppa egentligen en



`646 00:24:22,600 --> 00:24:24,340`
regim som Orbans då



`647 00:24:24,340 --> 00:24:27,140`
från att använda liknande för att begränsa



`648 00:24:27,140 --> 00:24:28,840`
tillgång till information



`649 00:24:28,840 --> 00:24:30,840`
för LGBTQI\+.



`650 00:24:31,420 --> 00:24:33,140`
Ja men det du säger nu är



`651 00:24:33,140 --> 00:24:35,000`
helt rätt och det kommer ju också vara en svart låda



`652 00:24:35,000 --> 00:24:36,640`
där man inte har insyn.



`653 00:24:36,800 --> 00:24:38,080`
Men tittar man på



`654 00:24:38,080 --> 00:24:40,680`
både Storbritannien och



`655 00:24:40,680 --> 00:24:42,320`
och ännu mer



`656 00:24:42,320 --> 00:24:44,460`
delar av USA så är ju



`657 00:24:44,460 --> 00:24:46,920`
det är ju jättemycket som är känsligt som



`658 00:24:46,920 --> 00:24:48,460`
unga inte borde få läsa om.



`659 00:24:48,900 --> 00:24:49,920`
Exakt, enligt dem.



`660 00:24:50,560 --> 00:24:52,060`
Och definitivt...



`661 00:24:52,060 --> 00:24:54,820`
Men att lägga, vi kan prata snabbt om det här



`662 00:24:54,820 --> 00:24:56,800`
om UKs DNS-filtrering



`663 00:24:56,800 --> 00:24:58,580`
helt enkelt, det vill säga att man måste ha



`664 00:24:58,580 --> 00:25:00,660`
age verification för att nå vissa...



`665 00:25:00,660 --> 00:25:03,160`
Det är väl framförallt gaming och adult content



`666 00:25:03,160 --> 00:25:04,080`
alltså porr liksom.



`667 00:25:04,640 --> 00:25:06,900`
Men det är ju super, i och med att man lägger det då



`668 00:25:06,900 --> 00:25:08,960`
hos leverantören så leverantören kommer ju



`669 00:25:08,960 --> 00:25:10,400`
bara se till att man har



`670 00:25:10,400 --> 00:25:12,960`
flyttat risken någonstans. Så man gör



`671 00:25:12,960 --> 00:25:15,020`
det man kan göra. Men det finns ju ingenting



`672 00:25:15,020 --> 00:25:16,900`
idag med i vetlingen som stoppar att man använder en



`673 00:25:16,900 --> 00:25:19,140`
VPN och så kommer man in på sina



`674 00:25:19,140 --> 00:25:20,500`
sajter från ett annat land där det inte är så.



`675 00:25:20,560 --> 00:25:22,820`
Det är age verification. Leverantören har ju



`676 00:25:22,820 --> 00:25:23,840`
i det här fallet



`677 00:25:23,840 --> 00:25:26,480`
inga incitament att göra någonting mer än



`678 00:25:26,480 --> 00:25:28,620`
absolut minsta möjliga. Exakt. De vill ju ha många



`679 00:25:28,620 --> 00:25:30,820`
användare. Och ett VPN-konto är ganska



`680 00:25:30,820 --> 00:25:32,880`
gratis idag. Precis. Och det gör ju att du kan



`681 00:25:32,880 --> 00:25:34,700`
komma från vilket land som helst. Och jag tycker att...



`682 00:25:34,700 --> 00:25:36,760`
Och börjar vi då säga såhär, vi förbjuder VPN-trafik



`683 00:25:36,760 --> 00:25:38,860`
vi förbjuder krypterad trafik. Precis, då har du ju inte



`684 00:25:38,860 --> 00:25:40,820`
internet längre. Nu är vi ju, då börjar vi gå in på



`685 00:25:40,820 --> 00:25:42,940`
ett jäkligt, alltså såhär snårig skog.



`686 00:25:43,140 --> 00:25:44,640`
Men då börjar vi komma till liksom



`687 00:25:44,640 --> 00:25:46,380`
lite Great Firewall of China. Ja, det är sant.



`688 00:25:46,380 --> 00:25:48,340`
Det är som du säger, det här är inte i världen



`689 00:25:48,340 --> 00:25:50,320`
implementeras inte detta. Nej. Så det är bara



`690 00:25:50,320 --> 00:25:52,600`
lägga din användare i ett land som inte har det här.



`691 00:25:52,600 --> 00:25:54,420`
Och då börjar vi då bli intressant, för att



`692 00:25:54,420 --> 00:25:56,480`
då måste vi ändå i värdera...



`693 00:25:56,480 --> 00:25:58,460`
Det är sjukt många användare som kommer från



`694 00:25:58,460 --> 00:25:59,480`
Niu. Ja.



`695 00:26:00,220 --> 00:26:02,600`
Nej, men om man vänder på det då, så vad har vi då?



`696 00:26:02,760 --> 00:26:03,960`
Jo, men vi har en



`697 00:26:03,960 --> 00:26:06,220`
point of contact som kommer innehålla



`698 00:26:06,220 --> 00:26:08,020`
integritet om detta blir ett



`699 00:26:08,020 --> 00:26:10,280`
bör, ett skallkrav på alla



`700 00:26:10,280 --> 00:26:12,360`
europeiska sajter. Då kommer jag också



`701 00:26:12,360 --> 00:26:14,160`
kunna fingerprinta folk som använder VPN



`702 00:26:14,160 --> 00:26:15,000`
när det är väldigt tydligt.



`703 00:26:16,400 --> 00:26:17,980`
Och det är inte heller så jäkla bra då.



`704 00:26:18,340 --> 00:26:20,520`
Du kommer ju också sätta en massa



`705 00:26:20,520 --> 00:26:22,100`
människor i kläm som inte av



`706 00:26:22,100 --> 00:26:24,360`
olika anledningar har tillgång till identifierade



`707 00:26:24,360 --> 00:26:26,360`
känslor, alltså som inte har ID-en



`708 00:26:26,360 --> 00:26:27,780`
eller pass eller...



`709 00:26:27,780 --> 00:26:30,700`
En sak som jag har satt och funderat på, kan det här vara



`710 00:26:30,700 --> 00:26:31,720`
ett



`711 00:26:31,720 --> 00:26:34,600`
ett steg i maktkampen



`712 00:26:34,600 --> 00:26:36,340`
mot de sociala medierietarna?



`713 00:26:36,960 --> 00:26:38,700`
Att det har varit svårt



`714 00:26:38,700 --> 00:26:40,560`
och även med GDPR



`715 00:26:40,560 --> 00:26:42,440`
har det varit svårt att tvinga dem att inte



`716 00:26:42,440 --> 00:26:44,100`
samla information om alla besökare.



`717 00:26:45,680 --> 00:26:46,200`
Så



`718 00:26:46,200 --> 00:26:47,940`
nu tar de bort



`719 00:26:48,340 --> 00:26:50,420`
en jävla massa besökare istället från de sociala



`720 00:26:50,420 --> 00:26:52,240`
medie-sajterna. Tror inte att det kommer



`721 00:26:52,240 --> 00:26:53,340`
att funka på det sättet.



`722 00:26:53,700 --> 00:26:56,660`
Det är det de försöker



`723 00:26:56,660 --> 00:26:57,560`
göra, det är det jag försöker säga.



`724 00:26:57,600 --> 00:27:00,120`
Tror du att risken är större att de får mer information



`725 00:27:00,120 --> 00:27:01,220`
om



`726 00:27:01,220 --> 00:27:03,700`
de individuella kontorna?



`727 00:27:03,860 --> 00:27:05,740`
Ja, de får ju åldersverifiering.



`728 00:27:05,900 --> 00:27:08,020`
Och det är ju väldigt värdefull information



`729 00:27:08,020 --> 00:27:10,120`
även om du inte har identiteten



`730 00:27:10,120 --> 00:27:11,780`
så är det ju ett marknadsförings...



`731 00:27:11,780 --> 00:27:14,160`
Det är så roligt att vi pratar om det här nu. Jag läser



`732 00:27:14,160 --> 00:27:16,340`
en bok just nu som heter



`733 00:27:16,340 --> 00:27:18,100`
jag fuskar lite



`734 00:27:18,340 --> 00:27:20,420`
som är skriven utav



`735 00:27:20,420 --> 00:27:22,160`
Sarah Wynne Williams



`736 00:27:22,160 --> 00:27:24,520`
som var en utav Facebooks



`737 00:27:24,520 --> 00:27:26,620`
första policy



`738 00:27:26,620 --> 00:27:28,520`
kör. Alltså hon går på nation



`739 00:27:28,520 --> 00:27:29,580`
och så här. Hon kommer från UN



`740 00:27:29,580 --> 00:27:32,260`
och går in på Facebook och beskriver



`741 00:27:32,260 --> 00:27:34,160`
sin resa från



`742 00:27:34,160 --> 00:27:36,100`
hur vi ska prata med regimer



`743 00:27:36,100 --> 00:27:38,120`
och länder, hur vi ska förhålla oss till information



`744 00:27:38,120 --> 00:27:38,960`
i olika länder.



`745 00:27:39,920 --> 00:27:41,900`
Jag är inte klar med boken än, men



`746 00:27:41,900 --> 00:27:44,560`
The Trajectory, alltså det vill säga



`747 00:27:44,560 --> 00:27:46,260`
vägen från hennes idé



`748 00:27:46,260 --> 00:27:48,300`
om att vi ska skapa en så



`749 00:27:48,340 --> 00:27:49,360`
social mediaplattform



`750 00:27:49,360 --> 00:27:50,600`
som är god.



`751 00:27:50,600 --> 00:27:51,480`
Som är god.



`752 00:27:52,980 --> 00:27:54,600`
Ja, det är så bäckmörkt



`753 00:27:54,600 --> 00:27:56,160`
nu när folk börjar förstå att



`754 00:27:56,160 --> 00:27:57,520`
vi kan driva opinion.



`755 00:27:58,220 --> 00:28:00,460`
Och sen då vad som händer inne i Facebook



`756 00:28:00,460 --> 00:28:02,780`
när de kommer fram till att de kan driva opinion.



`757 00:28:03,040 --> 00:28:04,340`
Den här boken är skriven av en person



`758 00:28:04,340 --> 00:28:05,800`
så att det är en åsikt och hennes



`759 00:28:05,800 --> 00:28:08,080`
livsåskådning på det här.



`760 00:28:08,540 --> 00:28:10,200`
Men det är ju inte positivt.



`761 00:28:10,340 --> 00:28:12,760`
Tänk om man ser tillbaka på hela Cambridge Analytica



`762 00:28:12,760 --> 00:28:14,020`
skandalen och sådär.



`763 00:28:14,140 --> 00:28:15,160`
Det har ju pågått länge.



`764 00:28:15,580 --> 00:28:18,220`
Och då kan man tänka sig att Facebook bara, ja det var ju dumt



`765 00:28:18,220 --> 00:28:20,720`
att de var där. Eller, det här är ett business case.



`766 00:28:20,920 --> 00:28:21,520`
Ja, såklart.



`767 00:28:21,980 --> 00:28:22,980`
Min spontana tanke är att...



`768 00:28:22,980 --> 00:28:26,280`
Vi vet ju att det har läckt Facebook



`769 00:28:26,280 --> 00:28:28,700`
material från marknadsföringsavdelningen



`770 00:28:28,700 --> 00:28:30,500`
där man vet att man har skamannonser



`771 00:28:30,500 --> 00:28:31,620`
men det är också revenue



`772 00:28:31,620 --> 00:28:33,540`
som man väljer att inte ta bort dem.



`773 00:28:35,060 --> 00:28:36,460`
Men en annan grej



`774 00:28:36,460 --> 00:28:37,260`
är ju det här.



`775 00:28:37,660 --> 00:28:39,960`
En logisk följd av det här är ju att



`776 00:28:39,960 --> 00:28:42,320`
om det blir



`777 00:28:42,320 --> 00:28:44,040`
16-årsgräns till en massa grejer



`778 00:28:44,040 --> 00:28:45,940`
så kommer ju typ alla 14-åringar



`779 00:28:45,940 --> 00:28:47,600`
kommer ju betala någon.



`780 00:28:48,220 --> 00:28:50,100`
För att skapa ett åldersbevis på deras



`781 00:28:50,100 --> 00:28:50,920`
mobiltelefon.



`782 00:28:51,600 --> 00:28:53,840`
Det kommer kring oss på massa olika sätt.



`783 00:28:53,840 --> 00:28:55,140`
Ja, men alltså...



`784 00:28:55,140 --> 00:28:57,760`
Eller så kommer de hänga på en sajt som hostas



`785 00:28:57,760 --> 00:28:58,280`
i ett land utanför.



`786 00:28:58,280 --> 00:29:00,520`
Ja, men har du precis fyllt...



`787 00:29:00,520 --> 00:29:03,020`
Har du precis fyllt så kan ju det ju snabba pengar



`788 00:29:03,020 --> 00:29:04,840`
och börja hjälpa folk att



`789 00:29:04,840 --> 00:29:06,140`
fixa åldersbevis.



`790 00:29:06,140 --> 00:29:08,120`
Det är ju som när den första personen fyllde 20



`791 00:29:08,120 --> 00:29:09,620`
och kunde köpa ut på systemet.



`792 00:29:09,740 --> 00:29:11,280`
Det är ju samma effekt liksom.



`793 00:29:12,400 --> 00:29:14,200`
En sak jag tänkte på här, jag tycker att



`794 00:29:14,200 --> 00:29:16,340`
att jag var ute efter det där



`795 00:29:16,340 --> 00:29:17,820`
att de försöker nå, eller



`796 00:29:18,220 --> 00:29:20,500`
sätta tryck på de här sociala medieplattformarna



`797 00:29:20,500 --> 00:29:21,700`
kommer från att jag läste just



`798 00:29:21,700 --> 00:29:24,180`
Australiens, det här är ju



`799 00:29:24,180 --> 00:29:25,700`
eSafety heter det i Australien då.



`800 00:29:26,080 --> 00:29:28,260`
Läste deras information om beslutet.



`801 00:29:29,260 --> 00:29:30,500`
Det är då eSafety's



`802 00:29:30,500 --> 00:29:32,520`
view that Facebook, Instagram,



`803 00:29:32,680 --> 00:29:34,640`
Snapchat, Threads, TikTok, Twitch,



`804 00:29:34,860 --> 00:29:36,720`
X, YouTube, Kik och Reddit



`805 00:29:36,720 --> 00:29:38,620`
are age-restricted platforms



`806 00:29:38,620 --> 00:29:40,720`
among others. Men de är liksom uttalade.



`807 00:29:41,860 --> 00:29:42,800`
Den listan



`808 00:29:42,800 --> 00:29:44,360`
kan förändras och de har en antal



`809 00:29:44,360 --> 00:29:46,220`
kategorier längre ner som liksom avgör



`810 00:29:46,220 --> 00:29:47,840`
om det ska vara



`811 00:29:48,220 --> 00:29:50,400`
age-restricted eller inte. Men de säger här, varför då?



`812 00:29:51,160 --> 00:29:52,780`
The social media age-restriction



`813 00:29:52,780 --> 00:29:55,100`
aim to protect young Australians



`814 00:29:55,100 --> 00:29:57,340`
from pressures and risks



`815 00:29:57,340 --> 00:29:59,580`
that users can be exposed to



`816 00:29:59,580 --> 00:30:01,720`
while logged into social media accounts.



`817 00:30:02,160 --> 00:30:03,220`
These come from



`818 00:30:03,220 --> 00:30:05,540`
design features that encourage



`819 00:30:05,540 --> 00:30:07,480`
them to spend more time on screens



`820 00:30:07,480 --> 00:30:09,340`
while also serving up content



`821 00:30:09,340 --> 00:30:11,400`
and can harm their health and well-being.



`822 00:30:11,700 --> 00:30:13,460`
De pekar ju verkligen ut att det liksom är



`823 00:30:13,460 --> 00:30:15,060`
det är algoritmerna



`824 00:30:15,060 --> 00:30:17,480`
och i viss mån innehållet då



`825 00:30:17,480 --> 00:30:17,800`
som



`826 00:30:18,220 --> 00:30:19,380`
är det som är skadligt.



`827 00:30:20,080 --> 00:30:20,460`
Och jag menar,



`828 00:30:20,740 --> 00:30:23,820`
ett annat sätt att go about this



`829 00:30:23,820 --> 00:30:25,960`
är ju att se till att de här plattformarna



`830 00:30:25,960 --> 00:30:26,420`
måste



`831 00:30:26,420 --> 00:30:29,800`
få inte ha skadliga algoritmer.



`832 00:30:30,380 --> 00:30:32,000`
Det låter ju nästan som en



`833 00:30:32,000 --> 00:30:33,440`
rimligare approach.



`834 00:30:33,920 --> 00:30:36,080`
Om vi nu har system där ute



`835 00:30:36,080 --> 00:30:38,000`
i världen som snurrar på vårt



`836 00:30:38,000 --> 00:30:39,120`
gemensamma internet,



`837 00:30:39,440 --> 00:30:41,360`
och de är



`838 00:30:41,360 --> 00:30:43,340`
skadliga saker där.



`839 00:30:43,620 --> 00:30:45,720`
Jag kan ju jämföra det med om någon har gått omkring



`840 00:30:45,720 --> 00:30:47,540`
och släppt ut giftig gas.



`841 00:30:48,220 --> 00:30:50,240`
Oavsett var det någonstans i världen så har ju folk



`842 00:30:50,240 --> 00:30:51,320`
runt omkring haft åsikter.



`843 00:30:52,620 --> 00:30:54,680`
Lösningen hade inte varit att du måste köpa en gasmask.



`844 00:30:54,780 --> 00:30:55,820`
Du måste, precis.



`845 00:30:56,280 --> 00:30:58,320`
Jag måste verifiera att jag kan



`846 00:30:58,320 --> 00:31:00,300`
klara av den här gasen. Det är inte lösningen.



`847 00:31:00,500 --> 00:31:02,260`
Utan sluta släppa ut gasen



`848 00:31:02,260 --> 00:31:04,080`
för helvete. Det här är skadligt liksom.



`849 00:31:04,320 --> 00:31:05,020`
Jag håller helt med.



`850 00:31:05,160 --> 00:31:07,340`
Och sen bygger väl det här lite på också att det är en



`851 00:31:07,340 --> 00:31:09,920`
dopaminidé här.



`852 00:31:10,160 --> 00:31:11,820`
Så det är ju ett knark.



`853 00:31:12,240 --> 00:31:12,600`
Exakt.



`854 00:31:12,860 --> 00:31:15,360`
Det här är ju ingenting som jag hittar på utan



`855 00:31:15,360 --> 00:31:18,040`
det är ju samma som en slot machine.



`856 00:31:18,220 --> 00:31:20,280`
Det är samma, exakt samma fenomen här



`857 00:31:20,280 --> 00:31:22,260`
att man ska serva så mycket bra content



`858 00:31:22,260 --> 00:31:23,580`
att man inte kan sluta.



`859 00:31:23,740 --> 00:31:25,880`
Med samma vinkel där då. Knark är ju inte lagligt



`860 00:31:25,880 --> 00:31:26,340`
för det mesta.



`861 00:31:27,400 --> 00:31:29,940`
Så får de att sluta tillverka det då.



`862 00:31:30,140 --> 00:31:31,160`
Jag ser nästa grej.



`863 00:31:31,640 --> 00:31:34,280`
För jag pratade alldeles nyss om hur man kommer betala



`864 00:31:34,280 --> 00:31:35,120`
för att sin



`865 00:31:35,120 --> 00:31:37,420`
äldre polare



`866 00:31:37,420 --> 00:31:39,480`
fixar en åldersverifiering.



`867 00:31:39,900 --> 00:31:42,000`
Den andra grejen är ju att det kommer ju komma



`868 00:31:42,000 --> 00:31:44,340`
massvis med sajter som erbjuder



`869 00:31:44,340 --> 00:31:46,180`
att ge oss dina



`870 00:31:46,180 --> 00:31:48,140`
creds så fixar vi



`871 00:31:48,140 --> 00:31:49,320`
åldersverifieringen för dig.



`872 00:31:49,460 --> 00:31:51,600`
Och sen kommer massa unga



`873 00:31:51,600 --> 00:31:53,340`
ge iväg sina konton till...



`874 00:31:53,340 --> 00:31:55,860`
Idén är ju, nu ska jag inte



`875 00:31:55,860 --> 00:31:57,860`
raljera på något sätt, men idén är ju



`876 00:31:57,860 --> 00:31:58,780`
säkerligen sund.



`877 00:32:00,040 --> 00:32:00,920`
Protect the children.



`878 00:32:01,140 --> 00:32:02,680`
Det tycker ju Ylva också.



`879 00:32:03,040 --> 00:32:05,240`
Sen är frågan till vilken nivå vi ska protect the children.



`880 00:32:05,900 --> 00:32:08,280`
Men vad jag vill säga här är att



`881 00:32:08,280 --> 00:32:10,420`
det är ju teknik vi pratar om här nu



`882 00:32:10,420 --> 00:32:11,200`
och det är liksom inte bara



`883 00:32:11,200 --> 00:32:13,180`
om vi slänger upp den här grejen så är det löst.



`884 00:32:14,240 --> 00:32:15,820`
Den morfar ju tekniken liksom.



`885 00:32:15,820 --> 00:32:17,820`
Ja, vi kan säkert komma på



`886 00:32:17,820 --> 00:32:19,480`
hundra olika sätt att mitigera



`887 00:32:19,480 --> 00:32:21,860`
det här problemet med proxys eller VPN



`888 00:32:21,860 --> 00:32:23,820`
eller olika SOX-lösningar.



`889 00:32:24,900 --> 00:32:27,020`
Så det här är ju...



`890 00:32:27,020 --> 00:32:28,500`
Det är väl bra att man pratar om det



`891 00:32:28,500 --> 00:32:29,920`
men frågan är om kontrollen ska ligga på



`892 00:32:29,920 --> 00:32:31,580`
nationsnivå. Jag vet ju fan om det är rätt väg.



`893 00:32:31,580 --> 00:32:34,040`
Jag ser inte att det här löser något problem.



`894 00:32:35,760 --> 00:32:36,940`
Jag ser lite som två saker.



`895 00:32:37,440 --> 00:32:39,280`
Alltså jag gillar att man har en universell



`896 00:32:39,280 --> 00:32:41,040`
ID-hantering i Europa till exempel.



`897 00:32:41,200 --> 00:32:43,020`
Det här har varit guld att inte behöva åka med sitt pass.



`898 00:32:43,120 --> 00:32:45,480`
Att man kan ha en identitet i en telefon



`899 00:32:45,480 --> 00:32:47,460`
som bank-ID som funkar i alla Europaländer.



`900 00:32:47,820 --> 00:32:49,800`
Det är det jag gillar i idén.



`901 00:32:49,900 --> 00:32:51,700`
Men att sen använda den som någon form av



`902 00:32:51,700 --> 00:32:53,920`
A-nyckel till olika tjänster på det öppna



`903 00:32:53,920 --> 00:32:54,560`
internetet.



`904 00:32:55,060 --> 00:32:57,060`
Jag tycker nog inte att det är



`905 00:32:57,060 --> 00:32:59,040`
där vi ska vara.



`906 00:32:59,120 --> 00:33:01,340`
Det föreslagna lösningen löser inte problemet



`907 00:33:01,340 --> 00:33:04,140`
som man har sagt, som man har identifierat



`908 00:33:04,140 --> 00:33:04,660`
att det finns.



`909 00:33:04,840 --> 00:33:07,940`
Jag kan tänka mig



`910 00:33:07,940 --> 00:33:09,720`
att det är...



`911 00:33:09,720 --> 00:33:11,300`
Det skickar en tydlig signal



`912 00:33:11,300 --> 00:33:12,420`
till alla föräldrar.



`913 00:33:13,280 --> 00:33:15,540`
Ja, fast det är ju bara en



`914 00:33:15,540 --> 00:33:17,160`
jävla pyttefraktion av föräldrar.



`915 00:33:17,820 --> 00:33:19,640`
Till dina kids



`916 00:33:19,640 --> 00:33:20,780`
skolklass och fråga alla



`917 00:33:20,780 --> 00:33:23,100`
vilka har koll på den här grejen?



`918 00:33:23,580 --> 00:33:25,880`
Det är ju liksom 1% av föräldrarna som räcker på handen.



`919 00:33:25,920 --> 00:33:27,200`
Ja, men det kommer ju bli...



`920 00:33:27,200 --> 00:33:28,140`
Om det blir konsekvens, ja.



`921 00:33:29,960 --> 00:33:31,480`
Eftersom den här kommer rullas ut



`922 00:33:31,480 --> 00:33:33,780`
så kommer det då vara kanske i svensk



`923 00:33:33,780 --> 00:33:35,620`
lag att du måste ha



`924 00:33:35,620 --> 00:33:37,660`
age verification. Då vet ju alla om att det är



`925 00:33:37,660 --> 00:33:39,560`
age verification. Det är uttalat



`926 00:33:39,560 --> 00:33:41,600`
från statligt håll att ungdomar under



`927 00:33:41,600 --> 00:33:43,620`
15 eller 16 ska inte jobba med socialmedia.



`928 00:33:43,620 --> 00:33:45,120`
Det kommer ju föräldrarna ta till sig.



`929 00:33:45,220 --> 00:33:47,660`
De kommer ju inte hjälpa kidsen att ta sig



`930 00:33:47,660 --> 00:33:49,720`
runt det här. Och de flesta kidsen idag



`931 00:33:49,720 --> 00:33:51,440`
har ju inte den



`932 00:33:51,440 --> 00:33:53,340`
degen kanske eller den tekniska know-howen



`933 00:33:53,340 --> 00:33:55,700`
så de går och skaffar sig ett VPN för att ta sig



`934 00:33:55,700 --> 00:33:57,620`
runt det här. I alla fall



`935 00:33:57,620 --> 00:33:59,500`
inte under 15 års ålder.



`936 00:33:59,640 --> 00:34:00,940`
Utan det är ju där någonstans det kommer.



`937 00:34:01,180 --> 00:34:02,820`
15, 16, kanske 14 på vissa.



`938 00:34:03,920 --> 00:34:05,280`
Det vill säga, det kommer ju ha effekt.



`939 00:34:05,400 --> 00:34:07,540`
Det kommer inte vara 100%, men det är klart att det kommer att ha effekt.



`940 00:34:07,820 --> 00:34:09,420`
Och mycket av den effekten tror jag kommer från



`941 00:34:09,420 --> 00:34:11,960`
just det att det är signalvärdet.



`942 00:34:11,960 --> 00:34:14,020`
För jag menar, att en vuxen kan ta sig



`943 00:34:14,020 --> 00:34:15,840`
runt det här, det är ju förmodligen sannolikt



`944 00:34:15,840 --> 00:34:17,460`
så att det går om man anstränger sig.



`945 00:34:17,660 --> 00:34:20,000`
Jag hittade en miljard grejer i mitt huvud. Vem säger att jag



`946 00:34:20,000 --> 00:34:22,060`
inte slänger upp ett konto och låter alla



`947 00:34:22,060 --> 00:34:23,700`
Europas ungdomar använda det?



`948 00:34:24,140 --> 00:34:25,980`
Grejen är ju såhär, om det bara vore så att



`949 00:34:25,980 --> 00:34:28,000`
det bara var ungdomarna som var tvungna att verifiera sig



`950 00:34:28,000 --> 00:34:29,320`
så hade väl det varit en sak.



`951 00:34:29,900 --> 00:34:32,080`
Men så är det ju inte. Det är alla som



`952 00:34:32,080 --> 00:34:33,740`
måste ju verifiera sig. Åh fy fan vad stökigt.



`953 00:34:34,580 --> 00:34:36,020`
Och nu drabbade jag mig, nu blir jag upprörd.



`954 00:34:37,000 --> 00:34:38,280`
Åh i helvete\!



`955 00:34:38,940 --> 00:34:40,140`
Det var det jag menade med innan.



`956 00:34:40,140 --> 00:34:42,360`
Det är väl en sak att man har en ID-kontroll



`957 00:34:42,360 --> 00:34:44,460`
och att man har en sessionsbaserad, centraliserad



`958 00:34:44,460 --> 00:34:46,580`
idé. Men implementationen



`959 00:34:46,580 --> 00:34:47,180`
blir ju



`960 00:34:47,180 --> 00:34:49,760`
inte sådan. Återigen, då blir det ju



`961 00:34:49,760 --> 00:34:51,920`
en privacy-dröm



`962 00:34:51,920 --> 00:34:53,900`
ur det perspektivet också. Så att även om



`963 00:34:53,900 --> 00:34:55,300`
det här görs



`964 00:34:55,300 --> 00:34:57,900`
superbra så är det ändå så att på något sätt måste



`965 00:34:57,900 --> 00:34:58,760`
mitt konto



`966 00:34:58,760 --> 00:35:01,280`
eller min session



`967 00:35:01,280 --> 00:35:04,400`
knytas till min attestation



`968 00:35:04,400 --> 00:35:06,060`
som säger att jag är över 16.



`969 00:35:06,440 --> 00:35:07,960`
Och den kommer ju vara pass.



`970 00:35:07,960 --> 00:35:10,160`
Och den kommer ju kopplas till



`971 00:35:10,160 --> 00:35:11,880`
nattjournalitet och pass med



`972 00:35:11,880 --> 00:35:13,940`
metadata. Hur lång tid tror du det kommer ta



`973 00:35:13,940 --> 00:35:16,420`
innan den första polisundersökningen



`974 00:35:16,420 --> 00:35:17,160`
kommer att ringa upp?



`975 00:35:17,180 --> 00:35:20,040`
I det, vet du det, utfördaren



`976 00:35:20,040 --> 00:35:22,200`
och säga, vi tror att det här kontot



`977 00:35:22,200 --> 00:35:24,080`
gjorde något dumt. Kan du ge oss



`978 00:35:24,080 --> 00:35:25,320`
allt du har så vi kan korrelera?



`979 00:35:25,460 --> 00:35:27,920`
Det finns idag. Blue notice



`980 00:35:27,920 --> 00:35:30,220`
och red notice. Det sätts ut på passnivå



`981 00:35:30,220 --> 00:35:32,060`
i Europa. Det blir en



`982 00:35:32,060 --> 00:35:33,900`
metadata-lager på din passidentitet.



`983 00:35:34,080 --> 00:35:36,180`
På ditt certifikat som du har i din pass.



`984 00:35:36,880 --> 00:35:37,940`
Svaret är väl det här



`985 00:35:37,940 --> 00:35:40,080`
att appen ska ju inte spara



`986 00:35:40,080 --> 00:35:40,460`
någonting.



`987 00:35:41,680 --> 00:35:43,420`
Nej, men bara ålder.



`988 00:35:43,420 --> 00:35:46,120`
Det finns ju redan profiler



`989 00:35:46,120 --> 00:35:47,100`
på mig.



`990 00:35:47,180 --> 00:35:49,440`
Men skall och bör



`991 00:35:49,440 --> 00:35:49,780`
är ju ett vanligt grej.



`992 00:35:49,780 --> 00:35:53,620`
De flesta sajter har ju koll på



`993 00:35:53,620 --> 00:35:55,400`
vem jag är när jag är ute och snurfar där.



`994 00:35:56,480 --> 00:35:58,040`
Om de var tveksamma



`995 00:35:58,040 --> 00:35:59,420`
över min ålder, de flesta



`996 00:35:59,420 --> 00:36:01,580`
A-genererade reklamannonserna säger redan



`997 00:36:01,580 --> 00:36:03,700`
att den här annonsen är direkt riktad



`998 00:36:03,700 --> 00:36:05,220`
till folk som är 56 år gamla.



`999 00:36:06,100 --> 00:36:07,840`
Så de har ju bra koll på det redan.



`1000 00:36:08,140 --> 00:36:09,820`
Men om de inte hade det så får de ju det



`1001 00:36:09,820 --> 00:36:11,020`
vid den här verifieringen.



`1002 00:36:12,460 --> 00:36:13,920`
Där är det ju också att du kan



`1003 00:36:13,920 --> 00:36:15,500`
välja att



`1004 00:36:15,500 --> 00:36:16,420`
ha



`1005 00:36:16,420 --> 00:36:18,700`
att jag är över 18 av test.



`1006 00:36:19,500 --> 00:36:21,840`
Så att du behöver ju inte...



`1007 00:36:21,840 --> 00:36:24,180`
Det här är ju en funktionsbeskrivning



`1008 00:36:24,180 --> 00:36:25,720`
på någonting som ändå nycklas mot



`1009 00:36:25,720 --> 00:36:27,100`
en riktig identitet.



`1010 00:36:28,000 --> 00:36:30,180`
Jo, men appen är gjord



`1011 00:36:30,180 --> 00:36:30,840`
superbra då.



`1012 00:36:31,100 --> 00:36:32,620`
Kan det ens teoretiskt funka?



`1013 00:36:32,880 --> 00:36:35,760`
Den riktiga identiteten lägger ganska många steg bak.



`1014 00:36:35,760 --> 00:36:37,480`
Alltså, ja, det ni säger nu,



`1015 00:36:37,560 --> 00:36:39,320`
absolut, men det Johan säger är viktigare.



`1016 00:36:39,600 --> 00:36:41,420`
Ja, alltså, det går väl an så länge



`1017 00:36:41,420 --> 00:36:43,040`
vi litar på regimen bakom.



`1018 00:36:43,320 --> 00:36:45,520`
Men har vi då ett knasigt EU-land



`1019 00:36:45,520 --> 00:36:46,300`
finns ganska många.



`1020 00:36:46,420 --> 00:36:46,540`
Ja, ändå.



`1021 00:36:47,580 --> 00:36:49,940`
Då kan ju det där metadata-lagret



`1022 00:36:49,940 --> 00:36:52,020`
kanske, det blir några extra rader i den



`1023 00:36:52,020 --> 00:36:53,700`
av finstacken som säger



`1024 00:36:53,700 --> 00:36:56,300`
du, jag vill veta vem de röstar på,



`1025 00:36:56,460 --> 00:36:57,660`
vad de har för sexuell läggning.



`1026 00:36:58,480 --> 00:37:00,000`
Jag har börjat anonymisera det här



`1027 00:37:00,000 --> 00:37:01,000`
attestet.



`1028 00:37:01,440 --> 00:37:03,980`
Ja, men det borde ju, eftersom det här är



`1029 00:37:03,980 --> 00:37:05,900`
en app som är tillgänglig via en appstore,



`1030 00:37:06,280 --> 00:37:07,740`
så borde man ju kunna verifiera



`1031 00:37:07,740 --> 00:37:09,340`
om den gör ondska eller inte.



`1032 00:37:10,160 --> 00:37:12,300`
Ja, det där är också jävligt intressant.



`1033 00:37:12,300 --> 00:37:13,380`
Beroende på om ondskan sker i backen.



`1034 00:37:13,380 --> 00:37:13,820`
Exakt.



`1035 00:37:14,340 --> 00:37:16,400`
Men vad kan den göra i backen i så fall?



`1036 00:37:16,420 --> 00:37:18,220`
Ja, det har vi noll koll på.



`1037 00:37:18,300 --> 00:37:20,420`
Låt säga att du har en app som pratar



`1038 00:37:20,420 --> 00:37:23,300`
med en ID-verifierings-backend



`1039 00:37:23,300 --> 00:37:25,140`
som sedan pratar med



`1040 00:37:25,140 --> 00:37:25,160`
din tredje part tjänst.



`1041 00:37:25,160 --> 00:37:27,100`
Ja, du kan ju förmodligen se vilka tjänster



`1042 00:37:27,100 --> 00:37:27,980`
går den här personen till.



`1043 00:37:28,580 --> 00:37:29,220`
Herregud, ja.



`1044 00:37:29,840 --> 00:37:31,480`
Det måste du kunna göra, för att frågan



`1045 00:37:31,480 --> 00:37:33,540`
kommer ju komma från tjänsten.



`1046 00:37:33,580 --> 00:37:33,920`
Ja, precis.



`1047 00:37:34,760 --> 00:37:36,020`
Ja, spännande.



`1048 00:37:36,600 --> 00:37:38,940`
Jag är nog mer inne på Johans grej så här.



`1049 00:37:39,480 --> 00:37:43,420`
Jag tror att på en högnivå



`1050 00:37:43,420 --> 00:37:45,420`
och arkitektur,



`1051 00:37:46,420 --> 00:37:48,720`
ja, men fan, det kan vara ändå en bra grej



`1052 00:37:48,720 --> 00:37:50,560`
att göra att vi inte behöver ha



`1053 00:37:50,560 --> 00:37:52,960`
med oss ett jävla plastpapper



`1054 00:37:52,960 --> 00:37:54,320`
med sig i passet.



`1055 00:37:54,880 --> 00:37:56,700`
Men implikationen på



`1056 00:37:56,700 --> 00:37:57,740`
identitet och privacy,



`1057 00:37:58,220 --> 00:38:00,400`
den kommer inte bli bra, för att det är så här



`1058 00:38:00,400 --> 00:38:02,640`
vi måste ha tillit till nation och stat



`1059 00:38:02,640 --> 00:38:04,380`
och det har vi ju aldrig varit



`1060 00:38:04,380 --> 00:38:07,480`
Det har aldrig varit ett problem innan, eller?



`1061 00:38:07,900 --> 00:38:08,660`
Men vi kan ju också



`1062 00:38:08,660 --> 00:38:10,060`
säga så här att i



`1063 00:38:10,060 --> 00:38:12,080`
många av de



`1064 00:38:12,080 --> 00:38:14,880`
identifieringsfrågor som vi har haft



`1065 00:38:14,880 --> 00:38:15,720`
historiskt sett,



`1066 00:38:16,420 --> 00:38:18,620`
säg till exempel, du ska in på



`1067 00:38:18,620 --> 00:38:21,000`
Skatteverket och du ska ändra någonting



`1068 00:38:21,000 --> 00:38:23,160`
rara om din person på Skatteverket



`1069 00:38:23,160 --> 00:38:24,960`
då är du ju



`1070 00:38:24,960 --> 00:38:26,280`
i lägen, du är



`1071 00:38:26,280 --> 00:38:28,920`
du vill identifiera dig



`1072 00:38:28,920 --> 00:38:31,180`
därför så har du i praktiken



`1073 00:38:31,180 --> 00:38:33,320`
lite lägre



`1074 00:38:33,320 --> 00:38:34,880`
säkerhetskrav



`1075 00:38:34,880 --> 00:38:36,880`
eller du har liksom en



`1076 00:38:36,880 --> 00:38:38,140`
helt annan hotbild.



`1077 00:38:38,660 --> 00:38:40,700`
När vi börjar flytta oss till de här



`1078 00:38:40,700 --> 00:38:43,200`
age verification



`1079 00:38:43,200 --> 00:38:44,480`
så blir det ju väldigt mycket



`1080 00:38:44,480 --> 00:38:45,200`
liksom



`1081 00:38:46,420 --> 00:38:48,700`
eftersom att det är någonting som vi inte väljer att göra



`1082 00:38:48,700 --> 00:38:50,540`
utan vi är påtvingade att göra den



`1083 00:38:50,540 --> 00:38:51,440`
i olika flöden



`1084 00:38:51,440 --> 00:38:54,400`
så blir det ju en mycket viktigare fråga om



`1085 00:38:54,400 --> 00:38:56,820`
vad händer om backen är ond



`1086 00:38:56,820 --> 00:38:58,200`
liksom, alltså om



`1087 00:38:58,200 --> 00:38:59,160`
autentiseringsbacken



`1088 00:38:59,160 --> 00:39:02,300`
säger då till exempel



`1089 00:39:02,300 --> 00:39:05,120`
om vi är amerikan och det värsta som kan hända



`1090 00:39:05,120 --> 00:39:06,540`
är sådana här



`1091 00:39:06,540 --> 00:39:07,920`
bilderna som kommer ut på hans



`1092 00:39:07,920 --> 00:39:10,200`
som hade liksom fejktuttar och så liksom



`1093 00:39:10,200 --> 00:39:12,040`
om det är det värsta som kan hända



`1094 00:39:12,040 --> 00:39:13,860`
som man vill



`1095 00:39:13,860 --> 00:39:15,780`
transa eller så liksom



`1096 00:39:16,420 --> 00:39:18,960`
då blir det ju helt plötsligt



`1097 00:39:18,960 --> 00:39:22,100`
då blir det ju väldigt allvarligt



`1098 00:39:22,100 --> 00:39:24,540`
om du kan bli identifierad i det flödet



`1099 00:39:24,540 --> 00:39:25,620`
definitivt



`1100 00:39:25,620 --> 00:39:28,140`
och det finns ju väldigt många exempel på liknande flöden



`1101 00:39:28,140 --> 00:39:30,580`
som är potentiellt oerhört känsliga



`1102 00:39:30,580 --> 00:39:32,600`
beroende på var man är någonstans



`1103 00:39:32,600 --> 00:39:35,200`
så där blir det ju



`1104 00:39:35,200 --> 00:39:35,580`
en



`1105 00:39:35,580 --> 00:39:38,620`
så det är intressant när de säger att de är privacy preserving



`1106 00:39:38,620 --> 00:39:40,640`
för privacy preserving



`1107 00:39:40,640 --> 00:39:42,040`
hade ju bara givet



`1108 00:39:42,040 --> 00:39:44,220`
en serie antaganden såhär



`1109 00:39:44,220 --> 00:39:46,220`
så hur onda antaganden



`1110 00:39:46,220 --> 00:39:47,980`
kan vi göra om



`1111 00:39:47,980 --> 00:39:50,480`
identifieringsinfrastrukturen



`1112 00:39:50,480 --> 00:39:52,480`
innan den inte längre är privacy preserving



`1113 00:39:52,480 --> 00:39:54,260`
sen så tycker jag att ett annat problem är



`1114 00:39:54,260 --> 00:39:54,780`
att man



`1115 00:39:54,780 --> 00:39:58,040`
vänjer folk vid att ge bort sin identitet



`1116 00:39:58,040 --> 00:39:59,380`
till höger och vänster hela tiden



`1117 00:39:59,380 --> 00:40:02,600`
du vänjer folk



`1118 00:40:02,600 --> 00:40:03,120`
vid att



`1119 00:40:03,120 --> 00:40:05,700`
tycka att det är något normalt att



`1120 00:40:05,700 --> 00:40:07,600`
släppa sin anonymitet



`1121 00:40:07,600 --> 00:40:10,220`
även om det är för en central tjänst



`1122 00:40:10,800 --> 00:40:12,580`
jag tycker inte det är någonting



`1123 00:40:12,580 --> 00:40:13,300`
vi ska ha



`1124 00:40:13,300 --> 00:40:14,600`
nej men det är väl



`1125 00:40:16,220 --> 00:40:18,460`
vad den hette den här idiotiska



`1126 00:40:18,460 --> 00:40:19,680`
lagstiftningen som var tidigare



`1127 00:40:19,680 --> 00:40:21,040`
alltså det är ju uppenbart



`1128 00:40:21,040 --> 00:40:24,060`
och det är ju uppenbart att väldigt många



`1129 00:40:24,060 --> 00:40:26,100`
politiker



`1130 00:40:26,100 --> 00:40:28,320`
och de som sitter och



`1131 00:40:28,320 --> 00:40:29,300`
jobbar i olika



`1132 00:40:29,300 --> 00:40:32,040`
liksom lagstiftar



`1133 00:40:32,040 --> 00:40:34,220`
polismyndighetslobbys och sånt



`1134 00:40:35,060 --> 00:40:36,440`
de vill ju gärna



`1135 00:40:36,440 --> 00:40:37,400`
att vi



`1136 00:40:37,400 --> 00:40:40,140`
vänjer oss vid att vara



`1137 00:40:40,140 --> 00:40:42,300`
lydiga medborgare som



`1138 00:40:42,300 --> 00:40:44,020`
håller i hatten



`1139 00:40:44,020 --> 00:40:46,220`
och bugar inför staten och gör som staten



`1140 00:40:46,220 --> 00:40:46,540`
säger



`1141 00:40:46,540 --> 00:40:49,720`
så det är en lite



`1142 00:40:49,720 --> 00:40:51,940`
det är en liten tråkig



`1143 00:40:51,940 --> 00:40:54,020`
mental vändning som samhället



`1144 00:40:54,020 --> 00:40:55,460`
håller på att göra för närvarande och



`1145 00:40:55,460 --> 00:40:57,960`
att de lyckas få igenom



`1146 00:40:57,960 --> 00:41:00,300`
ungefär samma idéer globalt



`1147 00:41:00,300 --> 00:41:01,120`
det är spännande också



`1148 00:41:01,120 --> 00:41:03,720`
precis och det får mig att känna att



`1149 00:41:03,720 --> 00:41:04,600`
den här



`1150 00:41:04,600 --> 00:41:07,580`
anledningen som man



`1151 00:41:07,580 --> 00:41:10,100`
åberopar för att införa de här sakerna



`1152 00:41:10,100 --> 00:41:12,160`
tror inte jag speglar hela verkligheten



`1153 00:41:12,160 --> 00:41:14,620`
inte för att vara superkonspiratorisk



`1154 00:41:14,620 --> 00:41:16,020`
min rumänsk



`1155 00:41:16,220 --> 00:41:18,860`
taxichaufför, han hävdar att det är globalisterna



`1156 00:41:18,860 --> 00:41:20,080`
som ligger bakom allting



`1157 00:41:20,080 --> 00:41:20,700`
George Soros



`1158 00:41:20,700 --> 00:41:23,400`
det är klart det är



`1159 00:41:23,400 --> 00:41:25,800`
vad brukar det vara en omskrivning för



`1160 00:41:25,800 --> 00:41:26,880`
nej men



`1161 00:41:26,880 --> 00:41:30,580`
det händer grejer



`1162 00:41:30,580 --> 00:41:31,940`
runt om i världen som är



`1163 00:41:31,940 --> 00:41:33,260`
läskiga just nu



`1164 00:41:33,260 --> 00:41:35,200`
på många olika fronter



`1165 00:41:35,200 --> 00:41:38,280`
jag tror att vi måste mota Ollegrin på de här grejerna



`1166 00:41:38,280 --> 00:41:40,140`
för att släpper man en centimeter



`1167 00:41:40,140 --> 00:41:42,040`
så är det en illa ute



`1168 00:41:42,040 --> 00:41:44,460`
och kärrkontrollgrejen den har ju kommit tillbaka i en ny



`1169 00:41:44,460 --> 00:41:46,200`
tappning liksom så att det här



`1170 00:41:46,220 --> 00:41:47,360`
är ju någonting som kommer hända



`1171 00:41:47,360 --> 00:41:49,780`
och det är såhär vi måste verkligen gå i bräschen för det här



`1172 00:41:49,780 --> 00:41:51,880`
för det är, när man har tryckt på knappen



`1173 00:41:51,880 --> 00:41:53,440`
är det svårt att ta bort knappen



`1174 00:41:53,440 --> 00:41:55,740`
och jag tror som du sa där Mattias



`1175 00:41:55,740 --> 00:41:57,540`
att ifall vi verkligen brydde oss om de här sakerna



`1176 00:41:57,540 --> 00:41:59,920`
så hade vi även lagt all den här energin



`1177 00:41:59,920 --> 00:42:01,760`
på att lagstifta kring



`1178 00:42:01,760 --> 00:42:04,020`
hur de här algoritmerna får se ut och hur de får fungera



`1179 00:42:04,020 --> 00:42:06,220`
för det är ju som Jesper sa initialt



`1180 00:42:07,000 --> 00:42:08,580`
vi, nu koncentrerar vi oss



`1181 00:42:08,580 --> 00:42:09,560`
på barn



`1182 00:42:09,560 --> 00:42:12,120`
dels för att det är väl ett lätt PR-mål



`1183 00:42:12,120 --> 00:42:13,960`
men det är väl framförallt för att man hävdar



`1184 00:42:13,960 --> 00:42:15,900`
att barn ska skyddas



`1185 00:42:15,900 --> 00:42:17,820`
i större utsträckning än vuxna, vuxna får ju



`1186 00:42:17,820 --> 00:42:19,340`
vara dumma, de får



`1187 00:42:19,340 --> 00:42:22,000`
förstöra sina liv, men med barn så är det lite



`1188 00:42:22,000 --> 00:42:23,840`
viktigare, men med det sagt



`1189 00:42:23,840 --> 00:42:25,740`
alltså de här algoritmerna och de här sajterna



`1190 00:42:25,740 --> 00:42:27,580`
de är ju lika usla för oss som de är för



`1191 00:42:27,580 --> 00:42:30,140`
kids, det kanske är lite uslare



`1192 00:42:30,140 --> 00:42:31,800`
för kids som i sina



`1193 00:42:31,800 --> 00:42:33,980`
formative years, men det är ju fan inte



`1194 00:42:33,980 --> 00:42:36,080`
det är inte bra för vår



`1195 00:42:36,080 --> 00:42:38,080`
hjärnutveckling heller



`1196 00:42:38,080 --> 00:42:39,240`
sen har vi också en



`1197 00:42:39,240 --> 00:42:41,740`
om man pratar ännu högre nivå, vi har ju liksom



`1198 00:42:41,740 --> 00:42:44,160`
en ganska konstig global struktur



`1199 00:42:44,160 --> 00:42:45,880`
nu där våra täckhjältar



`1200 00:42:45,900 --> 00:42:47,680`
har större BNP än



`1201 00:42:47,680 --> 00:42:49,660`
många länder, alltså de flesta länderna



`1202 00:42:49,660 --> 00:42:51,420`
de har en sån maktfaktor och sån



`1203 00:42:51,420 --> 00:42:53,820`
extrem maktfaktor och ekonomi



`1204 00:42:53,820 --> 00:42:55,480`
att de kan styra



`1205 00:42:55,480 --> 00:42:58,260`
opinion, och det är läskigt



`1206 00:42:58,260 --> 00:42:59,540`
ur ett



`1207 00:42:59,540 --> 00:43:00,780`
nationsperspektiv dock



`1208 00:43:00,780 --> 00:43:03,600`
de här lagarna



`1209 00:43:03,600 --> 00:43:05,640`
som är på väg, de visar ju ändå att



`1210 00:43:05,640 --> 00:43:08,100`
stater kan sätta hårt mot hårt



`1211 00:43:08,100 --> 00:43:08,760`
kan de det?



`1212 00:43:10,760 --> 00:43:11,860`
varför gör de då



`1213 00:43:11,860 --> 00:43:13,700`
det på det här sättet, varför inte sätta



`1214 00:43:13,700 --> 00:43:15,280`
push på, återigen, ner på



`1215 00:43:15,900 --> 00:43:18,140`
algoritmnivå istället, så här får det inte funka



`1216 00:43:18,140 --> 00:43:19,700`
det är det som får mig att känna att det här



`1217 00:43:19,700 --> 00:43:22,160`
det är inte algoritmerna som är det man vill åt här



`1218 00:43:22,160 --> 00:43:23,920`
aaah, du tänker så



`1219 00:43:23,920 --> 00:43:25,840`
men jag tror på riktigt att



`1220 00:43:25,840 --> 00:43:28,480`
det är den typen



`1221 00:43:28,480 --> 00:43:29,860`
av lobbyverksamhet som ligger bakom



`1222 00:43:29,860 --> 00:43:31,580`
som finns bakom chat-kontrollen också



`1223 00:43:31,580 --> 00:43:33,460`
jag vill helst inte att mina paket



`1224 00:43:33,460 --> 00:43:36,100`
vi ska begränsa frihet, vi ska ha mer kontroll



`1225 00:43:36,100 --> 00:43:38,060`
på vad folk



`1226 00:43:38,060 --> 00:43:39,040`
säger och skriver och tänker



`1227 00:43:39,040 --> 00:43:41,060`
protect the children



`1228 00:43:41,060 --> 00:43:43,260`
och så ska vi inte ha det



`1229 00:43:43,260 --> 00:43:44,600`
nej, så ska vi verkligen inte ha det



`1230 00:43:44,600 --> 00:43:45,100`
det är



`1231 00:43:45,900 --> 00:43:47,400`
fan vad deppig jag blir nu



`1232 00:43:47,400 --> 00:43:48,840`
ni är så cyniska



`1233 00:43:48,840 --> 00:43:51,040`
men sen är det ju också så här att internet



`1234 00:43:51,040 --> 00:43:52,740`
jag har sagt det här i många år



`1235 00:43:52,740 --> 00:43:54,760`
att man har ett internetabonnemang och sen har man



`1236 00:43:54,760 --> 00:43:55,960`
ett VPN-abonnemang



`1237 00:43:55,960 --> 00:43:58,660`
alltså du ser, man surfar inte på internet



`1238 00:43:58,660 --> 00:43:59,680`
utan kondom liksom



`1239 00:43:59,680 --> 00:44:01,820`
och det kommer ju utveckla sig, tänker jag



`1240 00:44:01,820 --> 00:44:05,200`
den DNS-infrastrukturen vi har idag



`1241 00:44:05,200 --> 00:44:06,500`
den behöver vi inte använda



`1242 00:44:06,500 --> 00:44:08,860`
vi kan dra igång signerade



`1243 00:44:08,860 --> 00:44:10,500`
DNS-zoner där vi själva hostar saker



`1244 00:44:10,500 --> 00:44:11,800`
genom proxys och sånt, så det är så här



`1245 00:44:11,800 --> 00:44:13,360`
det är bara det att



`1246 00:44:13,360 --> 00:44:14,280`
det är mycket man kan göra



`1247 00:44:14,280 --> 00:44:15,440`
homehosting är



`1248 00:44:15,900 --> 00:44:18,540`
men jag menar så här, behöver internet



`1249 00:44:18,540 --> 00:44:20,760`
bli liksom ett piratsamhälle, måste vi



`1250 00:44:20,760 --> 00:44:22,580`
behöva? Alltså det kommer ju bli mer och mer



`1251 00:44:22,580 --> 00:44:24,440`
så under förutsättningar att vi fortsätter introducera



`1252 00:44:24,440 --> 00:44:25,500`
den här typen av lagstiftning



`1253 00:44:25,500 --> 00:44:27,380`
och det är så onödigt för det skapar liksom



`1254 00:44:27,380 --> 00:44:28,940`
så konstiga grejer



`1255 00:44:28,940 --> 00:44:32,160`
det är ju bara en tidsfråga innan, du kommer inte vilja ha en europeisk DNS



`1256 00:44:32,160 --> 00:44:33,300`
om du är en



`1257 00:44:33,300 --> 00:44:36,500`
och sen är det ju också så här



`1258 00:44:36,500 --> 00:44:38,160`
du kommer inte vilja ha



`1259 00:44:38,160 --> 00:44:39,420`
du kommer bara ha mesh-internet



`1260 00:44:39,420 --> 00:44:42,440`
ja men vad fan, peka på något i rötten och köra din egen



`1261 00:44:42,440 --> 00:44:43,340`
resolver då liksom



`1262 00:44:43,340 --> 00:44:45,140`
ja men ha det helt decentraliserat



`1263 00:44:45,900 --> 00:44:46,900`
off the grid



`1264 00:44:46,900 --> 00:44:47,400`
exakt



`1265 00:44:47,400 --> 00:44:49,160`
och då är det så här, om jag nu kör min egen DNS



`1266 00:44:49,160 --> 00:44:51,160`
om nu DNS blir bärvågen för det här



`1267 00:44:51,160 --> 00:44:53,160`
ja hur ska jag, jag är ingen könsleverantör



`1268 00:44:53,160 --> 00:44:55,160`
jag är ju en privatperson, jag behöver inte implementera någonting



`1269 00:44:55,160 --> 00:44:57,160`
precis, du kan göra vad du vill



`1270 00:44:57,160 --> 00:44:59,160`
ja, nu så här, det är bara, det har de säkert tänkt på



`1271 00:44:59,160 --> 00:45:01,160`
men jag menar det är så här, det är inte en



`1272 00:45:01,160 --> 00:45:03,160`
lite som du var inne på Johan, det är inte en



`1273 00:45:03,160 --> 00:45:05,160`
binära approach liksom



`1274 00:45:05,160 --> 00:45:07,160`
bara vi gör det här så blir det kanon



`1275 00:45:07,160 --> 00:45:08,160`
snarare tvärtom



`1276 00:45:08,160 --> 00:45:10,160`
jag tror att det kommer ske en



`1277 00:45:10,160 --> 00:45:12,160`
eller har väl redan börjat ske en



`1278 00:45:12,160 --> 00:45:14,160`
social backlash mot sociala medier



`1279 00:45:14,160 --> 00:45:14,660`
ja



`1280 00:45:14,660 --> 00:45:15,240`
ändå



`1281 00:45:15,240 --> 00:45:15,740`
mm



`1282 00:45:15,900 --> 00:45:17,900`
folk har insett att så här, det här är



`1283 00:45:17,900 --> 00:45:19,900`
det här är ingen bra grej, det kommer börja bli



`1284 00:45:19,900 --> 00:45:21,900`
trendigare och trendigare att



`1285 00:45:21,900 --> 00:45:22,900`
koppla ifrån sig helt



`1286 00:45:22,900 --> 00:45:23,400`
ja



`1287 00:45:23,400 --> 00:45:24,400`
från sociala medier



`1288 00:45:24,400 --> 00:45:26,400`
det tycker jag man ser



`1289 00:45:26,400 --> 00:45:28,400`
att det redan händer till stor utsträckning



`1290 00:45:28,400 --> 00:45:30,900`
folk försöker lägga band på sig själva på olika sätt



`1291 00:45:30,900 --> 00:45:32,900`
låsa ner appar, ta bort sina konton



`1292 00:45:32,900 --> 00:45:34,900`
det där tror jag kommer fortsätta



`1293 00:45:34,900 --> 00:45:36,900`
för att det är helt enkelt



`1294 00:45:36,900 --> 00:45:38,900`
inte socialt credit att vara



`1295 00:45:38,900 --> 00:45:40,900`
konstant i online längre



`1296 00:45:40,900 --> 00:45:42,900`
på samma sätt



`1297 00:45:42,900 --> 00:45:44,900`
och det tror jag är en bra lösning



`1298 00:45:44,900 --> 00:45:45,240`
ja



`1299 00:45:45,240 --> 00:45:47,240`
sen så är ju inte det en lösning



`1300 00:45:47,240 --> 00:45:49,240`
hundra procentig lösning på hela saken



`1301 00:45:49,240 --> 00:45:51,240`
men min känsla är att det här skulle kunna vara



`1302 00:45:51,240 --> 00:45:53,240`
self-correcting



`1303 00:45:53,240 --> 00:45:55,240`
to a point



`1304 00:45:55,240 --> 00:45:57,240`
du tror på folket



`1305 00:45:57,240 --> 00:45:59,240`
jag tror att vi inte har gett det här till mycket tid för att avgöra



`1306 00:45:59,240 --> 00:46:01,240`
åt andra håll



`1307 00:46:01,240 --> 00:46:03,240`
nej, det kan jag nog också ställa mig bakom



`1308 00:46:03,240 --> 00:46:05,240`
och sen så kan jag väl också säga



`1309 00:46:05,240 --> 00:46:07,240`
som



`1310 00:46:07,240 --> 00:46:09,240`
kan jag sitta här väldigt enkelt och säga



`1311 00:46:09,240 --> 00:46:11,240`
som inte har några barn men



`1312 00:46:11,240 --> 00:46:13,240`
lite ansvar får nog ligga på föräldrarna också



`1313 00:46:13,240 --> 00:46:14,240`
så är det faktiskt



`1314 00:46:14,240 --> 00:46:16,240`
så har det väl varit med allting i alla tider



`1315 00:46:16,240 --> 00:46:18,240`
jag menar jag vet att



`1316 00:46:18,240 --> 00:46:20,240`
ifall jag satt och spelade tv-spel i mer än fyra timmar



`1317 00:46:20,240 --> 00:46:22,240`
så kom min mamma och var arg på mig



`1318 00:46:22,240 --> 00:46:24,240`
liksom



`1319 00:46:24,240 --> 00:46:26,240`
ja nej nej och så var det ju för mig med att du har riktigt utsladdad



`1320 00:46:26,240 --> 00:46:28,240`
ur datorn liksom, nu får du göra något annat



`1321 00:46:28,240 --> 00:46:30,240`
och jag menar det är



`1322 00:46:30,240 --> 00:46:32,240`
under förutsättningen att dina barn fortfarande bor hemma hos dig



`1323 00:46:32,240 --> 00:46:34,240`
så har du faktiskt en del du kan säga till om



`1324 00:46:34,240 --> 00:46:36,240`
sen så inser jag också att det inte



`1325 00:46:36,240 --> 00:46:38,240`
är alltid så lätt och det finns en himla massa



`1326 00:46:38,240 --> 00:46:40,240`
sociala tryck och sådana här saker



`1327 00:46:40,240 --> 00:46:42,240`
som gör att det blir problematiskt och svårt



`1328 00:46:42,240 --> 00:46:44,240`
men man får också vara lite vuxen



`1329 00:46:44,240 --> 00:46:46,240`
vi hade ju faktiskt den här



`1330 00:46:46,240 --> 00:46:48,240`
jag har ju 17-åringar hemma



`1331 00:46:48,240 --> 00:46:50,240`
vi hade den här diskussionen för bara två veckor sedan



`1332 00:46:50,240 --> 00:46:52,240`
för jag noterade att en utav mina kids



`1333 00:46:52,240 --> 00:46:54,240`
la sjuka mängder tid på sin telefon



`1334 00:46:54,240 --> 00:46:56,240`
och



`1335 00:46:56,240 --> 00:46:58,240`
istället för



`1336 00:46:58,240 --> 00:47:00,240`
min gut reaction var faktiskt



`1337 00:47:00,240 --> 00:47:02,240`
förbjud



`1338 00:47:02,240 --> 00:47:04,240`
det är ju mitt



`1339 00:47:04,240 --> 00:47:06,240`
ditt familjekonto så jag kan ju styra



`1340 00:47:06,240 --> 00:47:08,240`
hur mycket tid de får ha på apparna



`1341 00:47:08,240 --> 00:47:10,240`
så jag började med att



`1342 00:47:10,240 --> 00:47:12,240`
stänga ner det och då sa min son att



`1343 00:47:12,240 --> 00:47:14,240`
det där är inte okej farsan, okej?



`1344 00:47:14,240 --> 00:47:16,240`
vad ska vi ha för alternativ då?



`1345 00:47:16,240 --> 00:47:18,240`
så då sa han, ja men låt mig



`1346 00:47:18,240 --> 00:47:20,240`
jag hör vad du säger, låt mig



`1347 00:47:20,240 --> 00:47:22,240`
sköta det här nu



`1348 00:47:22,240 --> 00:47:24,240`
och nu har det bara gått två veckor



`1349 00:47:24,240 --> 00:47:26,240`
men det har varit, konsumtionen har gått ner



`1350 00:47:26,240 --> 00:47:28,240`
stadigt



`1351 00:47:28,240 --> 00:47:30,240`
ja det är så, du har ändå sett det över tid för vi pratade precis när det hade hänt



`1352 00:47:30,240 --> 00:47:32,240`
och då hade det liksom



`1353 00:47:32,240 --> 00:47:34,240`
hans son har skaffat en mobil till



`1354 00:47:34,240 --> 00:47:36,240`
och har skaffat att vi sätter upp den nyligen till



`1355 00:47:36,240 --> 00:47:38,240`
respekt



`1356 00:47:38,240 --> 00:47:40,240`
här kan han se runt sig



`1357 00:47:40,240 --> 00:47:42,240`
när du säger det och vi litar ju på det



`1358 00:47:42,240 --> 00:47:44,240`
då det



`1359 00:47:44,240 --> 00:47:46,240`
då brukar jag ändå validera lite Johans idé här



`1360 00:47:46,240 --> 00:47:48,240`
eller Johans tes, det vill säga



`1361 00:47:48,240 --> 00:47:50,240`
ja, reminder, det här är inte så jävla bra



`1362 00:47:50,240 --> 00:47:52,240`
och vi pratar rätt mycket hemma om det nu också



`1363 00:47:52,240 --> 00:47:54,240`
så att ser jag någon av grabbarna



`1364 00:47:54,240 --> 00:47:56,240`
sitter för sjunkna i sin telefon



`1365 00:47:56,240 --> 00:47:58,240`
eller om de ser mig



`1366 00:47:58,240 --> 00:48:00,240`
då petar man i magen litegrann och säger



`1367 00:48:00,240 --> 00:48:02,240`
har du dopamin nu eller?



`1368 00:48:02,240 --> 00:48:04,240`
får du din fix nu eller?



`1369 00:48:04,240 --> 00:48:06,240`
det här tror jag är helt rätt



`1370 00:48:06,240 --> 00:48:08,240`
jag använde datorer för mycket när jag var ung



`1371 00:48:08,240 --> 00:48:10,240`
han har ju blivit jätteirriterad



`1372 00:48:10,240 --> 00:48:12,240`
ja, och jag skulle vilja säga att



`1373 00:48:12,240 --> 00:48:14,240`
vi kan ju inte vara exakt samma snabbare



`1374 00:48:14,240 --> 00:48:16,240`
dopaminkickare



`1375 00:48:16,240 --> 00:48:18,240`
kanske inte



`1376 00:48:18,240 --> 00:48:20,240`
algoritmerna var inte riktigt fullt lika utvecklade



`1377 00:48:20,240 --> 00:48:22,240`
när vi var tvungna att använda dial-up



`1378 00:48:22,240 --> 00:48:24,240`
av flera anledningar så är inte jag så orolig



`1379 00:48:24,240 --> 00:48:26,240`
för just Australiens lista här då



`1380 00:48:26,240 --> 00:48:28,240`
för att dels är jag ju äldre än 16



`1381 00:48:28,240 --> 00:48:30,240`
som är deras gräns



`1382 00:48:30,240 --> 00:48:32,240`
och dels så är det på listan så finns då



`1383 00:48:32,240 --> 00:48:34,240`
Facebook, Instagram, Kik, Reddit, Snapchat



`1384 00:48:34,240 --> 00:48:36,240`
Threads, TikTok, Twitch, X



`1385 00:48:36,240 --> 00:48:38,240`
och Youtube



`1386 00:48:38,240 --> 00:48:40,240`
så det är egentligen, utav dem så är det bara Youtube



`1387 00:48:40,240 --> 00:48:42,240`
som jag känner att jag skulle



`1388 00:48:42,240 --> 00:48:44,240`
sakna med och då är jag oerhört



`1389 00:48:44,240 --> 00:48:46,240`
generös i mitt uttryck



`1390 00:48:46,240 --> 00:48:48,240`
de andra är liksom



`1391 00:48:48,240 --> 00:48:50,240`
not so important



`1392 00:48:50,240 --> 00:48:52,240`
jag kanske skulle bara göra



`1393 00:48:52,240 --> 00:48:54,240`
bygga sociala medier där man måste



`1394 00:48:54,240 --> 00:48:56,240`
verifiera att man är under 18



`1395 00:48:56,240 --> 00:48:58,240`
för att få vara med



`1396 00:48:58,240 --> 00:49:00,240`
jag höll på att säga



`1397 00:49:00,240 --> 00:49:02,240`
jag pratar ju inte om det i något gammalt Peter-avsnitt



`1398 00:49:02,240 --> 00:49:04,240`
Lunestorm



`1399 00:49:04,240 --> 00:49:06,240`
det var nästan så



`1400 00:49:06,240 --> 00:49:08,240`
har vi lyckats ta oss igenom



`1401 00:49:08,240 --> 00:49:10,240`
punkterna, vad händer



`1402 00:49:10,240 --> 00:49:12,240`
det har vi nog täckt va?



`1403 00:49:12,240 --> 00:49:14,240`
vad som försöker lösas



`1404 00:49:14,240 --> 00:49:16,240`
och risker skulle jag säga



`1405 00:49:16,240 --> 00:49:18,240`
att vi har definierat rätt väl



`1406 00:49:18,240 --> 00:49:20,240`
fördelar har vi väl



`1407 00:49:20,240 --> 00:49:22,240`
jag tror på riktigt att det här



`1408 00:49:22,240 --> 00:49:24,240`
låt oss säga att det går igenom enligt



`1409 00:49:24,240 --> 00:49:26,240`
plan allting, så tror jag att



`1410 00:49:26,240 --> 00:49:28,240`
det kommer bli färre



`1411 00:49:28,240 --> 00:49:30,240`
under 16-åringar



`1412 00:49:30,240 --> 00:49:32,240`
på sociala medier, det tror jag



`1413 00:49:32,240 --> 00:49:34,240`
åtminstone på de stora sociala medierna



`1414 00:49:34,240 --> 00:49:36,240`
ja, precis



`1415 00:49:36,240 --> 00:49:38,240`
på dem jag just rappade upp till



`1416 00:49:38,240 --> 00:49:40,240`
huruvida medlemsavtalet



`1417 00:49:40,240 --> 00:49:42,240`
på 4chan kommer öka



`1418 00:49:42,240 --> 00:49:44,240`
skulle det låta vara osagt



`1419 00:49:44,240 --> 00:49:46,240`
not age restricted social media platforms



`1420 00:49:46,240 --> 00:49:48,240`
finns också en lista på



`1421 00:49:48,240 --> 00:49:50,240`
discord, github, google classroom



`1422 00:49:50,240 --> 00:49:52,240`
legoplay, messenger, pinterest, roblox



`1423 00:49:52,240 --> 00:49:54,240`
steam och steam chat, whatsapp



`1424 00:49:54,240 --> 00:49:56,240`
och youtube kids



`1425 00:49:56,240 --> 00:49:58,240`
discord vet jag har age verification och har blivit hackad och blivit av



`1426 00:49:58,240 --> 00:50:00,240`
med sända optionuppgifter från det



`1427 00:50:00,240 --> 00:50:02,240`
perfekt



`1428 00:50:02,240 --> 00:50:04,240`
det är ju bara början på en dum grej



`1429 00:50:04,240 --> 00:50:06,240`
nej



`1430 00:50:06,240 --> 00:50:08,240`
det är privacy for the win



`1431 00:50:08,240 --> 00:50:10,240`
alltså



`1432 00:50:10,240 --> 00:50:12,240`
är det slutsatsen



`1433 00:50:12,240 --> 00:50:14,240`
ja men jag tror fan det med det



`1434 00:50:14,240 --> 00:50:16,240`
om det nu är problemet man vill komma tillrätta med



`1435 00:50:16,240 --> 00:50:18,240`
är att sociala medier är onda för att de har



`1436 00:50:18,240 --> 00:50:20,240`
ondskefulla algoritmer som gör oss dopaminberoende



`1437 00:50:20,240 --> 00:50:22,240`
gå efter algoritmerna



`1438 00:50:22,240 --> 00:50:24,240`
inför inte



`1439 00:50:24,240 --> 00:50:26,240`
slutet på privacy online



`1440 00:50:26,240 --> 00:50:28,240`
för att komma åt det problemet på helt fel sätt



`1441 00:50:28,240 --> 00:50:30,240`
jag kan tänka mig dock att det där



`1442 00:50:30,240 --> 00:50:32,240`
är ju



`1443 00:50:32,240 --> 00:50:34,240`
det som är svårt med det är



`1444 00:50:34,240 --> 00:50:36,240`
vad är en dålig algoritm



`1445 00:50:36,240 --> 00:50:38,240`
absolut



`1446 00:50:38,240 --> 00:50:40,240`
det här är ju fan företagshemligheter



`1447 00:50:40,240 --> 00:50:42,240`
det får ingen annan veta



`1448 00:50:42,240 --> 00:50:44,240`
det här är ju det lättare av de två alternativen



`1449 00:50:44,240 --> 00:50:46,240`
att försöka driva igen



`1450 00:50:46,240 --> 00:50:48,240`
men allting kan inte vara lätt



`1451 00:50:48,240 --> 00:50:50,240`
men ett problem



`1452 00:50:50,240 --> 00:50:52,240`
runt de här grejerna



`1453 00:50:52,240 --> 00:50:54,240`
vi tog förut upp att man kommer



`1454 00:50:54,240 --> 00:50:56,240`
vissa kommer lägga på



`1455 00:50:56,240 --> 00:50:58,240`
det på grejer



`1456 00:50:58,240 --> 00:51:00,240`
som kanske inte borde vara där



`1457 00:51:00,240 --> 00:51:02,240`
men



`1458 00:51:02,240 --> 00:51:04,240`
det finns ju också det att om du är som tjänsteleverantör



`1459 00:51:04,240 --> 00:51:06,240`
så finns det ju



`1460 00:51:06,240 --> 00:51:08,240`
en risk att du smackar på



`1461 00:51:08,240 --> 00:51:10,240`
en 16 års gräns på



`1462 00:51:10,240 --> 00:51:12,240`
massa grejer



`1463 00:51:12,240 --> 00:51:14,240`
bara för att det kanske skulle kunna vara



`1464 00:51:14,240 --> 00:51:16,240`
ett problem



`1465 00:51:16,240 --> 00:51:18,240`
för det är ju en vanlig grej



`1466 00:51:18,240 --> 00:51:20,240`
alltså olika varianter på självcensur



`1467 00:51:20,240 --> 00:51:22,240`
att du



`1468 00:51:22,240 --> 00:51:24,240`
fegar ut och sätter gränser



`1469 00:51:24,240 --> 00:51:26,240`
där det inte borde vara gränser



`1470 00:51:26,240 --> 00:51:28,240`
det kan också bli en sån sammansvändning där



`1471 00:51:28,240 --> 00:51:30,240`
det är plötsligt mer och mer information



`1472 00:51:30,240 --> 00:51:32,240`
men nej



`1473 00:51:32,240 --> 00:51:34,240`
du skulle kunna hävda att Wikipedia



`1474 00:51:34,240 --> 00:51:36,240`
är social media för att folk får editera där



`1475 00:51:36,240 --> 00:51:38,240`
så att teoretiskt



`1476 00:51:38,240 --> 00:51:40,240`
skulle vi kunna säga att ungdomar



`1477 00:51:40,240 --> 00:51:42,240`
får läsa Wikipedia längre



`1478 00:51:42,240 --> 00:51:44,240`
eller att du måste identifiera din ålder för att läsa Wikipedia



`1479 00:51:44,240 --> 00:51:46,240`
ja men alltså det är inte en



`1480 00:51:46,240 --> 00:51:48,240`
oring



`1481 00:51:48,240 --> 00:51:50,240`
jag tror att det är så man ska se på det



`1482 00:51:50,240 --> 00:51:52,240`
inte att ungdomar får inte göra detta



`1483 00:51:52,240 --> 00:51:54,240`
utan du måste verifiera dig för att komma åt det



`1484 00:51:54,240 --> 00:51:56,240`
det är den vinkeln man måste ha på det



`1485 00:51:56,240 --> 00:51:58,240`
och ja och



`1486 00:51:58,240 --> 00:52:00,240`
var det slutsatsen?



`1487 00:52:00,240 --> 00:52:02,240`
jag tror det



`1488 00:52:02,240 --> 00:52:04,240`
det går åt helvete med allt



`1489 00:52:04,240 --> 00:52:06,240`
men snart så kommer ni kunna signa upp er på



`1490 00:52:06,240 --> 00:52:08,240`
Säkerhetsbrogasterns decentraliserade internetlösning



`1491 00:52:08,240 --> 00:52:10,240`
som vi håller på att bygga



`1492 00:52:10,240 --> 00:52:12,240`
någon moderation och inga algoritmer



`1493 00:52:12,240 --> 00:52:14,240`
till en kostnad av



`1494 00:52:14,240 --> 00:52:16,240`
ja men vänta var inte det



`1495 00:52:16,240 --> 00:52:18,240`
var det Grock som utlovade det



`1496 00:52:18,240 --> 00:52:20,240`
eller var det Truth Social



`1497 00:52:20,240 --> 00:52:22,240`
som gick ut med det här



`1498 00:52:22,240 --> 00:52:24,240`
det här är free voice på riktigt liksom



`1499 00:52:24,240 --> 00:52:26,240`
det är ju det som både Facebook



`1500 00:52:26,240 --> 00:52:28,240`
och Twitter



`1501 00:52:28,240 --> 00:52:30,240`
sparkade ju typ alla sina



`1502 00:52:30,240 --> 00:52:32,240`
moderatortjänster



`1503 00:52:32,240 --> 00:52:34,240`
det kommer bli kanon



`1504 00:52:34,240 --> 00:52:36,240`
ja toppen



`1505 00:52:36,240 --> 00:52:38,240`
ja men på den där lilla halvdeprimerande



`1506 00:52:38,240 --> 00:52:40,240`
not som får vi väl ta en runda av för idag



`1507 00:52:40,240 --> 00:52:42,240`
jag som pratade lite Johan Ryberg Möller med mig



`1508 00:52:42,240 --> 00:52:44,240`
hade jag Jesper Larsson



`1509 00:52:44,240 --> 00:52:46,240`
Jajamen



`1510 00:52:46,240 --> 00:52:48,240`
Peter Magnusson



`1511 00:52:48,240 --> 00:52:50,240`
Nullpekaren i din adressrymd



`1512 00:52:50,240 --> 00:52:52,240`
och Mattias Idag



`1513 00:52:52,240 --> 00:52:54,240`
och mer dopamin



`1514 00:52:54,240 --> 00:52:56,240`
ha det gött hej



`1515 00:52:56,240 --> 00:52:58,240`
tja



`1516 00:52:58,240 --> 00:53:00,240`
jag ska bara häng kvar en sekund nu



`1517 00:53:00,240 --> 00:53:02,240`
jag ska bara se



`1518 00:53:02,240 --> 00:53:04,240`
han hette väl Dave eller vad fan hette han



`1519 00:53:04,240 --> 00:53:06,240`
Kronmål



`1520 00:53:06,240 --> 00:53:08,240`
Dave och Plank



`1521 00:53:08,240 --> 00:53:10,240`
Dave Plank



`1522 00:53:10,240 --> 00:53:12,240`
nej jag tror du har fel i det här



`1523 00:53:12,240 --> 00:53:14,240`
Daves konstant



`1524 00:53:14,240 --> 00:53:16,240`
Dave från de här pingvinerna



`1525 00:53:16,240 --> 00:53:18,240`
det där som är fienden



`1526 00:53:18,240 --> 00:53:20,240`
är det en av dem som är Dave



`1527 00:53:20,240 --> 00:53:22,240`
nej den är fienden



`1528 00:53:22,240 --> 00:53:24,240`
den onda blackfisken är Dave



`1529 00:53:24,240 --> 00:53:26,240`
även stormen



`1530 00:53:26,240 --> 00:53:28,240`
råkar ju vara Dave



`1531 00:53:28,240 --> 00:53:30,240`
men du har koll



`1532 00:53:30,240 --> 00:53:32,240`
nu slutar vi prata fysik


