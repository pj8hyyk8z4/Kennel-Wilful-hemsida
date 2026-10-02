# AI-mall för uppgiftsplanering

Använd den här mallen för att göra en begäran om en webbplatsändring till en
granskningsbar plan innan implementering påbörjas. Planen ska utgå från
repositoryts faktiska innehåll och får inte behandlas som tillstånd att ändra
WordPress eller publicera till produktion.

## Arbetsflöde

1. Beskriv önskat resultat och varför det behövs. Länka till relevanta sidor,
   ärenden eller bifogad visuell kontext.
2. Be AI:n undersöka repositoryt och ange vilka underlag som stöder planen.
   Skilj verifierade fakta från slutsatser och öppna frågor; hitta inte på
   filer, funktioner, kommandon eller beslut.
3. Fastställ omfattning, avgränsningar och mätbara acceptanskriterier. Be om
   förtydligande innan planering fortsätter om ett obesvarat val påverkar
   beteende, design eller publicering.
4. Beskriv implementation, verifiering, risker och återställning. Beakta att
   ändringar i produktionsmiljön kräver webbplatsägarens uttryckliga
   godkännande och en verifierad återställningspunkt.
5. Granska planen och besvara öppna frågor innan arbetet börjar. Efter
   implementering uppdateras planen med faktiskt ändrade filer och resultat
   från körda kontroller.

### Säker hantering

- Klistra inte in lösenord, API-nycklar, tokens, privata nycklar,
  databasdumpar, säkerhetskopior eller person-, kund-, formulär- eller
  orderuppgifter i AI-verktyg, promptar eller Git.
- Behandla den publika webbplatsen som en referens, inte som en utvecklings-
  eller testmiljö. Ändringar ska först göras och granskas i en lokal kopia
  enligt [WordPress Studio-flödet](./README.md#redigering-med-wordpress-studio).
- Hitta inte på att en körbar applikation, byggprocess eller tester finns.
  Kontrollera README och repositoryt; ange uttryckligen när verifiering inte
  kan köras.
- Skilj planering från genomförande. Ingen databasändring, synkronisering,
  publicering eller annan produktionsåtgärd får ske utan separat uttryckligt
  godkännande.

## Prompt att använda med AI

Kopiera och fyll i följande prompt:

> Skapa en granskningsbar uppgiftsplan för ändringen nedan. Undersök först
> repositoryt och använd dess dokumentation som källa. Märk varje relevant
> uppgift som verifierat faktum, antagande eller öppen fråga. Hitta inte på
> befintlig kod, kommandon, miljöer eller beslut. Om en obesvarad fråga ändrar
> lösningens beteende eller omfattning, stanna och fråga mig i stället för att
> välja själv. Ge en avgränsad stegvis plan, mätbara acceptanskriterier,
> verifiering, risker och eventuell återställning. Planera inte
> produktionsändringar utan uttryckligt godkännande. Följ mallen i
> `AI-TASK-PLAN.md`.
>
> **Begärd ändring:** [Beskriv önskat resultat]
>
> **Bakgrund och underlag:** [Länkar, berörda URL:er, bifogad kontext]
>
> **Kända begränsningar:** [Vad som inte får ändras eller antas]
>
> **Önskat beteende/resultat:** [Beskriv vad som ska vara sant efter ändringen]

## Plan

### Sammanfattning

- **Uppgift:**
- **Önskat resultat:**
- **Berörda användare eller ytor:**

### Underlag och nuläge

| Påstående | Typ (verifierat / antagande / öppen fråga) | Källa eller hur det ska verifieras |
| --- | --- | --- |
| | | |

### Omfattning

**Ingår**

- 

**Ingår inte**

- 

### Frågor och beslut

| Fråga eller beslut | Ansvarig | Blockerar arbetet? |
| --- | --- | --- |
| | | |

### Genomförandesteg

1. 
2. 
3. 

### Acceptanskriterier

- [ ] 

### Verifiering

- **Kontroller eller tester:** [Ange faktiska tillgängliga kommandon; annars
  ange vad som behöver etableras.]
- **Manuell granskning:** [Sidor, tillstånd, enheter eller flöden.]
- **Resultat:** [Fylls i efter genomförande.]

### Risker och återställning

- **Risk:** [Påverkan och sannolik berörd data eller yta.]
- **Förebyggande kontroll:** [Backup, lokal granskning, separat fil-/databasändring.]
- **Återställning:** [Känd återställningspunkt och ansvarig; lämna öppet om okänt.]

### Godkännanden före produktionsåtgärd

- [ ] Ändringen och omfattningen är godkända av webbplatsägaren.
- [ ] Aktuell och återställningsbar säkerhetskopia är verifierad.
- [ ] Publiceringsmetod och ansvarig är bekräftade.
- [ ] Planerad produktionsverifiering och återställning är överenskomna.

### Genomföranderesultat

- **Ändrade filer eller inställningar:**
- **Körda kontroller och utfall:**
- **Kvarstående risker eller avvikelser:**
- **Publiceringsstatus och godkännande:**
