# FASHION-REDESIGN  (GitHub-repo: oinkoink12/redesign)

> **Push nooit automatisch naar GitHub — wacht altijd op een expliciete opdracht van de gebruiker.**

## Wat is dit

Redesign-concept voor de **iBOOD Fashion-vertical**. Eén `index.html` toont
de **huidige iBOOD.com-look** als basis met een **toggle** (rechtsonder)
naar het **nieuwe design**, zodat oud en nieuw direct vergelijkbaar zijn op
dezelfde echte data. Zusterrepo's: [`firesale`](../firesale),
[`trapprijs`](../trapprijs) (prijsmechaniek; hier draait het om design/UX).

## Status (laatste stand)

- **iBOOD-homepage is het startpunt** (gedeeld door beide designs):
  `#view-home`/`#nv-home` met gele "Aanvul Alert!"-promobanner, vaste
  hero-deal ("Deal X|N", handmatige ‹/›, geen auto-rotatie) en
  categoriebanden. Router: `home` (geen body-class) →
  `v-vertical`/`v-brand`/`v-pdp` via `setView()`; `goHome()` (logo +
  niet-Fashion-nav + breadcrumb Home), `goVertical()` (nav Fashion +
  breadcrumb Fashion). **Auto-rotatie overal verwijderd** (homepage- én
  vertical-hero, beide designs).
- **Homepage = niet-Fashion deals** (`GEN` = `PRODUCTS` zonder Fashion);
  Fashion-vertical = `POOL` (Fashion) → andere producten/PDP's. Homepage
  "Bekijk alle deals" (promo + banden) → `openFlash()`: flash-detail/
  listing-view via `listItems()` (schakelt merk-filter ↔ flash-lijst),
  niet meer een PDP. Hero "Bekijk deal" → PDP van die deal.
- **Nieuw-design vertical-hero herbouwd**: tweekoloms-rij (tekst /
  sfeerbeeld `assets/sfeer-fashion.png`, fallback-gradient + placeholder)
  + gecentreerde deal-kaart eronder (uitlijning gefixt, geen overloop).
- Live op Vercel: redesign-delta-smoky.vercel.app (push `main` =
  auto-deploy).
- **Huidige-site-replica is af** in `index.html`, in de iBOOD-stijlgids
  (palet `--primary:#fc5628`, `--ink:#1e0033`, …) + **Stabil Grotesk**
  (`fonts/`). Werkende flow met view-router (`state.view`):
  - **Vertical (Fashion)**: topbar, header+nav, search, "Direct naar",
    hero-deal-carousel, "Waar vind je de beste Fashion aanbiedingen?",
    flashblokken **per merk** (lifestyle-tegel + kaarten + "Bekijk alle N
    deals"), nieuwsbrief, "Deze deals zijn alleen vandaag geldig",
    "Eerder bekeken", footer.
  - **Merk-detailpagina** (`openBrand`): breadcrumb, lifestyle-banner,
    toolbar (`N van de N producten` + Sorteren + Verberg/Toon filters),
    filter-sidebar (Merk functioneel/klikbaar; Categorie/Geslacht/Kleur/
    Maat/Voorraad als facet-look), responsive grid.
  - **PDP** (`openPDP`): galerij + thumbnails, dealbox (aftelklok/
    adviesprijs/`!`-prijs), Kleur/Geslacht/Maat-selects, CTA "Ik neem er
    1!", USP's, verzendblok, Praat mee/Hou ik van/Deel, Productinformatie
    + Specificaties, aanbevolen-rijen. Bereikbaar vanaf elke kaart + hero.
  - **Toggle** Huidige site ⇄ Nieuw design (`localStorage` `fr-mode`).
- **Nieuw design is af** in `#site-new` (eigen `nd-`-CSS, eigen
  `#nv-vertical/#nv-brand/#nv-pdp`, gedeelde `body.v-*`-routing + state +
  data + `openBrand/openPDP/goVertical`). Naar 3 mockups: luchtige
  vertical (donkere topbar, gecentreerde zoekbalk, peach hero met
  zwevende split deal-kaart + auto-rotatie, "Direct naar"-chips,
  lifestyle-tegels, per-merk-blokken), flashpage/merk-detail
  (peach-banner, in/uitklapbare filter-sidebar, sorteerbare 3-koloms
  grid, blauwe newsletter, "Eerder bekeken"), en PDP (gestapelde
  galerij + thumbs, prijsblok met `-X%`, klikbare maatknoppen,
  accordions). Teksten bewust NL i.p.v. de Engelse mockup-labels;
  hero/banner gebruiken productfoto's met tint-overlay (geen aparte
  lifestyle-assets in de dataset).
- `data.js` — ~98 producten hergebruikt uit de firesale-dataset
  (`window.PRODUCTS`); slechts 2 Fashion-merken (Lacoste, McGregor, 9
  items) → flow klopt, alleen dunner gevuld dan de echte site.
- De iBOOD **Performance/admin-strook** is bewust weggelaten (geen
  publieke pagina).
- Gecommit + gepusht: `main` → `origin` (`github.com/oinkoink12/redesign`).
  Vercel is nog **niet** gekoppeld (eenmalig importeren op vercel.com,
  zero-config, root = `/`).

## Volgende stap (de kern)

De **nieuw-design-kant** bouwen achter de bestaande toggle, op dezelfde
data en dezelfde flow (vertical → merk-detail → PDP). Input nodig van de
gebruiker: óf nieuw-design-mockups, óf akkoord dat Claude zelf een
redesign-voorstel maakt binnen de iBOOD-stijlgids.

## Werkwijze

- Statische site, **geen build-stap**. Lokaal: open `index.html`.
- `node` lokaal beschikbaar → inline JS valideren met `vm.Script` vóór
  commit (zie firesale/CLAUDE.md). De `data.js`-regel is groot (~49 KB).
- Bij grote screenshots: één per bericht, JPEG, < ~2 MB (base64-inflatie).
