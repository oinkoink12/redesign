# FASHION-REDESIGN  (GitHub-repo: oinkoink12/redesign)

> **Push nooit automatisch naar GitHub — wacht altijd op een expliciete opdracht van de gebruiker.**

## Wat is dit

Redesign-concept voor de **iBOOD Fashion-vertical**. Eén `index.html` toont
de **huidige iBOOD.com-look** als basis met een **toggle** (rechtsonder)
naar het **nieuwe design**, zodat oud en nieuw direct vergelijkbaar zijn op
dezelfde echte data. Zusterrepo's: [`firesale`](../firesale),
[`trapprijs`](../trapprijs) (prijsmechaniek; hier draait het om design/UX).

## Status (laatste stand)

- **Live**: https://redesign-delta-smoky.vercel.app/ (zero-config Vercel,
  push naar `main` = auto-deploy).
- **Beide designs af en volledig functioneel** op dezelfde data + dezelfde
  flow. Toggle rechtsonder wisselt huidige site ⇄ nieuw design
  (`localStorage` `fr-mode`).

### Routing & startpunt
- App opent op de **iBOOD-homepage** (gedeeld), niet direct op Fashion.
  Views: `home` (geen body-class) → `v-vertical` → `v-brand` → `v-pdp`,
  geschakeld via `setView(cls)`. Functies: `goHome()` (logo +
  niet-Fashion-nav + breadcrumb Home), `goVertical()` (nav Fashion +
  breadcrumb Fashion), `openBrand(b)` / `openFlash()` / `openPDP(id)`.
- IDs huidige replica: `#view-home/#view-vertical/#view-brand/#view-pdp`.
  IDs nieuw design: `#nv-home/#nv-vertical/#nv-brand/#nv-pdp`. CSS-routing
  toont in beide sites de juiste view via dezelfde body-class.
- **Geen auto-rotatie meer** ergens — alleen handmatige ‹/›-pijlen.

### Data-split (cruciaal)
- `POOL` = Fashion-producten (9, merken Lacoste/Mcgregor) — voedt de
  **Fashion-vertical**.
- `GEN` = `PRODUCTS.filter(p => p.category !== 'Fashion')` (~89, alle
  andere categorieën) — voedt de **homepage** (hero + banden + flash-
  listing vanaf homepage). Hierdoor leiden klikken vanaf de homepage
  altijd naar andere PDP's dan via de Fashion-vertical.

### Homepage (`#view-home` / `#nv-home`, gedeeld component)
- Renderer: `renderHome()` injecteert identieke HTML in beide containers
  (`hp-c` en `hp-n`). Bevat: gele **"Aanvul Alert!"**-promobanner, vaste
  hero-deal-kaart ("Deal X|N · Nog 7 uur", productbeeld + lichtblauwe
  **categorie-badge** linksonder zoals de "Gigabit"-badge in de mockup,
  brand + titel + USP-bullets + adviesprijs + `!`-prijs, **Bekijk deal**
  → `openPDP` + **Praat mee 2**, ‹/›-pijlen op de zijkanten van de hero),
  en categoriebanden voor de daadwerkelijk aanwezige categorieën.
- **"Bekijk alle deals"-knoppen** (promo + banden) → `openFlash()`:
  generaliseerde listing-view (zelfde markup als brand-detail) die `GEN`
  toont met label "Alle deals". Schakelt via `state.flashList` + helper
  `listItems()` (= `state.flashList ?? POOL.filter(brand)`).

### Nieuw-design vertical-hero (`.nd-hero`)
- **Full-bleed sfeerbeeld-achtergrond**: `assets/sfeer-fashion.png`
  (Lacoste-model, ~605 KB). Img absolute inset:0 over een gradient-
  placeholder met "SFEERBEELD"-tekst; bij errorload verdwijnt de img
  (`onerror="this.remove()"`) en zie je de placeholder. **Scrim**
  (`linear-gradient` 90deg) maakt links leesbaar voor titel/CTA.
- "Fashion" + "Lacoste maakt indruk deze week." + oranje **Bekijk alle
  deals** linksboven over de foto.
- **Brede deal-kaart** (`.nd-deal`, full wrap-width, `grid 42% / 1fr`)
  die over de onderkant van de hero valt (`margin:32px 0 -64px`).
  Links: timer-pill + productbeeld. Rechts: merk-chip + social-pills
  (Praat mee/Deel/Hou ik van) in dhead, titel, korte omschrijving,
  adviesprijs, prijs, **full-width oranje "Bekijk deal"-knop**, en een
  navy ronde `›`-pijl absoluut op de rechterrand (vertically centered).
- `.nd-chips{padding-top:84px}` om ruimte te geven onder de overlap.

### Huidige-site-replica (in dezelfde stijlgids `--primary:#fc5628`,
`--ink:#1e0033`, font Stabil Grotesk uit `fonts/`)
- **Vertical (Fashion)**: topbar, header+nav, search, "Direct naar",
  hero-deal, flashblokken per merk, nieuwsbrief, "Eerder bekeken",
  footer.
- **Merk-detail** (`openBrand`): breadcrumb, lifestyle-banner, toolbar
  (`N van de N producten` + Sorteren + Verberg/Toon filters), filter-
  sidebar (Merk klikbaar; rest cosmetisch), responsive grid.
- **PDP** (`openPDP`): galerij + thumbnails, dealbox (aftelklok +
  adviesprijs + `!`-prijs), Kleur/Geslacht/Maat-selects, CTA "Ik neem
  er 1!", USP's, verzendblok, social-rij, Productinfo + Specificaties,
  aanbevolen-rijen.

### Nieuw design (extra t.o.v. replica)
- Eigen `nd-`-CSS scoped onder `#site-new`. Zelfde state + data + entry-
  points (`openBrand`/`openPDP`/`goVertical`/`goHome`/`openFlash`).
- **Flashpage/merk-detail** (`renderNdBrand`): peach-banner met chip,
  filter-sidebar (in/uitklapbaar, "Alles wissen"), sorteerdropdown,
  3-koloms grid, blauwe newsletter, "Eerder bekeken"-rij. Sidebar-merk
  is functioneel/klikbaar (resetset `flashList=null`).
- **PDP** (`renderNdPDP`): gestapelde galerij + thumbnails, brand-caps,
  titel, omschrijving, rating, prijsblok met dynamisch `-X%`-badge,
  klikbare maatknoppen (S/M/L/XL/XXL), kleurstaal, voorraad, full-width
  **In winkelmandje**-CTA + hartje, USP's, accordions
  (Productinformatie open, Specs/Verzending/Reviews dicht), "Dit vind
  je misschien ook leuk"-rij.
- **Bewuste keuzes**: teksten NL (i.p.v. mockup-Engels), categorie-
  badge in homepage-hero i.p.v. losse alt-thumbnails (die zagen er
  rommelig uit op 64×64).

### Repo & assets
- `index.html` (één bestand, HTML+CSS+JS), `data.js` (~98 producten als
  `window.PRODUCTS`, hergebruikt uit firesale), `fonts/` (Stabil Grotesk
  woff/woff2), `assets/sfeer-fashion.png` (Lacoste-sfeerbeeld).
- Inline JS valideren vóór commit: `node -e "..."` met `vm.Script` op het
  laatste `<script>`-blok (zie firesale/CLAUDE.md voor het patroon).
- De iBOOD **Performance/admin-strook** is bewust weggelaten (geen
  publieke pagina).

## Volgende stap

Geen vaste open lijn meer — gebruiker stuurt feedback in tekst. Mogelijke
verfijningen die op tafel lagen: mockup-teksten naar Engels zetten,
flash-sidebar functioneel maken (filters echt laten filteren), extra
lifestyle-foto's per merk.

## Werkwijze

- Statische site, **geen build-stap**. Lokaal: open `index.html`.
- `node` lokaal beschikbaar → inline JS valideren met `vm.Script` vóór
  commit (zie firesale/CLAUDE.md). De `data.js`-regel is groot (~49 KB).
- Bij grote screenshots: één per bericht, JPEG, < ~2 MB (base64-inflatie).
