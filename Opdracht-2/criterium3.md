# Onderbouwing Technisch Ontwerp – Minesweeper

Dit document legt kort en duidelijk uit wat je ziet in de twee UML‑diagrammen en waarom ze zo zijn gemaakt. 


## Waarom een Use Case diagram en een Activity diagram?

Door gebruik te maken van zowel een Use Case diagram en een Acticity diagram, krijgen we een compleet beeld van zowel de functionaliteiten en de workflow van de mineweeper game.  

- **Use Case diagram**: Beantwoordt "WHAT en WHO?". Welke functies heeft het spel? Wie doet wat (speler, timer)? Dit geeft een compleet overzicht van alle doelen en acties in het systeem.
- **Activity diagram**: Beantwoordt "HOW en FLOW?". Hoe verloopt het spel stap voor stap? Wat gebeurt er na een klik? Dit geeft een volledig beeld op de activiteiten die gebreurten tijdens het spel.

De twee diagrammen bij elkaar geven ze een volledig beeld: wat het systeem kan doen (use cases) en hoe het dat doet (activity flow). 


## 1. Hoe laten de diagrammen dit zien?

### Use case diagram (wat kan de gebruiker/systeem doen?)
Bevat 3 actoren (Speler, Nieuwe Speler, Timer), 1 systeem en 10 use cases (goals). Je ziet als functies niveau kiezen, klik op cel, vlag togglen, herstarten, timer bijhouden, quick‑loss, winnen, highscores opslaan en bekijken. Relaties (include/trigger) maken duidelijk dat winnen leidt tot opslaan van highscore en dat de eerste klik de timer start.

### Activity diagram (hoe verloopt de gameflow?)
Toont de hele spelcyclus in een loop. Belangrijke beslissingen: klik op cel, is de cel al onthuld/gevlagd, eerste klik (start timer), is het een mijn (verlies), quick‑loss (≤1s), en gewonnen? Bij winnen worden highscores gecheckt/opgeslagen en is er feedback (geluid/confetti) met herstart.



## 2. Ethiek
- Quick‑loss (eerste klik ≤ 1s) geeft een snelle melding en auto‑restart. Dit voorkomt frustratie door pech en voelt eerlijk.
- Transparantie: timer is zichtbaar, win/lose meldingen zijn duidelijk, highscores zijn per niveau.
- Toegankelijk: niveaus maken instappen makkelijk en uitdagend voor verschillende spelers.



## 3. Privacy (dataminimalisatie)
- We slaan alleen de beste tijd per niveau op in `localStorage` (geen naam, e‑mail, IP of tracking). Dit zie je terug bij UC9/UC10 en in de activity‑stap “Highscore check & opslaan”.
- Alles draait lokaal in de browser en is te verwijderen via browserinstellingen.
- Als er later online highscores komen, dan met toestemming, transparantie en een optie om te verwijderen.



## 4. Security (veilig gebruik, consistente state)
- Validaties: je kunt niet opnieuw klikken op onthulde/gevlagde cellen. Acties na gameOver worden genegeerd. Coördinaten blijven binnen het bord. Dit voorkomt rare states.
- Veilig met de DOM: zet tekst met `textContent`, bewaar coördinaten in `dataset`, en vermijd `innerHTML`.
- LocalStorage: een gebruiker kan lokaal vals spelen (tijd aanpassen), maar dit is single‑player en zonder beloningen. Acceptabel risico. Een servervariant kan later checksums/validatie krijgen.
- Data is niet te achterhalen door derden omdat alles lokaal is opgeslagen.



