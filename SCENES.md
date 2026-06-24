# Scenes

> Dit bestand beschrijft elke scene: wat er te zien is, welke assets gebruikt worden en wat er geanimeerd moet worden.
> Claude leest dit als creative brief bij het schrijven van composities.
>
> **Totale duur:** ~32 s · **Canvas:** 1920×1080 · **30 fps**
> **Taal:** Alles in het **Nederlands** — zowel de teksten in de video als de visuals/schermen van de Sim (NL-versie van de PensionSim-screenshots gebruiken).
> **Achtergrondmuziek:** `assets/background-music.wav` (rustig muziekje, versie zoals gestuurd naar Jordi; eigen variant bespreekbaar). Loopt over de volledige video, fade-out in de laatste seconde.
> **Tempo & leesbaarheid:** Schermen en overgangen bewust **rustig** houden. Geef elk scherm en elke tekst ruim de tijd om gelezen te worden — ook prettig leesbaar voor oudere bestuurders. Geen snelle flitsen of jump-cuts; zachte, kalme bewegingen.
>
> **Kleuren**
> | Rol | Hex |
> |------|------|
> | Achtergrond opening/outro (donkerblauw) | `#000f47` |
> | Achtergrond canvas (licht blauw) | `#ceecff` |
> | Logo & openingstekst (wit) | `#ffffff` |
> | Transition mint-groen | `#3fd6a0` |
>
> **Belangrijke kleurwissel:** de video **opent in donkerblauw** (`#000f47`) met wit logo + witte tekst, en gaat via een **groene overgang naar licht blauw** (`#ceecff`) voor het Sim-gedeelte.
>
> **Typografie:** Noto Sans (700–900 weight). Openingstekst "PensionSim" in het wit.

---

## Scene-overzicht

| # | Bestand | Tijd | Inhoud |
|---|---------|------|--------|
| 1 | `compositions/scene1-logo-intro.html` | 0:00–0:05 | Wit Cardano-logo op donkerblauw + witte tekst "PensionSim" |
| T1 | `compositions/transition-wipe.html` | ~0:01 → | Groene overgang van donkerblauw naar licht blauw, met tekst "Ervaar om bestuurder in de WTP te zijn" |
| 2 | `compositions/scene2-dashboard.html` | 0:05–0:13 | Langzame scroll door het volledige dashboard, daarna drie profielkaarten met progress bars |
| TX | `compositions/scene-tussentekst.html` | 0:07 | Licht blauw scherm: "Doorleef verschillende scenario's" |
| 3 | `compositions/scene3-charts.html` | 0:07–0:12 | Scenario / marktdata-grafieken |
| TX | `compositions/scene-tussentekst.html` | 0:12 | Groen → licht blauw: "Ontdek hoe jouw beleggingsstrategie uitpakt" |
| 4 | `compositions/scene4-controls.html` | 0:12–0:28 | Beleidsgedeelte: sliders + rustige scroll naar beneden |
| T2 | `compositions/transition-wipe.html` | ~0:27 → | Groene overgang naar outro |
| 5 | `compositions/scene5-logo-outro.html` | 0:28–0:32 | Call to action |

> Scenes 2–4 spelen op één doorlopend "canvas" (zwevende app-vensters op de licht blauwe achtergrond) en mogen desgewenst tot één compositie `scene2-4-canvas.html` worden samengevoegd; hieronder staan ze los beschreven voor de duidelijkheid.

---

## scene1-logo-intro 👀

**Bestand:** `compositions/scene1-logo-intro.html`
**Duur:** 5 s
**Assets:**
- `assets/cardano_logo_white.svg` (wit logo)

**Beschrijving:**
**Donkerblauwe achtergrond (`#000f47`)** met het Cardano-logo in **wit**, gecentreerd. Daaronder verschijnt in het **wit** de tekst **"PensionSim"** in het lettertype **Noto Sans**, uppercase.

**Animatiewensen:**
- Logo rustig fade-in + heel lichte scale-up (kalm, `power2.out`, ~1.0 s). Geen flits.
- "PensionSim" verschijnt zacht onder het logo (`power2.out`, ~0.8 s), met genoeg rust om te lezen.
- Tegen het einde van de scene zet de kleurwissel in: zie T1 (groene overgang naar licht blauw).

---

## transition-wipe  (T1 & T2) 👀

**Bestand:** `compositions/transition-wipe.html`
**Duur:** ~0.8 s (rustig, niet te snel)
**Assets:** geen (puur CSS/SVG)

**Beschrijving:**
Mint-groene (`#3fd6a0`) overgang die kalm over het scherm veegt en de achtergrond verwisselt. Bij **T1** is dit de kleurwissel van **donkerblauw → licht blauw (`#ceecff`)**. Bij **T2** de overgang van het Sim-canvas naar de outro.

**Tekst tijdens T1 (op ~0:01):** in de overgang van het openingsscherm naar licht blauw verschijnt de zin:
> **"Ervaar om bestuurder in de WTP te zijn"**

**Animatiewensen:**
- Groen vlak schuift rustig in en uit (`power2.inOut`, elk ~0.4 s) — bewust kalmer dan een snelle wipe.
- De zin verschijnt leesbaar in beeld tijdens de overgang en blijft lang genoeg staan om gelezen te worden.
- Embedden met lichte overlap, bv. `data-start="scene1 - 0.3"`, `data-track-index="2"`.

---

## scene-tussentekst  (herbruikbaar) 👀

**Bestand:** `compositions/scene-tussentekst.html`
**Duur:** ~2 s per keer (rustig leesbaar)
**Assets:** geen (tekst op achtergrond)
**Variabele:** `tekst` (de te tonen zin)

**Beschrijving:**
Een rustig **licht blauw scherm (`#ceecff`)** met één centrale zin in donkere/heldere leesbare tekst (Noto Sans, ruim formaat). Wordt twee keer ingezet:
- **Op 0:07** (na de profielen, vóór de scenario-marktdata): **"Doorleef verschillende scenario's"**
- **Op 0:12** (bij het volgende groene scherm dat naar licht blauw gaat): **"Ontdek hoe jouw beleggingsstrategie uitpakt"**

**Animatiewensen:**
- Zin fade-in van onder (`power2.out`, ~0.6 s), ruime standtijd, dan zachte fade-out.
- Geen drukke animatie — rust en leesbaarheid voorop.

---

## scene2-dashboard 👀

**Bestand:** `compositions/scene2-dashboard.html`
**Duur:** 8.0 s
**Assets:**
- `assets/figma-dashboard-overview-nl.svg` (Nederlandstalig dashboard, 1440×1609 px, weergegeven op ~1247 px hoogte in het tabletvenster van 756 px)
- `assets/profile-1.svg` (Kaart Peter - happy, groene balk)
- `assets/profile-2.svg` (Kaart Naomi - neutraal, blauwe balk)
- `assets/profile-3.svg` (Kaart Mike - unhappy, rode balk)

**Beschrijving:**
Het overzichtsdashboard verschijnt als een gestileerd tabletvenster (iPad-achtig, 1160×800 px) op de **licht blauwe** achtergrond (`#ceecff`). Het dashboard scrollt langzaam van boven naar beneden zodat de volledige pagina te zien is. Daarna verschijnen de drie profielkaarten. **Nederlandstalige** schermversie gebruiken.

**Animatietijdlijn:**

| Tijdstip | Actie |
|----------|-------|
| 0.0 s | Tablet fadeert rustig in met lichte scale-up (`power2.out`, 0.8 s) |
| 0.8 s | Dashboard begint **langzaam** omhoog te scrollen (`power1.inOut`, 3.2 s, 480 px) — laat de volledige pagina zien |
| 4.0 s | Scroll bereikt de onderkant; korte pauze van ~0.3 s |
| 4.05 s | Tablet wordt wazig (`blur 6px`, `power2.inOut`, 0.5 s) als diepte-effect vóór de kaarten |
| 4.30 s | Kaart 1 (Peter) daalt vanuit bovenzijde in beeld (`power2.out`, 0.55 s); caption schuift gelijktijdig in van rechts naar links (`power2.out`, 0.8 s) |
| 4.45 s | Kaart 2 (Naomi) daalt in beeld |
| 4.60 s | Kaart 3 (Mike) daalt in beeld |
| 4.95 s | Progress bar kaart 1 onthult van links naar rechts (witte cover schuift weg, `power2.inOut`, 0.7 s) |
| 5.10 s | Progress bar kaart 2 onthult |
| 5.25 s | Progress bar kaart 3 onthult |
| ~5.95 s | Laatste progress bar klaar; kaarten blijven ~2 s in beeld |
| 8.0 s | Einde scene |

**Overige details:**
- Caption: donkerblauwe achtergrond (`#000f47`), witte tekst "Doorleef verschillende scenario's", Noto Sans 700, 52 px; blijft op zijn positie staan in scene 3.
- Drie kaarten horizontaal naast elkaar, gecentreerd (1518 px breed, gap 24 px), `border-radius: 25px`, `padding: 20px`, witte achtergrond, zachte schaduw.
- Progress bar covers (witte vlakken die de gekleurde balk verbergen) zijn exact gepositioneerd op basis van de SVG-coördinaten: `left: 87px; top: 236px; height: 13px` — breedte varieert per kaart (313 px / 254 px / 254 px).
- Korte standtijd, dan tussentekst "Doorleef verschillende scenario's". **VOORLOPIG VERBORGEN.**

---

## scene3-charts 👀

**Bestand:** `compositions/scene3-charts.html`
**Duur:** ~5 s (0:07–0:12)
**Assets:**
- `assets/ratio-1.svg` (Kaart ratio)
- `assets/solidariteits-2.svg` (Kaart solidariteitsreserve)
- `assets/pensioen-3.svg` (Kaart pensioen)
- `assets/market-1.svg` (Kaart market)
- `assets/vervangingratio-2.svg` (Kaart vervangingsratio)

**Beschrijving:**
Scene 3 sluit naadloos aan op het eindshot van scene 2: het tablet staat al wazig in beeld (`blur(6px)`), het dashboard staat vast op de onderkant (`y: -480px`), en de drie profielkaarten zijn zichtbaar. Er wordt **niet opnieuw gescrolld**. De scene begint direct met de kaarten die weggaan en nieuwe kaarten die instromen.

**Licht blauwe** achtergrond (`#ceecff`). **Nederlandstalige** schermversie gebruiken.

**Aansluiting op scene 2 (eindstaat):**
- `#sc3-db-img` start op `y: -480` (via `gsap.set`) — zelfde positie als einde scene 2, geen scroll
- Tablet blijft wazig (`filter: blur(6px)`)
- Caption staat al zichtbaar op zijn vaste positie linksonder

**Animatietijdlijn:**

| Tijdstip | Actie |
|----------|-------|
| 0.0 s | Profielkaart 1 (Peter) verdwijnt naar onderzijde scherm (`power2.in`, 0.4 s) |
| 0.1 s | Profielkaart 2 (Naomi) verdwijnt |
| 0.2 s | Profielkaart 3 (Mike) verdwijnt |
| 0.8 s | Grafiekkaart 1 (ratio-1) daalt in vanuit bovenzijde (`power2.out`, 0.4 s) |
| 0.9 s | Grafiekkaart 2 (solidariteits-2) daalt in |
| 1.0 s | Grafiekkaart 3 (pensioen-3) daalt in |
| 1.3–2.4 s | Grafieklijntjes onthullen van links naar rechts per kaart (cover schuift weg, `power2.inOut`, 0.8 s) |
| 2.9–3.5 s | Golf 1-kaarten verdwijnen via bovenzijde scherm (`power2.in`, 0.4 s) |
| 3.7 s | Golf 2: kaart 1 (market-1) schuift in van links, kaart 2 (vervangingratio-2) van rechts (`power2.out`, 0.5 s) |
| 4.3–5.25 s | Grafieklijntjes golf 2 onthullen (`power2.inOut`, 0.8 s) |
| 6.0 s | Einde scene |

**Overige details:**
- Golf 1: 3 kaarten, 488×479 px elk, gap 24 px, gecentreerd (1512 px breed, left 204 px)
- Golf 2: 2 kaarten, `flex: 1` zodat ze samen dezelfde 1512 px breedte innemen
- Alle kaarten: `border-radius: 25px`, `padding: 20px`, witte achtergrond, zachte schaduw
- Grafiekcovers (`sc3-line-cover`): witte vlakken over het grafiekgebied, scaleX 1→0 (`transform-origin: right center`)

---

## scene4-controls ⏳ (cursor)

**Bestand:** `compositions/scene4-controls.html`
**Duur:** ~14 s (0:12–0:28)
**Assets:**
- `assets/figma-controls-panel-nl.svg` (Nederlandstalig beleidspaneel: sliders, cohort-grafieken, wijzigingen-tabel, knoppen incl. "Uitvoeren")
- `assets/cursor.svg` (muiscursor)

**Assets specifieke zaken**
- figma-controls-panel-nl: het menu (bestaande uit: overzicht, markt, nieuws, beleid) dient sticky te zijn en niet mee te scrollen. 
- Het block in de rechterkolom met als titel "Wijzigingen" dient ook sticky te zijn en niet mee te scrollen en dient direct in beeld te staan. Zorg dat de blauwe button ook op zijn positie blijft.
- Verberg het rechterblok op het scrollende gedeelte.
- Zorg voor eenzelfde achtergrond kleur (licht grijs).

**Beschrijving:**
Het beleidsgedeelte. Het control-paneel komt rustig in beeld. In plaats van de eerdere pop-ups wordt nu **langzaam naar beneden gescrold** door het paneel, zodat de sliders en grafieken vanzelf in beeld komen — de pop-ups zijn daarmee niet meer nodig. Het paneel dient iets groter te zijn in deze scene om leesbaarheid te waarborgen. 


**Animatiewensen:**
- Paneel rustig in beeld (`power2.out`).
- **Vertraagde scroll** naar beneden door het paneel (`sine.inOut`, ruim uitgesmeerd over de scene) — dit vervangt de pop-ups.
- De scroll wordt opgedeeld in secties, zodat deze goed leesbaar zijn.
- Wijzigingen-tabel: getallen rustig faden in.
- Geen snelle bewegingen — alles goed leesbaar en te volgen.
- Wanneer de scroll volledig is fade de cursor in beeld onder de "uitvoeren" knop op passende afstand.
- De cursor klikt de "Uitvoeren" knop, deze krijgt een klik animatie waarna rustig de overgang naar T2 start.

---

## scene5-logo-outro

**Bestand:** `compositions/scene5-logo-outro.html`
**Duur:** 4 s (0:28–0:32)
**Assets:**
- `assets/cardano_logo_white.svg` (wit logo)

**Beschrijving:**
Terug naar de **donkerblauwe** achtergrond (`#000f47`) met het Cardano-logo in **wit**. Daaronder de nieuwe **call to action**:
> **"Vraag nu jouw PensionSim workshop aan: www.cardano.nl/pensionsim"**

Rustige, statische eindkaart, ruim leesbaar.

**Animatiewensen:**
- Logo rustig fade-in + heel lichte scale-up (`power2.out`, ~1.0 s).
- Call-to-action-tekst fade-in van onder (`power2.out`), ~0.4 s na het logo; de URL goed leesbaar.
- Lange rust tot het einde (`tl.set({}, {}, 4)` om de scene op volle 4 s te houden).
- Achtergrondmuziek fade-out gelijk met het einde van deze scene.
