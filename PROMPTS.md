# Promptlog

> Claude voegt hier automatisch een entry toe na elke compositie die aangemaakt of aangepast wordt.
> Formaat: datum — auteur — bestandsnaam · prompt · assets · iteratie · notities

---

## 2026-06-15 — Paul — asset-vrije onderdelen (storyboard-herziening)

**Prompt:**
> run scenes.md — SCENES.md herzien naar volledige ~32s storyboard (5 scenes + transitions +
> herbruikbare tussentekst). Bouw nu alleen de asset-vrije onderdelen; scene2/3/4 + cursor wachten
> op de NL-SVG-exports.

**Bestanden:**
- `compositions/scene1-logo-intro.html` (herschreven: 5s, rustige fade-in + lichte scale-up, geen flits)
- `compositions/transition-wipe.html` (nieuw, herbruikbaar T1 & T2: mint-groen #3fd6a0, vars `tekst`+`duur`)
- `compositions/scene-tussentekst.html` (nieuw, herbruikbaar: licht blauw #ceecff, var `tekst`+`duur`)
- `compositions/scene5-logo-outro.html` (nieuw: donkerblauw, logo + CTA met URL)
- `index.html` (review-reel ~14s; placeholders voor scene2/3/4)

**Verwijderd:** `generic-tansition-1.html`, `scene2-tussen-scherm.html` (achterhaald door de herziene brief)
**Assets:** `cardano_logo_white.svg`, `background-music.wav`
**Iteratie:** v1

**Notities:**
Asset-namen in de brief (figma-dashboard-overview-nl / figma-charts-panel-nl / figma-controls-panel-nl
/ figma-cursor) bestaan nog niet; gebruiker levert de NL-exports later aan → scene2/3/4 op ⏳.
Kleurreis donkerblauw → mint-groene wipe → licht blauw → mint-groene wipe → donkerblauw werkt
(snapshot-geverifieerd). Transitions verbergen de cuts; T1 draagt de openingstekst (donkere tekst op
groen voor contrast). transition-wipe: groen vlak schuift in (power2.inOut), houdt vast om de cut te
maskeren, schuift uit en onthult de volgende scene. T1 op 2s (leesbare tekst), T2 op 1,2s. Reel-timing
van de transitions is gekalibreerd op de huidige (tijdelijke) scene-cuts; wordt herijkt zodra scene2/3/4
erin staan. Lint 0 errors, validate geen console errors. Muziek-fade-out in laatste seconde nog te doen
zodra de volledige timeline staat. Klaar voor review.

---

## 2026-06-15 — Paul — generic-tansition-1.html

**Prompt:**
> Plaats de generieke transitie tussen scene 1 en 2. Een solide kleurvlak veegt diagonaal over
> het scherm (linksboven → rechtsonder) en onthult de volgende scene bij de terugkeer. Twee fases
> van elk 1s, scènewissel op exact t=1s (50%). position:fixed, z-index 9999, will-change:transform,
> solide background-color (geen gradiënt/transparantie). Kleur #1A1A2E (placeholder → gewenste hex).

**Bestand:** `compositions/generic-tansition-1.html` (gekoppeld in `index.html`, track 2)
**Assets:** —
**Iteratie:** v1

**Notities:**
130%-vlak van translate(-110%,-110%) → (0,0) op exact t=1s → (110%,110%). Twee fases: power2.in
(fase 1) + power2.out (fase 2) = symmetrische ease-in-out met max snelheid op het midden (geen
pauze), render-veilig zonder CustomEase-plugin; benadert de gevraagde cubic-bezier(0.76,0,0.24,1).
Kleur = Electric blue #ceecff (stijlgids: "transitions altijd in Electric blue"; #1A1A2E was een
placeholder). Duur: header zei 1,4s maar de animatiewensen (2×1s, wissel op 50%) zijn consistent
op 2s → comp = 2s gebouwd; de zichtbare veeg duurt ~1,1s (off-screen delen tonen niet), wat dicht
bij de 1,4s ligt. Placement gekalibreerd op data-start="2.5" zodat de volledige dekking exact op
de cut (4,0s) valt — er bleek een consistente ~0,5s offset tussen nominale en effectieve substart
(empirisch: dekkingstijd = nominale start + 1,5). Lint 0 errors, validate geen console errors.

---

## 2026-06-15 — Paul — scene1-logo-intro.html

**Prompt:**
> Run scenes.md — scene1-logo-intro: donkerblauwe achtergrond waar het logo geanimeerd
> binnenkomt, "PensionSim" eronder in wit (Noto Sans). Logo middle & centered, geanimeerd
> gelijk aan de hero-logo op cardano.nl (div.hero-homepage__logo--light).

**Bestand:** `compositions/scene1-logo-intro.html`
**Assets:** `assets/cardano_logo_white.svg`, `assets/background-music.wav`
**Iteratie:** v1

**Notities:**
SVG inline geplakt zodat het wordmark te animeren is. Cardano.nl hero-animatie kon niet uit
de live site gelezen worden (geen animatie-CSS bereikbaar via fetch); geïnterpreteerd als een
links-naar-rechts onthulling (clip-path wipe, power3.inOut) — past bij de hero-stijl. Subtiele
opkomst (y + opacity, expo.out) + radial glow voor diepte. "PensionSim" fadet daarna in.
Achtergrond #000f47 (stijlgids). Lint 0 errors, validate geen console errors. Klaar voor review.

---

## 2026-06-15 — Paul — scene2-tussen-scherm.html

**Prompt:**
> Run scenes.md — scene2-tussen-scherm: donkerblauwe achtergrond met witte titel
> "Ervaar om bestuurder in de WTP te zijn", middle & centered. Titel komt smooth & slow
> het scherm binnen vanuit rechts (middle aligned).

**Bestand:** `compositions/scene2-tussen-scherm.html`
**Assets:** `assets/background-music.wav`
**Iteratie:** v1

**Notities:**
Titel schuift vanaf rechts in (x: 1100 → 0) over 1.2s met power2.out (smooth & slow) + fade.
Noto Sans 900, gecentreerd, 2s. Gekoppeld in index.html met data-start="scene1". Muziek nu 6s
(scene1 4s + scene2 2s). Lint 0 errors, validate geen console errors. Klaar voor review.

---
