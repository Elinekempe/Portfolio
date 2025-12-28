# Documentatie Testscenario's

Dit document beschrijft de testscenario's voor de PorkySMP-applicatie, inclusief stappen, verwachte resultaten en testgegevens voor zowel hoofdscenario's als alternatieve scenario's.

## Hoe Tests Uit te Voeren

Om alle tests in de applicatie uit te voeren, gebruik je een van de volgende methoden:

### Frontend Tests

1. Dependencies installeren (als nog niet gedaan):
```bash
cd frontend
npm install
```

2. Tests uitvoeren (niet-interactief):
```bash
CI=true npm test -- --watchAll=false
```

3. Met coverage rapport:
```bash
CI=true npm test -- --coverage --watchAll=false
```
### Backend Tests

1. Dependencies installeren (als nog niet gedaan):
```bash
cd backend
npm install
```

2. Tests uitvoeren:
```bash
npm test
```

## Overzicht Testbestanden

| Testbestand | Doel | Type |
|-----------|---------|------|
| HomePage.test.js | Test homepage laden en rendering | Frontend |
| Carousel.test.js | Test carousel slide-navigatie | Frontend |
| PrivateRoute.test.js | Test toegangscontrole en redirects | Frontend |
| InputWithFavicon.test.js | Test URL-normalisatie en favicon preview | Frontend |
| MarkdownContent.test.js | Test markdown-rendering | Frontend |
| Button.test.js | Test button varianten en sizes | Frontend |
| utils.test.js | Test utility functies (cn, getFaviconUrl) | Frontend |
| useHome.test.js | Test homepage data-fetching hook | Frontend |
| useRules.test.js | Test regels data-fetching hook | Frontend |
| api.test.js | Test backend API endpoints | Backend |

## Testscenario's

### 1. Homepage Tests

#### Scenario 1.1: Homepage Laadt Content
**Stappen:**
1. Roep de HomePage component aan met gemockte useHome hook
2. Mock retourneert geslaagde data met afbeeldingen

**Testgegevens:**
- useHome mock retourneert: `{ home: [{ images: [] }], loading: false, error: null }`

**Verwacht Resultaat:**
- Titel "Porky SMP" wordt getoond
- Link naar rules pagina is aanwezig
- Geen foutmelding zichtbaar

#### Scenario 1.2: Homepage Toont Loading-Status
**Stappen:**
1. Roep HomePage aan met loading state
2. Mock useHome retourneert loading=true

**Testgegevens:**
- useHome mock retourneert: `{ home: [], loading: true, error: null }`

**Verwacht Resultaat:**
- Bericht "Loading content…" wordt weergegeven
- Geen inhoud is zichtbaar

#### Scenario 1.3: Homepage Toont Fout bij Mislukken
**Stappen:**
1. Roep HomePage aan met error state
2. Mock useHome retourneert error

**Testgegevens:**
- useHome mock retourneert: `{ home: [], loading: false, error: new Error('fail') }`

**Verwacht Resultaat:**
- Foutmelding "Failed to load content." wordt weergegeven
- Geen inhoud is zichtbaar

### 2. Carousel Tests

#### Scenario 2.1: Carousel Navigatie met Dots
**Stappen:**
1. Render carousel met 3 afbeeldingen
2. Initieel is dot 0 actief (roze achtergrond)
3. Klik op dot 1
4. Verifieer dat dot 1 nu actief is

**Testgegevens:**
- images array: ['a.jpg', 'b.jpg', 'c.jpg']
- autoPlay: false

**Verwacht Resultaat:**
- Dot 0 start met klasse 'bg-pink-600' (actief)
- Dot 1 krijgt klasse 'bg-pink-600' na klik
- Slide indicator verandert

#### Scenario 2.2: Carousel Navigatie met Pijlen
**Stappen:**
1. Render carousel met 3 afbeeldingen
2. Dot 0 is actief
3. Klik "next" knop
4. Verifieer dot 1 is actief
5. Klik "previous" knop
6. Verifieer dot 0 is actief

**Testgegevens:**
- images array: ['a.jpg', 'b.jpg', 'c.jpg']
- autoPlay: false

**Verwacht Resultaat:**
- Next/previous knoppen werken correct
- Indicatoren updaten bij navigatie
- Carousel cycled through slides

### 3. Access Control Tests

#### Scenario 3.1: PrivateRoute Toont Content voor Geauthenticeerde Gebruiker
**Stappen:**
1. Render PrivateRoute met geauthenticeerde user
2. Mock useAuth retourneert user object

**Testgegevens:**
- useAuth mock: `{ user: { name: 'Eline' }, loading: false }`

**Verwacht Resultaat:**
- Beschermde inhoud ("Protected Content") wordt weergegeven
- Geen redirect naar login

#### Scenario 3.2: PrivateRoute Redirect naar Login voor Niet-Geauthenticeerde Gebruiker
**Stappen:**
1. Render PrivateRoute zonder geauthenticeerde user
2. Mock useAuth retourneert user: null

**Testgegevens:**
- useAuth mock: `{ user: null, loading: false }`

**Verwacht Resultaat:**
- Redirect naar "/auth" wordt geactiveerd
- Beschermde inhoud is niet zichtbaar

### 4. Input Component Tests

#### Scenario 4.1: URL-Normalisatie (Protocol Toevoegen)
**Stappen:**
1. Render InputWithFavicon met waarde "example.com"
2. Klik op input veld
3. Tab naar volgende veld (blur event)
4. Verifieer URL is genormaliseerd

**Testgegevens:**
- Input waarde: "example.com"
- Verwacht na blur: "https://example.com"

**Verwacht Resultaat:**
- Protocol (https://) wordt automatisch toegevoegd
- onChange event wordt aangeroepen met genormaliseerde URL
- Input bevat volledige URL

#### Scenario 4.2: Favicon Preview voor Geldig Domein
**Stappen:**
1. Render InputWithFavicon
2. Voer geldige domein in: "example.com"
3. Wacht op debounce timer
4. Verifieer favicon afbeelding verschijnt

**Testgegevens:**
- Input waarde: "example.com"
- Favicon URL: bevat "example.com"

**Verwacht Resultaat:**
- Favicon preview afbeelding wordt geladen
- Afbeelding src bevat Google favicon service URL
- Afbeelding is zichtbaar in input

### 5. UI Component Tests

#### Scenario 5.1: Button Destructive Variant
**Stappen:**
1. Render Button met variant="destructive"
2. Controleer className

**Testgegevens:**
- Props: `{ variant: "destructive" }`

**Verwacht Resultaat:**
- Button bevat klasse 'bg-red-500'
- Destructive stijl is toegepast

#### Scenario 5.2: Button Large Size
**Stappen:**
1. Render Button met size="lg"
2. Controleer className

**Testgegevens:**
- Props: `{ size: "lg" }`

**Verwacht Resultaat:**
- Button bevat klasse 'h-11'
- Large size stijl is toegepast

### 6. Utility Function Tests

#### Scenario 6.1: Class Name Utility (cn)
**Stappen:**
1. Roep cn('a', false && 'b', 'c') aan
2. Verifieer output

**Testgegevens:**
- Input: 'a', false && 'b', 'c'

**Verwacht Resultaat:**
- Output: 'a c'
- Falsy waarden worden gefilterd
- Truthy waarden worden gekoppeld

#### Scenario 6.2: Favicon URL Constructor
**Stappen:**
1. Roep getFaviconUrl('example.com') aan
2. Verifieer gegenereerde URL

**Testgegevens:**
- Input domein: 'example.com'

**Verwacht Resultaat:**
- URL bevat 'google.com/s2/favicons'
- URL bevat 'domain=example.com' parameter
- URL is geldig en kan opgehaald worden

### 7. Data Fetching Hook Tests

#### Scenario 7.1: useHome Hook Laadt Data Succesvol
**Stappen:**
1. Render component met useHome hook
2. Mock fetch retourneert geslaagde response
3. Wacht op data laden

**Testgegevens:**
- Fetch mock retourneert: JSON array []
- Loading state: true → false

**Verwacht Resultaat:**
- loading begint als true
- loading wordt false na fetch
- error blijft null
- Data array is ingesteld

#### Scenario 7.2: useHome Hook Handelt Fetch Error Af
**Stappen:**
1. Render component met useHome hook
2. Mock fetch reject/failed response
3. Wacht op error afhandeling

**Testgegevens:**
- Fetch mock retourneert failed response (ok: false)

**Verwacht Resultaat:**
- loading wordt false
- error wordt ingesteld
- Component toont error state correct

#### Scenario 7.3: useRules Hook Laadt Data Succesvol
**Stappen:**
1. Render component met useRules hook
2. Mock fetch retourneert geslaagde response
3. Wacht op data laden

**Testgegevens:**
- Fetch mock retourneert: JSON array []

**Verwacht Resultaat:**
- loading begint als true
- loading wordt false na fetch
- RulesContent array bevat data

#### Scenario 7.4: useRules Hook Handelt Fetch Error Af
**Stappen:**
1. Render component met useRules hook
2. Mock fetch reject/failed response

**Testgegevens:**
- Fetch mock retourneert failed response

**Verwacht Resultaat:**
- loading wordt false
- error wordt ingesteld

### 8. Backend API Tests

#### Scenario 8.1: Test Endpoint Retourneert Status 200
**Stappen:**
1. Maak GET request naar /api/test
2. Verifieer response

**Testgegevens:**
- Request: GET /api/test

**Verwacht Resultaat:**
- Status code: 200
- Response bevat: `{ message: "Backend is working!" }`

#### Scenario 8.2: Home Endpoint Retourneert JSON Array
**Stappen:**
1. Maak GET request naar /api/home
2. Verifieer response type

**Testgegevens:**
- Request: GET /api/home

**Verwacht Resultaat:**
- Status code: 200
- Response is een JSON array
- Array kan leeg of gevuld zijn

#### Scenario 8.3: Rules Endpoint Retourneert JSON Array
**Stappen:**
1. Maak GET request naar /api/rules
2. Verifieer response type

**Testgegevens:**
- Request: GET /api/rules

**Verwacht Resultaat:**
- Status code: 200
- Response is een JSON array
- Array kan leeg of gevuld zijn



## Test Statistieken

| Type | Aantal | Status |
|------|--------|--------|
| Frontend Tests | 18 | ✅ Groen |
| Backend Tests | 3 | ✅ Groen |
| Totaal | 21 | ✅ 100% Groen |
