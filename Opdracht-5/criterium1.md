# Verbetervoorstellen



We hebben alle applicaties getest en alle tests zijn geslaagd. Maar er zijn nog verbeterpunten. Hieronder staan 3 belangrijke voorstellen om de applicatie nog sneller, betrouwbaarder en gebruiksvriendelijker te maken.



## 1. Beter status reporting (Server)

**Probleem:**

De huidige tests controleren alleen of de server "200 OK" teruggeeft en een lijst met data. We testen niet niet of er iets foutgaat met de status reporting en hoe de frontend daar mee omgaat.

**Oplossing:**
- **Data controleren:** Controleren of de server de juiste data teruggeeft (niet alleen een lijst, maar ook de juiste velden). 
- **Fouten testen:** 
  - Wat gebeurt er bij een pagina die niet bestaat? (404 fout)
  - Wat gebeurt er bij een server probleem? (50X fout)
  - Wat gebeurt er bij verkeerde data?
- **Input controleren:** Controleren of de server verkeerde invoer afwijst.

**Het resultaat:**

De server wordt betrouwbaarder. Als er iets fout gaat, krijgen gebruikers duidelijke foutmeldingen in plaats van crashes of vreemde meldingen.

---

### 2. Implementatie van integration tests voor data flow
**Probleem:**

Nu testen we alleen losse onderdelen afzonderlijk met nep-data. We testen niet of alles samen ook echt werkt van de server tot wat de gebruiker ziet.

**Oplossing:**
- **Complete flow testen:**
  - Start een test-server.
  - Laat de website data opvragen bij deze test-server.
  - Controleer of alles correct op het scherm komt.
- **Samenwerking checken:** Testen of alle onderdelen goed met elkaar communiceren.
- **Fouten doorgeven:** Checken of foutmeldingen correct worden doorgegeven van server naar scherm

**Het resultaat:**

We weten zeker dat de hele applicatie werkt, niet alleen de losse onderdelen. Problemen tussen verschillende delen van de app worden vroeg ontdekt.



## 3. Uitbreiding Test Coverage voor Edge Cases

**Probleem:**

De huidige tests dekken alleen de basis scenario's. We testen niet wat er gebeurt met uitzonderingen:
- Wat als er geen afbeeldingen zijn in de carousel?
- Wat als de API heel traag antwoord?
- Wat als een afbeelding niet laadt?

**Oplossing:**

- **Lege states testen:**
  - Carousel met 0 afbeeldingen.
  - Homepage zonder data.
  - Lege regellijst.

- **Traagheid testen:**
  - API response duur 5 seconden (in plaats van direct).
  - Controleren dat loading spinner werkt.
  - Controleren dat gebruiker niet kan klikken op knoppen

- **Kapotte afbeeldingen testen:**
  - Favicon URL die niet bestaat.
  - Afbeelding links die 404 geven.
  - Controleren dat app niet crasht.

**Het resultaat:**

Tests die het echte gedrag van gebruikers simuleren. De app werkt goed zelfs als dingen niet perfect gaan.


