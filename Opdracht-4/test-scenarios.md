# Documentatie Testscenario's - PorkySMP

## Overzicht

| Categorie | Waarde |
|-----------|--------|
| **Totaal Testbestanden** | 10 |
| **Frontend Testbestanden** | 9 |
| **Backend Testbestanden** | 1 |

---

## Hoe tests uit te voeren

### Frontend tests

**1. Dependencies installeren:**
```bash
cd frontend
npm install
```

**2. Tests uitvoeren (niet-interactief):**
```bash
CI=true npm test -- --watchAll=false
```

**3. Met coverage rapport:**
```bash
CI=true npm test -- --coverage --watchAll=false
```

### Backend tests

**1. Dependencies installeren:**
```bash
cd backend
npm install
```

**2. Tests uitvoeren:**
```bash
npm test
```

---

## Overzicht testbestanden

| # | Testbestand | Doel | Type |
|---|-------------|------|------|
| 1 | `HomePage.test.js` | Homepage laden en rendering | Frontend |
| 2 | `Carousel.test.js` | Carousel slide-navigatie | Frontend |
| 3 | `PrivateRoute.test.js` | Toegangscontrole en redirects | Frontend |
| 4 | `InputWithFavicon.test.js` | URL-normalisatie en favicon preview | Frontend |
| 5 | `MarkdownContent.test.js` | Markdown-rendering | Frontend |
| 6 | `Button.test.js` | Button varianten en sizes | Frontend |
| 7 | `utils.test.js` | Utility functies (cn, getFaviconUrl) | Frontend |
| 8 | `useHome.test.js` | Homepage data-fetching hook | Frontend |
| 9 | `useRules.test.js` | Regels data-fetching hook | Frontend |
| 10 | `api.test.js` | Backend API endpoints | Backend |

---

## Testscenario's

### 1. Homepage tests

#### Scenario 1.1: Homepage laadt content

**Stappen:**
1. Roep de HomePage component aan met gemockte useHome hook
2. Mock retourneert geslaagde data met afbeeldingen

**Testgegevens:**
```javascript
useHome mock: { 
  home: [{ images: [] }], 
  loading: false, 
  error: null 
}
```

**Verwacht resultaat:**
-  Titel "Porky SMP" wordt getoond
-  Link naar rules pagina is aanwezig
-  Geen foutmelding zichtbaar

---

#### Scenario 1.2: Homepage toont loading-status

**Stappen:**
1. Roep HomePage aan met loading state
2. Mock useHome retourneert loading=true

**Testgegevens:**
```javascript
useHome mock: { 
  home: [], 
  loading: true, 
  error: null 
}
```

**Verwacht resultaat:**
-  Bericht "Loading content…" wordt weergegeven
-  Geen inhoud is zichtbaar

---

#### Scenario 1.3: Homepage toont fout bij mislukken

**Stappen:**
1. Roep HomePage aan met error state
2. Mock useHome retourneert error

**Testgegevens:**
```javascript
useHome mock: { 
  home: [], 
  loading: false, 
  error: new Error('fail') 
}
```

**Verwacht resultaat:**
-  Foutmelding "Failed to load content." wordt weergegeven
-  Geen inhoud is zichtbaar

---

### 2. Carousel tests

#### Scenario 2.1: Carousel navigatie met dots

**Stappen:**
1. Render carousel met 3 afbeeldingen
2. Initieel is dot 0 actief (roze achtergrond)
3. Klik op dot 1
4. Verifieer dat dot 1 nu actief is

**Testgegevens:**
```javascript
images: ['a.jpg', 'b.jpg', 'c.jpg']
autoPlay: false
```

**Verwacht resultaat:**
- Dot 0 start met klasse 'bg-pink-600' (actief)
- Dot 1 krijgt klasse 'bg-pink-600' na klik
- Slide indicator verandert

---

#### Scenario 2.2: Carousel navigatie met pijlen

**Stappen:**
1. Render carousel met 3 afbeeldingen
2. Dot 0 is actief
3. Klik "next" knop → Verifieer dot 1 is actief
4. Klik "previous" knop → Verifieer dot 0 is actief

**Testgegevens:**
```javascript
images: ['a.jpg', 'b.jpg', 'c.jpg']
autoPlay: false
```

**Verwacht resultaat:**
- Next/previous knoppen werken correct
- Indicatoren updaten bij navigatie
- Carousel werkt zoals verwacht

---

### 3. Access control tests

#### Scenario 3.1: PrivateRoute voor geauthenticeerde gebruiker

**Stappen:**
1. Render PrivateRoute met geauthenticeerde user
2. Mock useAuth retourneert user object

**Testgegevens:**
```javascript
useAuth mock: { 
  user: { name: 'Eline' }, 
  loading: false 
}
```

**Verwacht resultaat:**
-  Beschermde inhoud ("Protected Content") wordt weergegeven
-  Geen redirect naar login

---

#### Scenario 3.2: PrivateRoute redirect voor niet-geauthenticeerde gebruiker

**Stappen:**
1. Render PrivateRoute zonder geauthenticeerde user
2. Mock useAuth retourneert user: null

**Testgegevens:**
```javascript
useAuth mock: { 
  user: null, 
  loading: false 
}
```

**Verwacht resultaat:**
-  Redirect naar "/auth" wordt geactiveerd
-  Beschermde inhoud is niet zichtbaar

---

### 4. Input component tests

#### Scenario 4.1: URL-normalisatie (protocol toevoegen)

**Stappen:**
1. Render InputWithFavicon met waarde "example.com"
2. Klik op input veld
3. Tab naar volgende veld (blur event)
4. Verifieer URL is genormaliseerd

**Testgegevens:**
```
Input waarde: "example.com"
Verwacht na blur: "https://example.com"
```

**Verwacht resultaat:**
-  Protocol (https://) wordt automatisch toegevoegd
-  onChange event wordt aangeroepen met genormaliseerde URL
-  Input bevat volledige URL

---

#### Scenario 4.2: Favicon preview voor geldig domein

**Stappen:**
1. Render InputWithFavicon
2. Voer geldige domein in: "example.com"
3. Wacht op debounce timer
4. Verifieer favicon afbeelding verschijnt

**Testgegevens:**
```
Input waarde: "example.com"
Favicon URL: bevat "example.com"
```

**Verwacht resultaat:**
-  Favicon preview afbeelding wordt geladen
-  Afbeelding src bevat Google favicon service URL
-  Afbeelding is zichtbaar in input

---

### 5. UI component tests

#### Scenario 5.1: Button destructive variant

**Stappen:**
1. Render Button met variant="destructive"
2. Controleer className

**Testgegevens:**
```javascript
Props: { variant: "destructive" }
```

**Verwacht resultaat:**
-  Button bevat klasse 'bg-red-500'
-  Destructive stijl is toegepast

---

#### Scenario 5.2: Button large size

**Stappen:**
1. Render Button met size="lg"
2. Controleer className

**Testgegevens:**
```javascript
Props: { size: "lg" }
```

**Verwacht resultaat:**
-  Button bevat klasse 'h-11'
-  Large size stijl is toegepast

---

### 6. Utility function tests

#### Scenario 6.1: Class name utility (cn)

**Stappen:**
1. Roep cn('a', false && 'b', 'c') aan
2. Verifieer output

**Testgegevens:**
```javascript
Input: 'a', false && 'b', 'c'
```

**Verwacht resultaat:**
```
Output: 'a c'
```
-  Falsy waarden worden gefilterd
-  Truthy waarden worden gekoppeld

---

#### Scenario 6.2: Favicon URL constructor

**Stappen:**
1. Roep getFaviconUrl('example.com') aan
2. Verifieer gegenereerde URL

**Testgegevens:**
```
Input domein: 'example.com'
```

**Verwacht resultaat:**
-  URL bevat 'google.com/s2/favicons'
-  URL bevat 'domain=example.com' parameter
-  URL is geldig en kan opgehaald worden

---

### 7. Data fetching hook tests

#### Scenario 7.1: useHome hook laadt data succesvol

**Stappen:**
1. Render component met useHome hook
2. Mock fetch retourneert geslaagde response
3. Wacht op data laden

**Testgegevens:**
```javascript
Fetch mock retourneert: JSON array []
```

**Verwacht resultaat:**

**Loading state flow:**
```
loading: true → fetch → loading: false
```
-  Loading begint als true
-  Loading wordt false na fetch
-  Error blijft null
-  Data array is ingesteld

---

#### Scenario 7.2: useHome hook handelt fetch error af

**Stappen:**
1. Render component met useHome hook
2. Mock fetch reject/failed response
3. Wacht op error afhandeling

**Testgegevens:**
```javascript
Fetch mock retourneert: failed response (ok: false)
```

**Verwacht resultaat:**
- Loading wordt false
- Error wordt ingesteld
- Component toont error state correct

---

#### Scenario 7.3: useRules hook laadt data succesvol

**Stappen:**
1. Render component met useRules hook
2. Mock fetch retourneert geslaagde response
3. Wacht op data laden

**Testgegevens:**
```javascript
Fetch mock retourneert: JSON array []
```

**Verwacht resultaat:**

**Loading state flow:**
```
loading: true → fetch → loading: false
```
-  Loading begint als true
-  Loading wordt false na fetch
-  RulesContent array bevat data

---

#### Scenario 7.4: useRules hook handelt fetch error af

**Stappen:**
1. Render component met useRules hook
2. Mock fetch reject/failed response

**Testgegevens:**
```javascript
Fetch mock retourneert: failed response
```

**Verwacht resultaat:**
-  Loading wordt false
-  Error wordt ingesteld

---

### 8. Backend API tests

#### Scenario 8.1: Test endpoint retourneert status 200

**Stappen:**
1. Maak GET request naar /api/test
2. Verifieer response

**Testgegevens:**
```
Request: GET /api/test
```

**Verwacht resultaat:**

| Property | Waarde |
|----------|--------|
| Status code | 200 |
| Response | `{ message: "Backend is working!" }` |

---

#### Scenario 8.2: Home endpoint retourneert JSON array

**Stappen:**
1. Maak GET request naar /api/home
2. Verifieer response type

**Testgegevens:**
```
Request: GET /api/home
```

**Verwacht resultaat:**

| Property | Waarde |
|----------|--------|
| Status code | 200 |
| Response type | JSON array |
| Content | Kan leeg of gevuld zijn |

---

#### Scenario 8.3: Rules endpoint retourneert JSON array

**Stappen:**
1. Maak GET request naar /api/rules
2. Verifieer response type

**Testgegevens:**
```
Request: GET /api/rules
```

**Verwacht resultaat:**

| Property | Waarde |
|----------|--------|
| Status code | 200 |
| Response type | JSON array |
| Content | Kan leeg of gevuld zijn |

---

## Test statistieken

| Type | Aantal | Status | Percentage |
|------|--------|--------|------------|
| **Frontend Tests** | 18 | ✅ Groen | 85.7% |
| **Backend Tests** | 3 | ✅ Groen | 14.3% |
| **Totaal** | **21** | **✅ 100% Groen** | **100%** |

---


