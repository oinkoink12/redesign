# FASHION-REDESIGN

> **Push nooit automatisch naar GitHub — wacht altijd op een expliciete opdracht van de gebruiker.**

## Wat is dit

Een **redesign-concept voor de iBOOD Fashion-vertical**. De pagina toont de
**huidige iBOOD.com-look als basis**, met een **toggle** die omschakelt
naar het **nieuwe design**. Zo zijn oud en nieuw direct vergelijkbaar op
dezelfde echte data.

Derde project naast de zusterrepo's [`firesale`](../firesale) en
[`trapprijs`](../trapprijs) — daar draait het om prijsmechaniek, hier om
**design/UX van de fashion-categorie**.

## Beslissingen (afgestemd met de gebruiker)

- **Basis-look**: de echte iBOOD.com nagemaakt (referentie = screenshots
  die de gebruiker aanlevert).
- **Nieuw design**: volgens mockups/inspiratie van de gebruiker
  (screenshots).
- **Data**: de ~100 producten uit de firesale-dataset (`PRODUCTS`,
  `../firesale/index.html`, ~49 KB op één regel) worden hergebruikt.
- **Toggle**: één `index.html`, zwevende schakelaar
  "Huidige site ⇄ Nieuw design", standaard = huidige site, keuze in
  `localStorage`. Zelfde patroon als de themaschakelaar in firesale.

## Structuur

Statische site, **geen build-stap** (zelfde aanpak als firesale):

- `index.html` — HTML + CSS + JS in één file (volgt zodra de screenshots
  binnen zijn).
- `fonts/` — Stabil Grotesk (woff2/woff, Regular/Medium/Bold/Black),
  gekopieerd uit firesale (iBOOD-styleguide-font).
- `CLAUDE.md`, `.gitignore`.

### Stijlgids-palet (uit firesale)

`--primary:#fc5628` · `--primary-dark:#e2461c` · inkt `#1e0033` ·
accentvarianten (#5ce567 / #6ea9e5) · lichte achtergrond. Font:
`"Stabil Grotesk", -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`.

## Status

Groundwork klaar (fonts, palet, dataset-bron, .gitignore). Wacht op
screenshots van (1) huidige iBOOD.com en (2) het nieuwe design om
`index.html` te bouwen. Nog **niets gecommit/gepusht**; GitHub-repo
`oinkoink12/fashion-redesign` (public) wordt pas aangemaakt op expliciet
akkoord.

## Werkwijze-aandachtspunten

- Lokaal bekijken: open `index.html` in de browser.
- Online via Vercel (zero-config, output = root).
- De `PRODUCTS`-regel is groot (~49 KB op één regel); regelgericht
  bewerken (zie firesale/CLAUDE.md).
- `node` lokaal beschikbaar — inline JS valideren met `vm.Script` vóór commit.
