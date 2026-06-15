# 🎬 Animatievideo Project — Claude Instructies

> **Stack:** HyperFrames · Claude Code · Git/GitHub · VS Code Live Share
> Docs: https://hyperframes.heygen.com/llms.txt

---

## Projectcontext

Product video op basis van Figma-exports en SVG-bestanden van schermen. De data is al zichtbaar in de beelden — het doel is animeren, niet opbouwen. Twee personen werken samen via VS Code Live Share en Git.

---

## Projectstructuur

```
my-video/
├── README.md                     ← technische instructies (dit bestand)
├── SCENES.md                     ← creative brief per scene
├── PROMPTS.md                    ← automatisch bijgehouden promptlog
├── meta.json
├── index.html                    ← root, koppelt alle scenes
├── compositions/
│   ├── scene1-logo-intro.html
│   ├── scene2-4-canvas.html
│   └── scene5-logo-outro.html
└── assets/
    ├── figma-cursors.svg
    ├── figma-logo-pieces.svg
    └── figma-logo-pills.svg
```

Assets komen **altijd** uit Figma of als SVG. Nooit zelf genereren.

---

## HyperFrames — structuur

### index.html — root koppelt scenes

```html
<div id="root" data-composition-id="my-video"
     data-start="0" data-width="1920" data-height="1080">

  <div id="scene1"
       data-composition-id="scene1-logo-intro"
       data-composition-src="compositions/scene1-logo-intro.html"
       data-start="0"
       data-track-index="1"></div>

  <div id="scene2"
       data-composition-id="scene2-4-canvas"
       data-composition-src="compositions/scene2-4-canvas.html"
       data-start="scene1"
       data-track-index="1"></div>

  <div id="scene5"
       data-composition-id="scene5-logo-outro"
       data-composition-src="compositions/scene5-logo-outro.html"
       data-start="scene2"
       data-track-index="1"></div>

  <script src="https://cdn.jsdelivr.net/npm/gsap@3/dist/gsap.min.js"></script>
  <script>
    const tl = gsap.timeline({ paused: true });
    window.__timelines = window.__timelines || {};
    window.__timelines["my-video"] = tl;
  </script>
</div>
```

### Sub-compositie — `<template>` wrapper verplicht

```html
<!-- compositions/scene1-logo-intro.html -->
<template id="scene1-logo-intro-template">
  <div data-composition-id="scene1-logo-intro" data-width="1920" data-height="1080">

    <img id="screen" class="clip"
         data-start="0" data-duration="5" data-track-index="0"
         src="../assets/figma-logo-pieces.svg"
         style="position:absolute; width:1920px; height:1080px; object-fit:cover;" />

    <style>
      [data-composition-id="scene1-logo-intro"] { background: #080B14; }
    </style>

    <script>
      const tl = gsap.timeline({ paused: true });
      tl.from("#screen", { opacity: 0, scale: 0.95, duration: 0.7, ease: "expo.out" }, 0);
      window.__timelines = window.__timelines || {};
      window.__timelines["scene1-logo-intro"] = tl;
    </script>
  </div>
</template>
```

---

## Data-attributen

### Timing

| Attribuut          | Voorbeeld          | Beschrijving                                                   |
|--------------------|--------------------|----------------------------------------------------------------|
| `data-start`       | `"0"` of `"scene1"` | Starttijd in seconden, of ID-referentie (relatieve timing)     |
| `data-duration`    | `"5"`              | Vereist voor `<img>`, optioneel voor video/audio, nooit op composities |
| `data-track-index` | `"1"`              | Z-volgorde (hoger = vooraan); clips op zelfde track mogen niet overlappen |

### Media

| Attribuut          | Voorbeeld | Beschrijving                                |
|--------------------|-----------|---------------------------------------------|
| `data-media-start` | `"2"`     | Trim-offset in de bronfile (seconden)       |
| `data-volume`      | `"0.8"`   | Volume 0–1                                  |
| `data-has-audio`   | `"true"`  | Geeft aan dat een videoclip audio bevat     |

### Composities hergebruiken met variabelen

Dezelfde compositie twee keer embedden met andere content:

```html
<!-- index.html -->
<div data-composition-id="screen-a"
     data-composition-src="compositions/screen-template.html"
     data-start="0" data-track-index="1"
     data-variable-values='{"src":"../assets/figma-cursors.svg","duration":"5"}'></div>

<div data-composition-id="screen-b"
     data-composition-src="compositions/screen-template.html"
     data-start="screen-a" data-track-index="1"
     data-variable-values='{"src":"../assets/figma-logo-pills.svg","duration":"4"}'></div>
```

```html
<!-- compositions/screen-template.html -->
<html data-composition-variables='[
  {"id":"src","type":"string","label":"Asset path","default":"../assets/figma-logo-pieces.svg"},
  {"id":"duration","type":"number","label":"Duration","default":"5"}
]'>
<body>
  <template id="screen-template-template">
    <div data-composition-id="screen-template" data-width="1920" data-height="1080">
      <img id="screen" class="clip" data-start="0" data-track-index="0"
           style="position:absolute; width:1920px; height:1080px;" />
      <script>
        const { src, duration } = __hyperframes.getVariables();
        document.querySelector("#screen").src = src;
        document.querySelector("#screen").setAttribute("data-duration", duration);
        const tl = gsap.timeline({ paused: true });
        tl.from("#screen", { opacity: 0, duration: 0.5, ease: "power2.out" }, 0);
        tl.set({}, {}, Number(duration)); // timeline uitbreiden tot clip-duur
        window.__timelines = window.__timelines || {};
        window.__timelines["screen-template"] = tl;
      </script>
    </div>
  </template>
</body>
</html>
```

### Relatieve timing

```html
data-start="scene1"         <!-- begint wanneer scene1 eindigt -->
data-start="scene1 + 0.5"   <!-- 0.5s na het einde van scene1 -->
data-start="scene1 - 0.3"   <!-- 0.3s overlap (voor transitions) -->
```

Regels: referentie werkt alleen binnen dezelfde compositie, geen circulaire verwijzingen, gerefereerde clip moet een bekende duur hebben.

---

## GSAP

### Basispatroon

```javascript
const tl = gsap.timeline({ paused: true }); // altijd paused: true

tl.from("#el", { opacity: 0, y: 30, duration: 0.5, ease: "expo.out" }, 0);  // 3e arg = absolute positie
tl.to("#el",   { opacity: 0, duration: 0.3, ease: "power2.in" }, 4.7);

// Verplicht: timeline registreren met exact de data-composition-id als sleutel
window.__timelines = window.__timelines || {};
window.__timelines["scene1-logo-intro"] = tl;
```

### Timeline uitbreiden tot clipduur

De compositieduur = `tl.duration()`. Als de laatste animatie eerder eindigt dan de beelden die je toont, wordt de compositie afgeknipt. Verleng altijd:

```javascript
// Afbeelding duurt 6 seconden, laatste animatie eindigt op 0.7s
tl.from("#screen", { opacity: 0, duration: 0.7, ease: "expo.out" }, 0);
tl.set({}, {}, 6); // verleng naar 6s — anders wordt de scene na 0.7s afgeknipt
```

### Beschikbare methoden

| Methode | Beschrijving |
|--------|-------------|
| `tl.from(target, vars, pos)` | Animeer vanuit waarden |
| `tl.to(target, vars, pos)` | Animeer naar waarden |
| `tl.fromTo(target, from, to, pos)` | Vanuit én naar waarden |
| `tl.set(target, vars, pos)` | Zet waarden direct (ook voor timeline verlengen via `tl.set({}, {}, N)`) |

### Animatiestijl — motion vocabulary

Beschrijf hoe een beweging moet voelen; Claude Code vertaalt dit naar de juiste ease:

| Beschrijving | GSAP ease        | Effect                       |
|-------------|------------------|------------------------------|
| smooth      | `power2.out`     | Natuurlijke vertraging       |
| snappy      | `power4.out`     | Snel en beslissend           |
| bouncy      | `back.out`       | Overshoots, dan tot rust     |
| springy     | `elastic.out`    | Trilt in positie             |
| dramatic    | `expo.out`       | Snelle start, lange glide    |
| dreamy      | `sine.inOut`     | Langzaam, symmetrisch        |

**Timing:** fast (0.2s) = energie · medium (0.4s) = professioneel · slow (0.6s) = luxe · cinematic (1–2s)

### Sub-compositie timelines — niet handmatig nesten

De framework nest sub-timelines automatisch op basis van `data-start`. Nooit handmatig toevoegen:

```javascript
// FOUT — niet doen:
masterTL.add(window.__timelines["scene1"], 0);

// GOED — elke compositie registreert alleen zijn eigen timeline:
window.__timelines["scene1-logo-intro"] = tl;
```

---

## Clipregels

| Element            | `class="clip"` | `data-duration` |
|--------------------|----------------|-----------------|
| `<div>`, `<img>`   | Verplicht      | Verplicht       |
| `<video>`          | Nooit          | Optioneel       |
| `<audio>`          | Nooit          | Optioneel       |
| Geneste compositie | —              | Nooit           |

---

## Veelgemaakte fouten

**1. Compositie te kort (afknippen)**
Timeline stopt na laatste animatie. Fix: `tl.set({}, {}, DURATION)` aan het einde.

**2. `window.__timelines` sleutel klopt niet**
Sleutel moet exact overeenkomen met `data-composition-id`. Animaties spelen niet als ze niet overeenkomen.

**3. `class="clip"` vergeten**
Elementen zonder `class="clip"` negeren `data-start` en `data-duration` — ze zijn altijd zichtbaar.

**4. Media aansturen in scripts**
Nooit `video.play()`, `video.pause()` of `audio.currentTime` in scripts. Het framework doet dit.

**5. GSAP animaties op `<video>` afmetingen**
Animeer nooit `width`/`height`/`top`/`left` direct op `<video>`. Wrap in een `<div>` en animeer de wrapper.

**6. Overmatig grote afbeeldingen (Figma-exports!)**
Figma exporteert soms op 2x of hoger. Chrome decodeert afbeeldingen tot RGBA-bitmaps: een 7000×5000px export = 140MB in geheugen. **Sla altijd op op maximaal 2× de canvasgrootte** (3840×2160 voor een 1080p compositie).

```bash
# Resize Figma-exports naar max 3840px breed (behoudt aspect ratio)
mogrify -path assets/ -resize 3840x3840\> assets/*.png
```

**7. `Math.random()` gebruiken**
Levert bij elke render andere frames. Gebruik een seeded PRNG als randomness nodig is.

**8. `async`/`await` in timeline setup**
Timeline constructie moet synchroon zijn.

---

## Assets — Figma-exports en SVG

### Figma PNG/WebP als `<img>` clip

```html
<img id="screen-1" class="clip"
     data-start="0" data-duration="6" data-track-index="1"
     src="../assets/figma-cursors.svg"
     style="position:absolute; width:1920px; height:1080px;" />
```

### Inline SVG voor animatie van losse elementen

Plak SVG-inhoud direct in de template om losse paden of groepen te animeren:

```html
<div id="svg-wrap" class="clip"
     data-start="0" data-duration="5" data-track-index="1"
     style="position:absolute; width:1920px; height:1080px;">
  <!-- SVG inline geplakt — groepen en paden zijn direct aanstuurbaar -->
  <svg viewBox="0 0 1920 1080">
    <g id="bar-1">...</g>
    <g id="bar-2">...</g>
  </svg>
</div>

<script>
  tl.from("#bar-1", { scaleY: 0, transformOrigin: "bottom", duration: 0.6, ease: "expo.out" }, 0.3);
  tl.from("#bar-2", { scaleY: 0, transformOrigin: "bottom", duration: 0.6, ease: "expo.out" }, 0.5);
</script>
```

---

## Stijl

Energieke SaaS product video — snel, flashy, donker.

| Rol           | Hex       |
|---------------|-----------|
| Achtergrond   | `#000f47` |
| Electric blue | `#ceecff` |

**Typografie:** Noto Sans, 700–900 weight via Google Fonts.

**Transitions tussen scenes:** altijd in Electric blue — jump cuts zijn vrijwel nooit bedoeld.

---

## Relevante blocks

```bash
npx hyperframes add logo-outro          # Cinematic logo reveal, 6s
npx hyperframes add shimmer-sweep       # Licht-sweep over tekst
npx hyperframes add flash-through-white # Transition: white flash
npx hyperframes add glitch              # Transition: glitch artifacts
npx hyperframes add grain-overlay       # Film grain texture
npx hyperframes add grid-pixelate-wipe  # Transition: grid dissolve
```

Embedden in `index.html`:

```html
<div id="trans-1"
     data-composition-id="flash-through-white"
     data-composition-src="compositions/flash-through-white.html"
     data-start="scene1 - 0.2"
     data-track-index="2"></div>
```

---

## CLI

```bash
npx hyperframes init my-video           # project aanmaken + skills installeren
npx hyperframes preview                 # live preview in browser (hot reload)
npx hyperframes lint                    # structuur controleren
npx hyperframes validate                # runtime errors, missing assets, contrast
npx hyperframes compositions            # lijst composities + opgeloste duur
npx hyperframes render --output v1.mp4  # renderen naar MP4
```

**Debugging volgorde:**
1. `npx hyperframes lint` — structurele fouten
2. `npx hyperframes validate` — runtime errors, ontbrekende assets
3. Klopt `window.__timelines["<id>"]` met `data-composition-id`?
4. Is de timeline lang genoeg? (`tl.set({}, {}, N)`)
5. Browser console: runtime errors staan als `[Browser:ERROR]`

---

## Promptlog — PROMPTS.md

Na elke compositie die Claude aanmaakt of aanpast, voegt het een entry toe aan `PROMPTS.md` in de root. Dit is het logboek van alle prompts en iteraties.

### Formaat

```markdown
## [datum] — [auteur] — [bestandsnaam]

**Prompt:**
> [de exacte prompt die gebruikt is]

**Bestand:** `compositions/scene1-logo-intro.html`
**Assets:** `assets/figma-logo-pieces.svg`
**Iteratie:** v1

**Notities:**
[wat werkte, wat niet, volgende stap]

---
```

### Voorbeeld `PROMPTS.md`

```markdown
# Promptlog

## 2026-06-15 — Lisa — scene1-logo-intro.html

**Prompt:**
> Using `/hyperframes`, animate assets/figma-logo-pieces.svg as a logo intro.
> Each piece flies in with expo.out and assembles over 1.2s. Dark background #080B14.
> Output: compositions/scene1-logo-intro.html

**Bestand:** `compositions/scene1-logo-intro.html`
**Assets:** `assets/figma-logo-pieces.svg`
**Iteratie:** v1

**Notities:**
Werkt goed. Wil nog een glow bloom na assembly — oppakken in v2.

---

## 2026-06-15 — Marc — scene1-logo-intro.html

**Prompt:**
> Add a neon blue glow bloom on the assembled logo after 1.2s. Duration 0.4s.

**Bestand:** `compositions/scene1-logo-intro.html`
**Assets:** —
**Iteratie:** v2

**Notities:**
Glow toegevoegd via GSAP textShadow. Klaar.

---
```

---

## Claude-instructies

- Communiceer in het Nederlands
- Lees `SCENES.md` voordat je een compositie schrijft — dit is de creative brief
- Werk de status in `SCENES.md` bij na elke compositie: ⬜ → 🔄 bij start, 🔄 → 👀 als het klaar is voor review
- Gebruik altijd `/hyperframes` slash command in Claude Code; zonder dit command gokt het model naar HTML-video conventies
- Elke scene → eigen bestand in `compositions/` met `<template>` wrapper
- Vermeld assetpaden expliciet in prompts (`assets/figma-cursors.svg`) — niet aannemen dat Claude ze kent
- Houd je aan de stijlgids
- Maak nooit assets zelf aan — gebruik wat in `assets/` staat
- Elke compositie krijgt een entrance-animatie — elementen die zomaar verschijnen voelen kapot op video
- Na elke compositie die aangemaakt of aangepast wordt: **voeg een entry toe aan `PROMPTS.md`** met de gebruikte prompt, bestandsnaam, assets en iteratienummer. Dit is verplicht.
- Maak een nieuwe versie (`scene2b.html`) in plaats van originelen te overschrijven
- Vraag verduidelijking voordat je bestanden van de ander aanpast
