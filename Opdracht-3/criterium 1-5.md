# Code realiseren

Hier is de link van de repository naar **ArtiestenWiki** waar de code te vinden is:
- [ArtiestenWiki](https://github.com/Elinekempe/ArtiestenWiki)


## Ontwikkeltools

Dit project is een website waar je informatie kunt vinden over verschillende artiesten, hun albums en populaire nummers.  
Hiervoor zijn de volgende ontwikkeltools gebruikt:

- HTML 
- Vanilla JavaScript
- Tailwind CSS
- JSON-data voor de artiestenlijst

## Projectstructuur

De website bestaat uit twee pagina's met deze onderdelen:

1.  **Startpagina + navigatie** - Zoekveld, sorteermogelijkheden en overzicht van artiestenkaarten
      -  **Artiestenkaarten** - Visuele kaarten met foto, genre, land en top hits
2.   **Detailpagina** - Uitgebreide informatie over één artiest
        -  **Lijsten** - Albums, hits en extra gegevens per artiest

---

## Functionaliteiten

Hieronder volgt een overzicht van de verschillende functionaliteiten die zijn toegevoegd aan de website:

### Overzichtspagina

- Lijst met artiestenkaarten
- Sorteren op naam, genre, land en jaren actief
- Zoekfunctie op naam, genre, awards en land
- Duidelijke melding wanneer er geen resultaten zijn

### Artiestkaarten

- Afbeelding of fallback-icoon per artiest
- Naam, land, genre en actieve jaren
- Top 3 hits zichtbaar op de kaart
- Klikbaar naar de detailpagina

### Detailpagina

- Uitgebreide artiestinformatie
- Afbeelding, biografie en basisgegevens
- Lijsten met albums en hits
- Website-link
- Foutmelding als een artiest niet gevonden wordt

### Data & structuur

- Gegevens worden geladen uit `artists.json`
- Logica is opgesplitst in losse JavaScript-bestanden
- Detailpagina is verdeeld over meerdere bestanden voor duidelijkere structuur

## Resultaat

Het resultaat is een overzichtelijke artiestenwebsite waarmee gebruikers artiesten kunnen zoeken, sorteren en bekijken in detail met een moderne en visuele interface.

## Vervolgstappen

- Extra filters toevoegen
- Meer detailinformatie per artiest tonen
- Overgangen en animaties verfijnen
- Mobiele weergave mogelijk maken 
