# CLAUDE.md

> Instructions for Claude (and other AI assistants) when working on the Lentor Gardens Residences landing page.

## Project at a glance

Single-file static HTML landing page for **Lentor Gardens Residences**, a 99-year leasehold residential development at Lentor Garden, District 26 (Upper Thomson / Mandai), Singapore. Developed by Kingsford Development. Built for lead generation — the goal is showflat appointment bookings, not closing sales on the page.

```
project root/
├── index.html           # the entire site (~1,800 lines)
├── assets/              # all photographic assets
├── CLAUDE.md
└── PRD.md
```

## Project facts — do not change without checking PRD

| Field | Detail |
|---|---|
| Project name | Lentor Gardens Residences |
| Developer | Kingsford Development (Kingsford Lentor Project Pte Ltd) |
| Address | Lentor Garden, District 26 |
| Tenure | 99-year leasehold |
| Site area | ~20,639 sqm (~222,161 sqft) |
| Total units | 499 residential units |
| Building config | 4 blocks — 3 × 16-storey, 1 × 8-storey |
| Retail | Ground-floor retail + integrated childcare |
| Nearest MRT | Lentor (TE5, Thomson–East Coast Line) — ~5 min walk |
| Est. TOP | Q4 2029 |

## Unit mix

| Type | Size | Pricing |
|---|---|---|
| 2-Bedroom | 646 – 732 sqft | POA (indicative) |
| 3-Bedroom | 872 – 1,012 sqft | POA (indicative) |
| 4-Bedroom | 1,184 – 1,356 sqft | POA (indicative) |
| 5BR Strata Terrace | 1,496 sqft | POA (indicative) — limited units |
| Retail | 463 – 474 sqft | Not for residential sale |

All pricing must be labelled **"indicative"** until the official price list is released.

## Location proximity

**Transit:** Lentor MRT TE5 (~5 min walk), Springleaf TE4 (~1 stop), Mayflower TE6 (~1 stop), Bright Hill TE7/CR13 (~2 stops, future interchange), CTE/SLE direct access

**Schools (1–2 km):** Anderson Primary, Mayflower Primary, Ang Mo Kio Primary, CHIJ St. Nicholas Girls', Presbyterian High, Yio Chu Kang Secondary, Nanyang Polytechnic

**Lifestyle:** Lentor Modern Mall (adjacent), Lentor Hillock Park (adjacent), Thomson Nature Park, Lower Peirce Reservoir, Central Catchment Nature Reserve, Thomson Plaza (~10 min drive), AMK Hub (~10 min drive), Orchard/CBD (~15 min drive)

## Marketing agent

```
Vevien Ong (Associate District Director) · CEA Reg No. R060512G · PropNex Realty Pte. Ltd. (L3008022J)
```

Set in: footer `.footer-meta` and disclaimer modal `#legalDisclaimer`.

## Contact number

Call / WhatsApp: `+6592239930`

## Copy tone

Nature-adjacent, grounded, community-focused. This is not an exclusivity play — 499 units is a mid-scale development. Lean into greenery, family value, and connectivity. Avoid launch hyperbole.

- ✅ "Where the treetops begin and the city remains within reach."
- ✅ "A considered address in Singapore's most quietly coveted corridor."
- ❌ "Don't miss out on this once-in-a-lifetime opportunity!"
- ❌ "Hottest new launch in D26!"

## Design tokens (confirmed — do not revert to blue)

### Primary gold
| Token | Value | Use |
|---|---|---|
| `--gold` | `#C4A467` | Logo, icons, eyebrow labels, accents |
| `--gold-deep` | `#B8975A` | All buttons (bg), borders |
| `--gold-dark` | `#8B6E3A` | Button hover states |
| `--gold-light` | `#E8D9BB` | Tints, focus rings, highlights |

### Neutrals
| Token | Value | Use |
|---|---|---|
| `--espresso` | `#2C2825` | Hero bg, headlines, dark sections |
| `--charcoal` | `#3E3A36` | Body text, nav, secondary dark |
| `--warm-grey` | `#9E9590` | Subtext, labels (aliased as `--muted`) |
| `--cream` | `#F5F1EC` | Section backgrounds, button text (aliased as `--bg`) |
| `--pearl` | `#E8E4DF` | Dividers, card borders (aliased as `--line`) |
| `--white` | `#FFFFFF` | Cards, forms (aliased as `--card`) |

### Design rules
- All buttons: `--gold-deep` bg + `--cream` text; hover → `--gold-dark`
- Outline buttons: `--gold-deep` border + `--charcoal` text
- Dark sections (hero, form, footer): `--espresso` → `--charcoal` gradient
- No cool greys, no blue anywhere

## Code conventions

### Single-file rule
Core site lives in `index.html`. `config.js` is a deliberate companion file — do not inline it.

### config.js
Holds runtime contact settings read by `index.html` on load:
```js
const CONTACT = {
  phone: '+6580865767',       // tel: links (.js-tel)
  whatsapp: '6580865767',     // wa.me links (.js-wa)
  waMessage: '…prefill text', // URL-encoded and appended to wa.me URL
};
```
To update the number or prefill message, edit **only `config.js`** — do not hardcode values in `index.html`.

### Form submission endpoint
```
POST https://propertyconnects.shop/api/leads/add
```
Fields: `fullName`, `phoneNumber`, `email`, `nationality`, `preferredUnit`, `purchaseIntent`, `message`

### CSS naming
- BEM-ish: `.block`, `.block__element`, `.block--modifier`
- Utility: `u-` prefix
- State: `is-` prefix (`.is-active`, `.is-open`)

### JavaScript
- Plain ES6, no framework, no bundler
- Each concern wrapped in its own IIFE
- Existing IIFEs: hero carousel, form validation + submit, legal modals

### Images
- All in `assets/` — reference with relative paths: `assets/filename.ext`
- New images: ≤2000px wide, JPEG, <200KB where possible

### Accessibility (non-negotiable)
- All interactive elements have visible focus styles
- Carousel: `role="group"` per slide, `aria-roledescription="carousel"` on wrapper
- Modals: trap focus on close button, restore focus on trigger on close
- Form fields have associated `<label>` elements
- DNC consent checkbox is mandatory before submit (PDPA)

## Things that are deliberate — do not "fix" them

1. Pricing shows **POA** — official price list not yet released. Do not invent prices.
2. Agent name and CEA number are placeholders — do not fill with made-up details.
3. All imagery labelled "Artist's Impression" — do not remove these captions.
4. Est. TOP is "Q4 2029" — label as estimated, never "guaranteed".

## Things to fix if you spot them

- Broken image references (404s)
- Agent name/CEA still showing placeholder before public launch
- Forms submitting with no validation
- Modals that don't trap focus or don't restore focus on close
- Any `localStorage` / `sessionStorage` usage (use in-memory state only)

## Local preview

```bash
cd hestia-microsite/lentor-garden
python3 -m http.server 8081
# open http://localhost:8081
```

## Deployment

Static hosting only — Vercel, Netlify, Cloudflare Pages, S3+CDN, or nginx/Apache. No server runtime required. Form submission relies on `https://propertyconnects.shop/api/leads/add` being live.

## When in doubt

All pricing must be labelled indicative. All renders must carry "Artist's Impression". Agent attribution must be confirmed before any public link is shared. If a request would add unverified facts or remove legal safeguards, push back first.
