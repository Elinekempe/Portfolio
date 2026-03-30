# Code realiseren

Hier is de link van de repository naar **CycleTrack** waar de code te vinden is:
- [CycleTrack](https://github.com/Elinekempe/CycleTrack)


## Ontwikkeltools

Dit project is een website voor het bijhouden van cyclusgegevens.  
Hiervoor zijn de volgende ontwikkeltools gebruikt:

- HTML
- Vanilla JavaScript
- Tailwind CSS
- localStorage

## Projectstructuur

De website bestaat uit één pagina met deze onderdelen:
- **Header + navigatie** - Maandnavigatie, vandaag/reset en privacyknop
- **Kalender** - Maandweergave met kleuren per cyclusfase
- **Dagdetail** - Invoer van symptomen, mood, tags, intensiteit en notities
- **Filters** - Filteren op symptomen en mood
- **Voorspelling** - Schatting van volgende menstruatie en ovulatie
- **Statistieken** - Overzicht van gemiddelde intensiteit

---


## Functionaliteiten

Hieronder volgt een overzicht van de verschillende functionaliteiten die zijn toegevoegd aan de website:

### Kalender

- Maandweergave met klikbare dagen
- Kleurcodering voor menstruatie, ovulatie en vruchtbare fase
- Highlight voor vandaag en geselecteerde dag
- Kleine puntjes voor weergave van gelogde data

### Daginvoer

- Opslaan en verwijderen van gegevens per datum
- Symptomen, mood en tags via knoppen
- Intensiteit via slider
- Notities per dag
- Extra switches voor menstruatie en gemeenschap

### Filters

- Filter op symptoom
- Filter op mood
- Dagen zonder match visueel lichter maken

### Voorspelling & statistiek

- Simpele voorspelling van volgende menstruatie
- Indicatie van ovulatiemoment
- Gemiddelde intensiteit op basis van ingevulde entries

### Data & privacy

- Gegevens lokaal opslaan in de browser met localStorage
- Privacymodus om gevoelige informatie op het scherm te vervagen

## Resultaat

Het resultaat is een werkende, overzichtelijke en privacyvriendelijke website waarmee gebruikers dagelijks hun cyclusdata kunnen opslaan en terugzien in een kalender en daaruit de juiste informatie kunnen halen.

## Vervolgstappen

- Export/import van data
- Extra statistieken en grafieken
- Toegankelijkheid verbeteren
- Responsief design voor mobiele apparaten