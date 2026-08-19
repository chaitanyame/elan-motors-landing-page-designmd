# Élan Motors

> French-designed electric urban hatchbacks — landing page built from a DESIGN.md spec.

A single-file HTML landing page for the fictional **Élan Motors** brand: premium French electric city cars that blend Parisian design with modern EV engineering. The page is a static marketing mockup — three model cards, a technology stats band, a configurator preview panel, and call-to-action bands — written in French (`<html lang="fr">`) with an English hero tagline.

## Table of contents

- [Repository contents](#repository-contents)
- [Page sections](#page-sections)
- [The lineup](#the-lineup)
- [Design system](#design-system)
  - [Responsive breakpoints](#responsive-breakpoints)
- [Interactivity](#interactivity)
- [Getting started](#getting-started)
- [Image sourcing (`fetch_images.py`)](#image-sourcing-fetch_imagespy)
- [Structured data cheat-sheet](#structured-data-cheat-sheet)
- [Accessibility notes](#accessibility-notes)
- [License](#license)

## Repository contents

| File | Purpose |
|---|---|
| `index.html` | The entire landing page (673 lines: HTML + embedded CSS + a small inline script) |
| `fetch_images.py` | Stdlib-only helper that sources CC-licensed car photos from the Wikimedia Commons API (see below) |
| `README.md` | This file |

## Page sections

| Section | Anchor | Content |
|---|---|---|
| Top nav | — | Sticky white bar with the `ÉLAN MOTORS` wordmark, links (Modèles / Technologie / Configurateur / Store) shown ≥1024px, hamburger button ≤1024px |
| Mobile menu | — | Fixed full-screen overlay; toggled by the hamburger, auto-closes when a link is tapped |
| Hero | `#hero` | Full-bleed photo (Renault Mégane E-Tech) under a `rgba(0,0,0,.45)` overlay, H1 **ÉLAN ÉLECTRIQUE**, tagline *"French-designed electric urban hatchbacks. Distinctive by design, effortless by engineering."*, CTAs *Explorer les modèles* (yellow) and *Configurateur* (outline) |
| Models | `#models` | "La Gamme" — **TROIS VISIONS DE LA VILLE**: three vehicle cards, each with a photo, name, tagline and a *Découvrir →* link |
| Technology | `#technology` | Dark section "INGÉNIERIE FRANÇAISE" with a 5-cell stats grid |
| Promo tiles | — | Two full-width tiles: *Configurateur Élan* (white) and *Offre de Lancement* (yellow, "Jusqu'à 4 000 € d'économie") |
| Configurator | `#configurator` | "VOTRE ÉLAN, VOTRE STYLE" — photo on the left, a spec panel for **Élan Cité — Finition Atelier** on the right |
| Yellow CTA | — | "RÉSERVEZ VOTRE ESSAI" — 120 centres en France, *Prendre rendez-vous* button |
| Dark CTA | `#store` | "PRÊT POUR L'AVENIR?" — *Commander* button, delivery "sous 8 à 12 semaines" |
| Footer | — | 4 link columns (Modèles / Technologie / Entreprise / Support), "© 2026 Élan Motors. Tous droits réservés.", legal links (Vie Privée / Mentions Légales / Cookies) |

## The lineup

| Model | Badge | Tagline (verbatim from the page) |
|---|---|---|
| **Élan Cité** | `NOUVEAU` | "Urban agility meets French design. 320 km range, compact footprint." |
| **Élan Évasion** | — | "Extended range for weekend escapes. 450 km WLTP, fast-charge capable." |
| **Élan Sport** | — | "Performance redefined. Dual motor AWD, 0–100 km/h in 4.2 s." |

Technology stats band: **450 km** Autonomie WLTP · **170 kW** Puissance Moteur · **4.2 s** 0–100 km/h · **87 kWh** Batterie · **22 min** Recharge Rapide.

Configurator panel (Élan Cité — Finition Atelier): **Motorisation** 100 kW / 320 km · **Jantes** 18" Alliage Noir · **Couleur** four swatches (`#ffed00` selected, `#000000`, `#ffffff`, `#333333`) · **Intérieur** Tissu Gris Chiné.

## Design system

- **Typography:** Inter Tight (Google Fonts), weights 400 / 600 / 700; uppercase display headings; `lang="fr"`
- **Brand yellow:** `#ffed00` (hover `#e6d200`) on black — used for primary buttons, the NOUVEAU badge, the launch-offer tile, the CTA band, and the selected color swatch
- **Neutrals:** ink `#000000`, body `#222222`, muted `#666666`, hairline borders `#f2f2f2`, dark-section labels `#8a8a8a`, hero overlay `rgba(0,0,0,.45)`, light-on-dark text `rgba(255,255,255,0.72)`
- **Buttons:** 48px tall, 2px radius, uppercase, bold 14.4px/0.144px tracking; primary (yellow), outline-light, outline-dark
- **Radii:** cards and promo tiles are sharp-cornered (`border-radius: 0`); only the badge (46px) and color dots (9999px) are rounded
- **Layout:** max-width 1280px container; CSS Grid (vehicles 1→2→3 cols, specs 1→3→5, configurator 3fr/2fr, footer 1→2→3→4) and Flexbox

### Responsive breakpoints

| Breakpoint | Change |
|---|---|
| 480px | Specs grid 1 → 3 columns |
| 640px | Footer grid 1 → 2 columns |
| 768px | Vehicle grid 1 → 2, promo grid 1 → 2, specs 3 → 5, footer 2 → 3; container padding 24 → 48px; hero title 56 → 40px; section titles 40 → 32px |
| 1024px | Nav links appear, hamburger hides; vehicle grid 2 → 3; configurator 3fr/2fr; footer 3 → 4; container padding 48 → 80px |
| ≤767px | Section padding 80 → 40px, hero title 40px |

## Interactivity

Honest note: this is a **static marketing mockup**, not a web app. The only wired JavaScript is the hamburger toggle and the mobile menu's auto-close on link tap. Everything else — nav links, card *Découvrir →* links, promo tiles, the *Configurer complet* / *Commander* / *Prendre rendez-vous* buttons, and the configurator color dots (which are `cursor:pointer` spans with no click handler) — is decorative `href="#"`. Anchors do work: `html{scroll-behavior:smooth}` and the nav links point to real `#models`, `#technology`, `#configurator`, `#store` sections.

## Getting started

The page loads the Inter Tight font from Google Fonts and all photos from Wikimedia Commons, so it needs network access. Serve the repo directory:

```bash
git clone https://github.com/chaitanyame/elan-motors-landing-page-designmd.git
cd elan-motors-landing-page-designmd

# Serve it (any static server works)
python3 -m http.server 8080
# → open http://localhost:8080
```

Opening `index.html` directly via `file://` also renders — the Google Fonts request just falls back to system sans-serif when offline.

## Image sourcing (`fetch_images.py`)

`index.html` references five hardcoded Wikimedia Commons photos (960px thumbs): a 2021 Renault Mégane E-Tech (hero), a Renault Zoe facelift (Cité), a Renault 5 E-Tech 2024 (Évasion), a 2022 Renault Mégane E-Tech (Sport), and a Renault Scenic E-Tech 2024 (configurator).

`fetch_images.py` is a **sourcing helper** for future revisions — it searches the Commons API for CC-licensed alternatives and prints ready-to-paste URLs:

```bash
python3 fetch_images.py
```

- Stdlib only (`json`, `urllib`), no dependencies
- 5 queries: `"electric car france"`, `"renault electric vehicle"`, `"electric hatchback"`, `"french electric car"`, `"urban electric vehicle"`
- Searches the `File:` namespace (`srnamespace=6`), 5 results per query, 800px thumbnails (`iiurlwidth=800`), `ElanMotors/1.0` User-Agent
- Output ends with a `--- Image URLs (for HTML) ---` block of direct `https://` thumb URLs

## Structured data cheat-sheet

The marketing facts on the page live only as HTML markup, so they aren't easy to reuse elsewhere. This cheat-sheet mirrors the same data in machine-readable JSON for maintainers, tests, or future automation (e.g. regenerating the configurator panel or powering a `/api` stub):

```json
{
  "brand": "Élan Motors",
  "lineup": [
    { "model": "Élan Cité",     "badge": "NOUVEAU", "range_km": 320, "tagline": "Urban agility meets French design. 320 km range, compact footprint." },
    { "model": "Élan Évasion",  "badge": null,      "range_km": 450, "tagline": "Extended range for weekend escapes. 450 km WLTP, fast-charge capable." },
    { "model": "Élan Sport",    "badge": null,      "range_km": null, "tagline": "Performance redefined. Dual motor AWD, 0–100 km/h in 4.2 s." }
  ],
  "tech_stats": { "autonomie_wltp": "450 km", "puissance_moteur": "170 kW", "acceleration_0_100_s": "4.2 s", "batterie": "87 kWh", "recharge_rapide": "22 min" },
  "configurator": {
    "vehicle": "Élan Cité — Finition Atelier",
    "motorisation": "100 kW / 320 km",
    "couleurs": ["#ffed00", "#000000", "#ffffff", "#333333"],
    "selected_color": "#ffed00"
  }
}
```

Keep this block in sync with `index.html` whenever you change a figure in the markup — it's the single source truth for any script that reads the page.

## Accessibility notes

The page has solid foundations and a few easy wins if you plan to reuse it:

- **Already good:** semantic landmarks (`<nav>`, `<section>`, `<footer>`), descriptive image `alt` text, `loading="lazy"` on below-fold images, `aria-label`-able buttons, and a clear visual focus state (hover/active color shifts).
- **Worth adding:** the hamburger button and mobile-menu links have no `aria-expanded` / `aria-controls` wiring, and the menu is a `div` rather than a native `<dialog>` or `<ul role="menu">`; the color-swatch dots are `cursor:pointer` `<span>`s with no `role="button"` or keyboard behaviour.
- The brand yellow `#ffed00` on black passes WCAG AA for normal text; the muted `#8a8a8a` labels on the dark section are borderline for small text — consider `#a0a0a0` or bumping weight there.

## License

No LICENSE file is included, and the page footer asserts **"© 2026 Élan Motors. Tous droits réservés."** — treat the design as proprietary to its author. There are no CI workflows or license files, so no badges are shown. The featured car photos remain property of their respective rights holders via Wikimedia Commons.
