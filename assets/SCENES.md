# Scenes

> Dit bestand beschrijft elke scene: wat er te zien is, welke assets gebruikt worden en wat er geanimeerd moet worden.
> Claude leest dit als creative brief bij het schrijven van composities.

> Use the attached background music for the video


**Assets:**
- `assets/background-music.wav`


---

## generic-transition 👀

**Bestand:** `compositions/generic-tansition-1.html`
**Duur:** 1.4 s
**Assets:**

**Beschrijving:**
Dit is de generieke transitie tussen twee scenes. Een solide kleurvlak veegt diagonaal over het scherm — van linksboven naar rechtsonder — en onthult de volgende scene bij de terugkeer.

Kleur: #1A1A2E (vervang dit door de gewenste hexcode)


**Animatiewensen:**
De transitie bestaat uit twee fases van elk 1 s, aangedreven door één diagonale wipe.
Fase 1 — Sluit de huidige scene af (0 s → 1 s)

Een rechthoekig vlak in de opgegeven transitiekleur start buiten beeld linksboven (translate: -110% -110%) en beweegt via een cubic-bezier(0.76, 0, 0.24, 1) curve naar het midden van het scherm (translate: 0% 0%). Het vlak is iets groter dan het viewport (130 % breedte en hoogte) zodat diagonale randen nooit een kale rand tonen. Op het moment dat het vlak het scherm volledig bedekt (precies op 1 s) wisselt de onderliggende scene.
Fase 2 — Onthul de nieuwe scene (1 s → 2 s)

Het vlak zet zijn beweging ononderbroken voort in dezelfde diagonale richting naar rechtsonder (translate: 110% 110%), waarmee het nieuwe scherm van linksboven naar rechtsonder wordt onthuld. De easing is een gespiegelde cubic-bezier(0.76, 0, 0.24, 1) zodat de in- en uitbeweging symmetrisch aanvoelen — het vlak versnelt licht weg en komt niet abrupt tot stilstand.
Timing & gevoel:

De totale beweging (entry + exit) beschrijft één vloeiende diagonale boog zonder pauze in het midden. De easing mag ook worden uitgedrukt als ease-in-out met een custom duration-bezier als de tool dat ondersteunt. Het geheel moet aanvoelen als een camerabeweging in een speelfilm: doelgericht, zacht en zonder schokken.
Technische aandachtspunten:

Gebruik will-change: transform op het transitievlak voor GPU-compositing.
De scènewisseling vindt plaats op exact t = 1 s (50 % van de totale duur), niet eerder.
Het vlak gebruikt position: fixed en z-index: 9999 zodat het altijd bovenop alle scène-elementen ligt.
De kleur van het vlak is een enkelvoudige background-color; geen gradiënten, geen transparantie.

---

## scene1-logo-intro 👀

**Bestand:** `compositions/scene1-logo-intro.html`
**Duur:** 4 s
**Assets:**
- `assets/cardano_logo_white.svg`

**Beschrijving:**
Donkerblauwe achtergrond waar het logo geanimeerd binnenkomt. 
Hieronder verschijnt de tekst "PensionSim" in het wit in het lettertype Noto Sans .


**Animatiewensen:**
Positie van het logo: middle and centered.
Animneer het logo gelijk aan de geanimeerde svg op http://www.cardano.nl in de div.hero-homepage__logo hero-homepage__logo--light


---

## scene2-tussen-scherm 👀

**Bestand:** `compositions/scene2-tussen-scherm.html`
**Duur:** 2 s
**Assets:**

**Beschrijving:**
Donkerblauwe achtergrond met een witte titel.
De titel is: Ervaar om bestuurder in de WTP te zijn


**Animatiewensen:**
Positie de titel: middle and centered.
Animatie: Titel komt het scherm binnen van uit het rechts (middle aligned), smooth & slow.


---