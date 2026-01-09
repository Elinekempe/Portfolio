# Verbetervoorstellen



We hebben de website getest en alle testen zijn geslaagd. Maar er zijn nog verbeterpunten. Hieronder staan 3 belangrijke voorstellen om de website nog sneller, betrouwbaarder en gebruiksvriendelijker te maken.



## 1. Beter status reporting (Server)

**Probleem:**

De huidige testen controleren alleen of de server "200 OK" teruggeeft en een lijst met data. Er wordt niet getest of er iets fout gaat met de status reporting en hoe de frontend daar mee omgaat.

**Oplossing:**
- **Data controleren:** Controleren of de server de juiste data teruggeeft. 
- **Fouten testen:** 
  - Wat gebeurt er bij een pagina die niet bestaat? (404 fout)
  - Wat gebeurt er bij een server probleem? (50X fout)
  - Wat gebeurt er bij verkeerde data? 
- **Input controleren:** Controleren of de server verkeerde invoer afwijst.

**Het resultaat:**

De server wordt betrouwbaarder. Als er iets fout gaat, krijgen gebruikers duidelijke foutmeldingen in plaats van crashes of vreemde meldingen.



## 2. Implementatie van integration testen voor data flow
**Probleem:**

Nu testen we alleen losse onderdelen afzonderlijk met nep-data. We testen niet of alles samen ook echt werkt, van de server tot wat de gebruiker ziet.

**Oplossing:**
- **Complete flow testen:**
  - Start een test-server.
  - Laat de website data opvragen bij deze test-server.
  - Controleer of alles correct weergegeven wordt.
- **Samenwerking checken:** Testen of alle onderdelen goed met elkaar communiceren.
- **Fouten doorgeven:** Checken of foutmeldingen correct worden doorgegeven van server naar frontend.

**Het resultaat:**

We weten zeker dat de hele website werkt, niet alleen de losse onderdelen. Problemen tussen verschillende delen van de website worden vroeg ontdekt.



## 3. Uitbreiding test coverage voor edge cases

**Probleem:**

De huidige testen dekken alleen de basis scenario's. We testen niet wat er gebeurt met uitzonderingen:
- Wat als er geen afbeeldingen zijn in de carousel?
- Wat als de API heel traag antwoordt?
- Wat als een afbeelding niet inlaadt?

**Oplossing:**

- **Lege states testen:**
  - Carousel met 0 afbeeldingen.
  - Homepage zonder data.
  - Controleren of er een nette melding of placeholder wordt getoond.

- **Traagheid testen:**
  - API response duur 5 seconden (in plaats van direct).
  - Controleren of loading spinner werkt.
  - Controleren of gebruiker niet kan klikken op knoppen.

- **Kapotte afbeeldingen testen:**
  - Favicon URL die niet bestaat.
  - Afbeelding links die 404 geven.
  - Controleren of website niet crasht.

**Het resultaat:**

Testen die het echte gedrag van gebruikers simuleren. De website werkt goed zelfs als dingen niet perfect gaan.

