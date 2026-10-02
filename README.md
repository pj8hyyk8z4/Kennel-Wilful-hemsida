# Kennel-Wilful-hemsida

Ett repository som beskriver hur webbplatsen [wilful.se](https://www.wilful.se/)
är uppbyggd och redigeras. Själva WordPress-installationen, innehållet och
inloggningsuppgifter finns inte i detta repository.

## AI-stödd uppgiftsplanering

Använd [AI-mallen för uppgiftsplanering](./AI-TASK-PLAN.md) innan en större
ändring påbörjas. En plan ska skilja verifierade fakta från antaganden, beskriva
omfattning och verifiering samt ange risker och nödvändiga godkännanden. Planen
är inte i sig ett godkännande att ändra eller publicera något på
produktionswebbplatsen.

## Redigering med WordPress Studio

[WordPress Studio](https://developer.wordpress.com/studio/) används för att
göra och granska ändringar lokalt innan de förs till produktionswebbplatsen.
Studio är en lokal WordPress-miljö, inte en direktredigerare för en godtycklig
offentlig webbplats. Redigera därför aldrig produktionsdatabasen eller
produktiva filer från detta repository.

### Förutsättningar

1. Installera WordPress Studio och logga in med det WordPress.com-konto som
   har administratörsbehörighet för webbplatsen.
2. Fastställ webbplatsens driftform med den som ansvarar för webbhotellet.
   Studio Sync stöds för WordPress.com med betalt abonnemang, Pressable och
   webbplatser med Jetpack Backup, VaultPress Backup, Jetpack Security eller
   Jetpack Complete som är anslutna till samma WordPress.com-konto.
3. Säkerställ att det finns en aktuell, återställningsbar säkerhetskopia innan
   någon synkronisering till eller från produktion görs.

Lägg aldrig lösenord, API-nycklar, databasdumpar eller säkerhetskopior i Git.

### Första lokala kopian

Välj en av följande vägar beroende på driftformen:

| Driftform | Så skapas den lokala kopian |
| --- | --- |
| Studio Sync är tillgänglig | Skapa en lokal webbplats i Studio, öppna **Sync**, anslut `https://www.wilful.se/` och välj **Pull**. Hämta databas, tema, aktuella tillägg och uppladdningar som behövs för redigeringen. |
| Studio Sync saknas | Exportera en säkerhetskopia från webbhotellet. Den ska innehålla `wp-config.php`, `wp-content/plugins`, `wp-content/themes`, `wp-content/uploads` samt databasdumpen. Välj sedan **Add site** → **Import from a backup** i Studio. |

En import eller **Pull** ersätter de delar som väljs i den lokala
Studio-webbplatsen. Gör därför en ny lokal export innan en befintlig
arbetskopia skrivs över.

### Redigeringsflöde

1. Hämta en ny säkerhetskopia eller gör **Pull** innan arbetet börjar.
2. Gör ändringen i den lokala Studio-webbplatsen och granska den via den
   lokala webbplatsadressen i Studio.
3. Dokumentera struktur- eller arbetsflödesändringar i detta repository.
   Ändringar i ett versionshanterat tema ska granskas och committas separat
   när ett sådant tema har lagts till här.
4. Ta en lokal export och kontrollera att en återställningspunkt finns för
   produktionswebbplatsen.
5. Publicera bara de avsedda delarna. Med Studio Sync väljs **Push** och
   specifika filer/mappar när möjligt; inkludera databasen endast när
   innehållsändringen verkligen kräver den. Utan Sync används webbhotellets
   godkända import- eller publiceringsrutin.
6. Verifiera den publicerade ändringen på `https://www.wilful.se/`.

En databas-push ersätter produktionsdatabasen. Den får inte användas utan
säkerhetskopia och särskild kontroll av att inga aktuella formulärsvar,
användare eller andra produktionsdata skrivs över.

### Avgränsning

Den publika webbplatsens WordPress REST-API visar att `wilful.se` är en
WordPress-webbplats, men avslöjar inte om den uppfyller kraven för Studio Sync.
Bekräfta driftform och backup-lösning med webbhotellets administratör innan
kopplingen aktiveras. Om kraven inte är uppfyllda används säkerhetskopia och
manuell import i stället för att försöka ansluta Studio direkt till URL:en.

## Inventering av nuvarande webbplats

Inventeringen nedan gjordes 2026-09-29 mot den publika webbplatsen och dess
öppna WordPress REST-API. Den är en verifierbar nulägesbild, inte en export av
produktionsmiljön. Den visuella referensen är den publicerade
[startsidan](https://www.wilful.se/); det finns inga skärmbilder eller
produktionsfiler i detta repository.

### Publicerade sidor

Följande 14 sidor returneras som publicerade av
[`wp/v2/pages`](https://www.wilful.se/wp-json/wp/v2/pages?per_page=100):

| Titel | URL | Anmärkning |
| --- | --- | --- |
| Loving Homes, Happy Dogs | <https://www.wilful.se/> | Startsida |
| About Breeder | <https://www.wilful.se/about-breeder/> | |
| Your Dog, Your Story | <https://www.wilful.se/your-dog-your-story/> | |
| Your Trusted Breeder | <https://www.wilful.se/your-trusted-breeder/> | |
| Our Services | <https://www.wilful.se/our-services/> | |
| Your Furry Friend | <https://www.wilful.se/your-furry-friend/> | |
| Our Gallery | <https://www.wilful.se/our-gallery/> | |
| News with Sidebar | <https://www.wilful.se/blog-1-column-with-sidebar/> | Nyhetsarkivsmall |
| News Classic | <https://www.wilful.se/blog-1-column/> | Nyhetsarkivsmall |
| Contact Us | <https://www.wilful.se/contact-us/> | Kontaktformulär förekommer i sidans beroenden |
| Shop | <https://www.wilful.se/shop/> | Butik |
| Cart | <https://www.wilful.se/cart/> | Varukorg |
| Checkout | <https://www.wilful.se/checkout/> | Kassa |
| My account | <https://www.wilful.se/my-account/> | Kundkonto |

### Inlägg och butik

Det finns 15 publicerade inlägg i
[`wp/v2/posts`](https://www.wilful.se/wp-json/wp/v2/posts?per_page=100):

| Titel | URL |
| --- | --- |
| Choosing the Right Breed: A Guide for Prospective Dog Owners | <https://www.wilful.se/choosing-the-right-breed-a-guide-for-prospective-dog-owners/> |
| The Art of Responsible Dog Breeding: What You Need to Know | <https://www.wilful.se/the-art-of-responsible-dog-breeding-what-you-need-to-know/> |
| Puppy Development Milestones: From Birth to Adoption | <https://www.wilful.se/puppy-development-milestones-from-birth-to-adoption/> |
| Top Tips for Preparing Your Home for a New Puppy | <https://www.wilful.se/top-tips-for-preparing-your-home-for-a-new-puppy/> |
| The Importance of Early Socialization for Puppies | <https://www.wilful.se/the-importance-of-early-socialization-for-puppies/> |
| Understanding Dog Health Certifications for Breeding Dogs | <https://www.wilful.se/understanding-dog-health-certifications-for-breeding-dogs/> |
| Common Myths About Dog Breeding Debunked | <https://www.wilful.se/common-myths-about-dog-breeding-debunked/> |
| How to Find a Reputable Dog Breeder: Your Checklist | <https://www.wilful.se/how-to-find-a-reputable-dog-breeder-your-checklist/> |
| What Separates Responsible Breeders from the Rest | <https://www.wilful.se/what-separates-responsible-breeders-from-the-rest/> |
| The Role of Nutrition in Raising Healthy Breeding Dogs | <https://www.wilful.se/the-role-of-nutrition-in-raising-healthy-breeding-dogs/> |
| Tips for Successful Puppy Training and Obedience | <https://www.wilful.se/tips-for-successful-puppy-training-and-obedience/> |
| Caring for Pregnant Dogs: A Guide for Breeders | <https://www.wilful.se/caring-for-pregnant-dogs-a-guide-for-breeders/> |
| The Genetics of Coat Colors and Patterns in Dogs | <https://www.wilful.se/the-genetics-of-coat-colors-and-patterns-in-dogs/> |
| Preparing for a Litter: A Breeder's Guide to Whelping | <https://www.wilful.se/preparing-for-a-litter-a-breeders-guide-to-whelping/> |
| Creating the Perfect Puppy Playroom: Tips and Ideas | <https://www.wilful.se/creating-the-perfect-puppy-playroom-tips-and-ideas/> |

Butiken är publicerad via WooCommerce och innehåller 36 produkter enligt
[`wc/store/products`](https://www.wilful.se/wp-json/wc/store/products?per_page=100).
Produktkategorierna är Accessories, Bags, Cloth, Hoodie, Shirts, Sweatshirts,
T-shirts och Uncategorized. Produkt- och kategorisidor ska betraktas som
befintliga publika URL:er även om de inte är fristående WordPress-sidor.

### Media, utformning och externa tjänster

- Det publika mediebiblioteket innehåller 89 filer: 54 PNG, 32 JPEG och 3
  WebP. Filerna hämtas från `wp-content/uploads`; hela listan kan hämtas via
  [`wp/v2/media`](https://www.wilful.se/wp-json/wp/v2/media?per_page=100).
- De identifierade ikonfilerna är
  [`kenela-fav.png`](https://www.wilful.se/wp-content/uploads/2024/01/kenela-fav.png)
  och
  [`cropped-kenela-fav.png`](https://www.wilful.se/wp-content/uploads/2024/01/cropped-kenela-fav.png).
  Den faktiska logotypen och dess licens kan inte bekräftas utan åtkomst till
  mediebiblioteket eller temafilerna.
- Startsidan laddar Google Fonts: Roboto, Roboto Slab, Source Sans 3, Source
  Sans Pro, Libre Baskerville, Fraunces, Outfit och Work Sans.
- Startsidan länkar till Facebook-sidan
  [Wilfuls BT](https://www.facebook.com/wilfulsbt) och till en YouTube-video.
  Ett Facebook-flöde laddas också från Facebooks CDN.
- Den publikt observerbara presentationen använder WordPress-temat `kenela`
  tillsammans med Elementor. Laddade tilläggstillgångar visar även
  WooCommerce, Contact Form 7, Custom Facebook Feed Pro, King Addons och
  Supreme Modules for Divi. Detta visar inte vilka tillägg som är aktiva i
  administrationsgränssnittet.

### Källor, bevarande och öppna frågor

| Område | Verifierat nuläge | Hantering före ändring |
| --- | --- | --- |
| Kod och konfiguration | Saknas i Git. Det publika HTML-svaret pekar på temat `kenela` och WordPress-tillägg, men deras källfiler är inte tillgängliga här. | Hämta tema och tillägg via Studio Sync eller en godkänd säkerhetskopia. |
| Innehållsdata | Sidor, inlägg, produkter, inställningar och formulärdata finns i produktionsdatabasen. | Exportera eller synkronisera databasen innan innehåll eller struktur ändras. |
| Bilder och övriga uppladdningar | Finns under produktionswebbplatsens `wp-content/uploads`; 89 publika mediaobjekt kan observeras via API:t. | Hämta uppladdningar med säkerhetskopian eller Studio Sync. |
| Publicering | Webbhotell, deploy-rutin, backup-lösning och Studio Sync-stöd är inte bekräftade. | Bekräfta med webbhotellets administratör innan import eller push. |

Tills ägaren har fattat dokumenterade beslut ska samtliga ovan listade publika
URL:er, befintligt innehåll, media, logotyp/favicons, butiksflöde och externa
integreringar bevaras oförändrade. Det finns ännu inget underlag för att
godkänna omarbetning av någon del. Följande behöver därför besvaras innan
implementering planeras:

1. Vem har administratörsbehörighet till WordPress, webbhotell och
   WordPress.com/Jetpack?
2. Var finns en återställningsbar säkerhetskopia och vem godkänner återläsning
   eller synkronisering?
3. Vilka av de upptäckta temana, tilläggen, produktkategorierna och
   integreringarna används avsiktligt?
4. Vilken logotyp, vilka bilder och vilket textinnehåll får ändras, ersättas
   eller tas bort?

## Arkitektur och tekniska flöden

Detta repository innehåller dokumentation, inte en webbapplikation. Det finns
ingen `package.json`, pakethanterare, byggkonfiguration eller importerad
WordPress-kod att köra lokalt från Git. Arkitekturen nedan beskriver därför
den nuvarande, publikt verifierbara WordPress-installationen och anger vad som
måste bekräftas när en lokal kopia har importerats.

### Systemets huvuddelar

| Del | Verifierat nuläge | Ansvar och gräns |
| --- | --- | --- |
| Webbplattform | WordPress levererar HTML för `wilful.se` och ett öppet REST-API under `/wp-json/`. | WordPress-kärnan, databasen och administrationsgränssnittet finns endast i produktionsmiljön eller i en importerad Studio-kopia. |
| Presentation | Det publika HTML-svaret laddar temat `kenela` och Elementor-tillgångar. | Temats mallar och Elementors sidlayouter är inte versionshanterade här. Ändra dem först i en lokal WordPress-kopia. |
| Innehåll | Sidor, inlägg, WooCommerce-produkter och produktkategorier är publicerade från WordPress. | Redaktionella data lagras i WordPress-databasen; ändringar i sidbyggaren kan också ligga där. |
| Handel | WooCommerce levererar butik, varukorg, kassa och konto. | Order-, kund- och betalningsuppgifter får inte exporteras till eller hanteras i Git. |
| Media | Bilder ligger i `wp-content/uploads` och refereras från WordPress-innehåll och presentation. | Behåll uppladdningsstrukturen vid import; originalfiler och rättigheter kontrolleras i WordPress. |
| Formulär och flöden | Contact Form 7-tillgångar laddas publikt. | Formulärkonfiguration, mottagare och inskickade svar måste granskas i den importerade installationen och får inte dokumenteras med personuppgifter. |

### Hur en sida byggs

1. En besökare begär en publik URL, exempelvis `/about-breeder/`.
2. WordPress matchar URL:en mot en sida, ett inlägg, en produkt eller en
   WooCommerce-systemvy.
3. WordPress hämtar innehåll och inställningar ur databasen. För de publika
   sidorna tyder laddade tillgångar på att tema `kenela` tillsammans med
   Elementor svarar för sidans mall, sektioner och widgets.
4. Temat och tilläggen laddar CSS, JavaScript, typsnitt och bilder. Webbläsaren
   hämtar därefter externa resurser, till exempel Google Fonts och
   Facebook-flödet.
5. Den färdiga HTML-sidan levereras från produktionswebbplatsen.

Återanvändbara UI-delar ska tills vidare behandlas som tema- eller
Elementor-komponenter: sidhuvud, sidfot, navigering, innehållssektioner,
produktkort, varukorg/kassa och kontaktformulär. Deras faktiska mallnamn,
placering och inställningar kan inte fastställas förrän `wp-content/themes`,
`wp-content/plugins` och databasen har importerats. När de finns lokalt ska
denna lista ersättas med de verkliga filerna, Elementor-mallarna och ansvariga
tilläggen.

### Dataflöden

| Källa | Bearbetning och lagring | Publicerad yta |
| --- | --- | --- |
| Redaktionellt innehåll i WordPress | WordPress-databasen; Elementor kan lagra layoutdata i databasen | Sidor, inlägg och nyhetsarkiv |
| Produktdata i WooCommerce | WordPress-databasen och WooCommerce | Butik, produktdetaljer, varukorg, kassa och konto |
| Uppladdade bilder och ikoner | `wp-content/uploads` | Bildblock, galleri, produktbilder och favicon |
| Formulärinmatning | Contact Form 7 och dess konfiguration; lagrings- och e-postflöde är inte verifierat | Kontaktsidan |
| Facebook-innehåll | Custom Facebook Feed Pro hämtar data från Facebook | Inbäddat flöde på publika sidor |

REST-API:et är en läsbar integrationsyta för publicerat innehåll, men ska inte
användas som ersättning för backup eller som skrivkälla utan autentisering och
ägarens godkännande. De verifierade publika ändpunkterna omfattar
`/wp-json/wp/v2/pages`, `/wp-json/wp/v2/posts`, `/wp-json/wp/v2/media` och
`/wp-json/wc/store/products`.

### Lokal utveckling och publicering

1. Skapa en lokal WordPress Studio-kopia genom Studio Sync eller en godkänd
   säkerhetskopia enligt avsnittet **Första lokala kopian**.
2. Kontrollera att databas, tema, aktiva tillägg och nödvändiga uppladdningar
   finns i den lokala kopian innan en ändring påbörjas.
3. Gör och granska ändringen lokalt. Anpassningar i ett importerat, eget tema
   ska läggas under versionshantering först när teamet har beslutat vilken
   del av `wp-content` som ska vara källkod i detta repository.
4. Ta en lokal export eller annan återställningspunkt. Publicera sedan bara
   godkända filer via Studio Sync eller webbhotellets etablerade rutin.
5. Kontrollera den publika URL:en efter publicering. Databasändringar får
   endast föras upp efter kontroll av formulärsvar, användare, order och annat
   aktuellt produktionsinnehåll.

Det finns ingen verifierad CI/CD-pipeline, deploy-hook eller byggprocess.
Inför inte Node-, PHP- eller andra verktyg enbart för dokumentationens skull.
Om ett versionshanterat tema eller en egen integration tillkommer ska dess
pakethanterare, byggkommando, testkommando och deploy-flöde dokumenteras här
vid samma ändring.

### Bevarade beslut och begränsningar

- Git är endast avsett för dokumentation och eventuellt framtida egen
  temakod; hemligheter, databaser, säkerhetskopior, order- och persondata får
  inte checkas in.
- Produktionsdatabasen är den auktoritativa källan för nuvarande innehåll och
  konfiguration tills en kontrollerad lokal kopia har skapats.
- Det är inte bekräftat om Studio Sync, Jetpack Backup eller motsvarande
  återställnings- och publiceringsfunktion finns. Det beslutet kräver åtkomst
  till webbhotellet och WordPress-administrationen.
- Publikt synliga tilläggstillgångar bekräftar inte exakta versioner, aktiv
  konfiguration eller licensstatus. Verifiera samtliga i WordPress innan de
  uppdateras, tas bort eller ersätts.

## Bygg, test och publicering

### Aktuell status

Det finns medvetet inga kommandon för installation, utveckling, bygge, lintning,
typkontroll eller test i detta repository. Det saknas också GitHub Actions.
Repositoryt innehåller ännu inte källkod eller assets från webbplatsen; att
lägga till generiska kommandon eller en alltid grön workflow skulle därför inte
validera den faktiska webbplatsen.

Den tekniska spärren för en automatiserad pipeline är importärendet
[#4](https://github.com/pj8hyyk8z4/Kennel-Wilful-hemsida/issues/4). Även
publiceringsmål, åtkomst och backup-rutin måste bekräftas med
webbplatsadministratören innan en deploymentworkflow kan skapas. Fram till dess
görs publicering manuellt enligt **Lokal utveckling och publicering** ovan.

| Funktion | Status i repositoryt | Förutsättning för införande |
| --- | --- | --- |
| Installation | Ej tillämplig | Importerad och versionshanterad källkod med dokumenterad pakethanterare |
| Lokal utveckling | WordPress Studio används utanför Git | En lokal kopia med databas, tema, tillägg och media |
| Build | Ej tillämplig | Fastställt tema-/frontendspråk och eventuellt byggverktyg |
| Lintning och typkontroll | Ej tillämplig | Källkod och språkval, till exempel PHP, JavaScript eller TypeScript |
| Automatiserade tester | Ej tillämplig | Körbar lokal miljö och identifierade kritiska användarflöden |
| GitHub Actions | Saknas avsiktligt | Reproducerbara kommandon som validerar importerad kod |
| Deployment | Manuell och ej bekräftad | Godkänt publiceringsmål, minsta behörighet och återställningsplan |

### Införande efter kodimport

När #4 har levererat en ren, körbar checkout ska bygg- och
publiceringsflödet etableras i denna ordning:

1. Dokumentera de verkliga, icke-interaktiva kommandona för installation,
   utveckling, build, lintning, typkontroll och test. Varje kommando ska kunna
   köras från en ren checkout utan lokala hemligheter.
2. Lägg till kontroller som passar den importerade tekniken. Minimikravet är
   att en build och relevanta statiska kontroller körs i pull requests och på
   `main`; tester tillkommer för kritiska flöden när det finns körbar kod.
3. Konfigurera GitHub Actions så att misslyckade kontroller ger misslyckad
   status och är ett krav före merge eller deployment. Workflowfiler ska endast
   använda versionsstyrd konfiguration och GitHub Secrets för känsliga värden.
4. Definiera ett explicit publiceringsmål och miljöer. Produktionsuppgifter,
   lösenord, tokens, databasdumpar, privata nycklar och `.env`-filer får aldrig
   läggas i Git eller skrivas ut i workflow-loggar.
5. Koppla deployment till en godkänd commit efter godkända kontroller. Om
   WordPress-databasen berörs krävs en verifierad backup och ett särskilt
   godkännande; filpublicering och databasändring ska kunna göras separat.
6. Dokumentera återställning som en namngiven backup, den commit som ska
   återställas till, ansvarig roll och verifiering av den publika webbplatsen.
   Testa återställningsrutinen i en lokal eller annan icke-produktiv miljö
   innan den används i produktion.

Miljövariabler ska dokumenteras med namn, syfte, om de krävs lokalt eller i CI
och var värdet administreras, men aldrig med värden. Exempelvis kan framtida
workflow-dokumentation referera till `WORDPRESS_*` eller
`DEPLOY_*`-variabler först när deras faktiska behov och minsta behörighet är
fastställda.

## Verifiering av visuell och funktionell paritet

Ingen paritetsverifiering har ännu utförts. #5 är blockerad tills #4 har
importerat en körbar implementation och #3 har etablerat relevanta
valideringskommandon. Den publika produktionswebbplatsen är tills dess endast
en visuell referens, inte ett testresultat.

När implementationen är tillgänglig ska varje punkt nedan jämföras mot
`https://www.wilful.se/` på samma dag och dokumenteras som **likvärdig**,
**avsiktlig avvikelse** eller **fel**. Avsiktliga avvikelser kräver ett
beslutat skäl och en länk till relevant ärende.

| Område | Referens och kontroll |
| --- | --- |
| Sidor och navigering | Kontrollera startsidan och samtliga sidor som listas under **Publicerade sidor**, inklusive menylänkar, intern navigering och 404-hantering. |
| Redaktionellt innehåll | Kontrollera rubriker, brödtext, bildordning, gallerier, länkar, nyhetsarkiv och de 15 inventerade inläggen. |
| Butik | Kontrollera butik, produktlistor, produktdetaljer, varukorg, kassa och konto utan att skapa order i produktion. |
| Kontakt | Kontrollera kontaktvägar och formulärets klientvalidering. Använd en kontrollerad testmottagare eller lokal miljö; skicka inte testdata till produktionsmottagare utan godkännande. |
| Responsivitet | Jämför minst mobil, tablet och desktop. Kontrollera särskilt överlappande bilder, horisontell scroll, navigering, gallerier och WooCommerce-vyer. |
| Tillgänglighet | Testa tangentbordsnavigering, synlig fokusmarkering, rubrikhierarki, alternativa texter, formuläretiketter och kontrast i centrala flöden. |
| Externa beroenden | Kontrollera att typsnitt, Facebook-flöde, YouTube, reCAPTCHA om det används och övriga godkända tredjepartsresurser fungerar eller har en dokumenterad reservhantering. |

Visuell jämförelse ska använda samma viewport, zoomnivå, innehållstillstånd och
inloggningsstatus för referens och implementation. Spara skärmbilder eller
andra jämförelseartefakter utanför Git om de innehåller persondata; annars kan
de versionshanteras med tydlig sid- och viewportbenämning. Playwright MCP är
konfigurerat i `.github/mcp.json` för browserinspektion när en betrodd och
körbar lokal implementation finns.

Funna avvikelser ska åtgärdas före publicering eller spåras i separata issues.
Kända layoutproblem ska hållas avgränsade; till exempel är överlappande bilder
redan spårat i [#7](https://github.com/pj8hyyk8z4/Kennel-Wilful-hemsida/issues/7).
Återkommande paritetskontroller och skärmbildstester läggs till först när de
kan köras reproducerbart mot den importerade implementationen.

## Innehålls- och datamodell

### Källa och avgränsning

WordPress-databasen är den auktoritativa källan för det nuvarande redaktionella
innehållet och WooCommerce-data. Innehåll ska inte kopieras till statiska filer
som en parallell källa. Vid import till en lokal Studio-kopia ska databas och
uppladdningar hämtas tillsammans så att relationer och Elementor-layoutdata
bevaras.

Den publikt synliga modellen har följande innehållstyper:

| Typ | Källa | Användning |
| --- | --- | --- |
| Sida | WordPress `page` | Startsida, informationssidor, galleri, kontakt, butikens systemsidor och nyhetsarkivsmallar |
| Inlägg | WordPress `post` | Nyhets- och kunskapsartiklar |
| Media | WordPress `attachment` | Bilder, favicons och annat uppladdat material |
| Produkt | WooCommerce `product` | Butikens produkter |
| Produktkategori | WooCommerce `product_cat` | Gruppindelning av produkter |
| Elementor-mall | `elementor_library` | Återanvändbara sidbyggarblock och mallar; faktisk användning måste bekräftas efter import |
| Formulär | Contact Form 7 | Kontaktflöde; konfiguration och mottagare ska kontrolleras lokalt |

Publika WordPress-register innehåller inte egna innehållstyper för hundar eller
kullar. De får därför inte antas vara importerbara befintliga data. Om sådant
innehåll ska bli en del av webbplatsen krävs först ägarens beslut om den
föreslagna utökningen nedan.

### Fält, relationer och validering

| Typ | Obligatoriska fält | Relationer | Validering |
| --- | --- | --- | --- |
| Sida | titel, slug, publiceringsstatus, innehåll | valfri utvald bild; kan använda Elementor-mall | Titel får inte vara tom; slug ska vara unik och URL-säker; publicerat innehåll måste ha avsedd publiceringsstatus |
| Inlägg | titel, slug, publiceringsdatum, status, brödtext | valfri utvald bild och kategori | Samma URL-krav som sida; datum ska vara giltigt; länkar och bilder ska ha granskats före publicering |
| Media | fil, MIME-typ, alt-text för meningsbärande bild | kan refereras av sida, inlägg eller produkt | Tillåt endast godkända filformat; alt-text krävs för informativa bilder; filrättighet och licens ska vara dokumenterad |
| Produkt | namn, slug, status, pris, valuta, produktkategori | noll eller fler bilder och kategorier | Pris ska vara ett icke-negativt belopp med korrekt valuta; slug ska vara unik; publicerad produkt behöver korrekt köpbarhetsstatus och tillgänglighetsinformation |
| Produktkategori | namn, slug | noll eller fler produkter | Namn och slug ska vara unika; kategori utan produkter ska vara ett medvetet redaktionellt val |
| Kontaktformulär | etikett, mottagare, samtyckestext | formulärfält och e-postmall | E-postfält ska valideras; samtycke krävs när det är tillämpligt; mottagare får inte exponeras publikt |

Exempel på ett publicerbart redaktionellt innehållsobjekt:

```text
typ: sida
titel: Om uppfödaren
slug: about-breeder
status: publish
innehåll: redaktionell text och godkända mediareferenser
utvald-bild: mediaobjekt med alt-text
```

Exempel på ett publicerbart butiksobjekt:

```text
typ: produkt
namn: Produktnamn
slug: produktnamn
status: publish
pris: 1000
valuta: USD
kategorier: [accessories]
bilder: [mediaobjekt med alt-text]
```

Prisexemplet beskriver struktur, inte ett rekommenderat pris eller en valuta.
Den importerade WooCommerce-konfigurationen är källan för befintliga
produktvärden, skatt och betalningsinställningar.

### Föreslagen utökning för kenneldata

Om ägaren bekräftar att hundar och kullar ska förvaltas i webbplatsen bör de
skapas som egna WordPress-innehållstyper eller ett motsvarande CMS-stöd, inte
som hårdkodade Elementor-sektioner. Följande är ett förslag och är inte
implementerat:

| Typ | Obligatoriska fält | Relationer och regler |
| --- | --- | --- |
| Hund | namn, slug, kön, födelsedatum, status, huvudbild | Status väljs från en kontrollerad lista, exempelvis aktiv, pensionerad eller minnesida. Hälso- och registreringsuppgifter publiceras endast efter uttryckligt godkännande. |
| Kull | namn eller identitet, födelsedatum, status | Refererar till tik och hane som hundobjekt. Datum måste vara giltigt och kullstatus ska styras av en kontrollerad lista. |
| Kontaktuppgift | visningsnamn, kontaktmetod, publiceringsstatus | Personuppgifter ska begränsas till avsedda kontaktvägar och hållas åtskilda från formulärsvar. |

### Redaktionellt flöde och migration

1. Redaktören skapar eller uppdaterar innehåll i WordPress och väljer korrekt
   status. Presentation styrs av tema- och Elementor-mallar, inte av
   duplicerad text i mallar.
2. Innan publicering kontrolleras obligatoriska fält, URL, alt-texter, interna
   länkar, produktpris och kontaktvägar. Ändringar i formulär ska granskas
   särskilt för mottagare och samtycke.
3. Vid import exporteras databas och `wp-content/uploads` i samma
   återställningsbara leverans. Importera först i en lokal miljö och jämför
   postantal, URL:er, mediareferenser, produktkategorier och innehållsstatus
   med inventeringen ovan.
4. Rensa hemligheter, privata kontaktuppgifter, order, konton och
   formulärsvar från allt som ska versionshanteras. Bevara deras relationer
   endast i den skyddade lokala eller produktiva databasen när de behövs för
   drift.

Exakta fältmeta, relationer, obligatoriska pluginfält och valideringsregler
ska revideras mot den importerade databasen innan de behandlas som slutliga.
Det finns ännu ingen importerad databas att mappa rad för rad; denna modell
avgränsar därför observerade fakta från föreslagen framtida struktur.
