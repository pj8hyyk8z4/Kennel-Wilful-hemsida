# Kennel-Wilful-hemsida

Ett repository som beskriver hur webbplatsen [wilful.se](https://www.wilful.se/)
är uppbyggd och redigeras. Själva WordPress-installationen, innehållet och
inloggningsuppgifter finns inte i detta repository.

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
