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
