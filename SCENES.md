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
| 2 | `compositions/scene2-dashboard.html` | 0:05–0:07 | Overzichtsdashboard met de drie profielen |
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
**Duur:** ~3 s (0:05–0:07)
**Assets:**
- `assets/figma-dashboard-overview-nl.svg` (Nederlandstalig dashboard met de drie profielen + grafieken eronder)
- `assets/profile-1.svg` (Kaart Peter - happy)
- `assets/profile-2.svg` (Kaart Naomi - neutraal)
- `assets/profile-3.svg` (Kaart Mike - unhappy)

**Beschrijving:**
Het overzichtsdashboard verschijnt als zwevend tablet (enigzins herkenbaar als ipad maar gestileerd, met tablet dimensions) venster op de **donker blauwe** achtergrond. 
En scrollt in het zwevende app venster het dashboard door.  
**Nederlandstalige** schermversie gebruiken.

**Animatiewensen:**
- Tablet venster komt rustig binnen met heel lichte scale-up + zachte schaduw (`power2.out`, ~0.8 s).
- De figma-dashboard-overview-nl.svg wordt rustig op de tablet doorgescrolt. 
- Als de deze volledig is doorgescrollt verschijnen vanaf de bovenzijde van het screen drie cards in beeld. 
- De cards hebben een borderradius van 25px, en een padding van 20px.
- De worden horizontaal naast elkaar met een nette gutter voor tussenruimte, over de tablet geplaatst.
- Per card toont een profiel. Gebruik hier voor de profile svgs.
- Korte standtijd, dan tussentekst "Doorleef verschillende scenario's" (0:07).

---

## scene3-charts ⏳ (wacht op NL-asset)

**Bestand:** `compositions/scene3-charts.html`
**Duur:** ~5 s (0:07–0:12)
**Assets:**
- `assets/figma-charts-panel-nl.svg` (Nederlandstalige scenario-/marktdata-grafieken: vermogensallocatie, reserve, pensioen vs prijsindex, marktdata)

**Beschrijving:**
Aandacht verschuift naar de scenario- en marktdata-grafieken. Panelen schuiven rustig naar voren zodat ze goed leesbaar zijn; lijnen en vlakken tekenen zich kalm op. **Nederlandstalige** labels.

**Animatiewensen:**
- Grafiekpanelen schuiven rustig naar voren (`power2.out`).
- Lijn-grafieken "draw-on", vlakdiagram bouwt rustig van onder op.
- Staggered per paneel, ~0.3 s tussen elk — bewust kalm tempo.
- Daarna tussentekst "Ontdek hoe jouw beleggingsstrategie uitpakt" (0:12).

---

## scene4-controls ⏳ (wacht op NL-asset + cursor)

**Bestand:** `compositions/scene4-controls.html`
**Duur:** ~14 s (0:12–0:28)
**Assets:**
- `assets/figma-controls-panel-nl.svg` (Nederlandstalig beleidspaneel: sliders, cohort-grafieken, wijzigingen-tabel, knoppen incl. "Uitvoeren")
- `assets/figma-cursor.svg` (muiscursor)

**Beschrijving:**
Het beleidsgedeelte. Het control-paneel komt rustig in beeld. In plaats van de eerdere pop-ups wordt nu **langzaam naar beneden gescrold** door het paneel, zodat de sliders en grafieken vanzelf in beeld komen — de pop-ups zijn daarmee niet meer nodig. Een cursor beweegt kalm over de interface. **Nederlandstalige** labels en knoppen.

**Animatiewensen:**
- Paneel rustig in beeld (`power2.out`).
- **Vertraagde scroll** naar beneden door het paneel (`sine.inOut`, ruim uitgesmeerd over de scene) — dit vervangt de pop-ups.
- Cursor beweegt kalm tussen de controls (`sine.inOut`); sliders en grafieken reageren rustig mee.
- Wijzigingen-tabel: getallen rustig faden in.
- Geen snelle bewegingen — alles goed leesbaar en te volgen.
- Slot: rustige overgang naar T2.

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
