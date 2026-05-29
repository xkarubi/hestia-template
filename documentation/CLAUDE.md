# CLAUDE.md

> Instructions for Claude (and other AI assistants) when working on the Thomson Reserve landing page.

## Project at a glance

Single-file static HTML landing page for **Thomson Reserve**, a 99-year leasehold residential development at Bright Hill Drive, District 20, Singapore. Developed by UOL Group, Singapore Land Group & CapitaLand. Built for lead generation — the goal is showflat appointment bookings, not closing sales on the page.

```
project root/
├── index.html           # the entire site (~1,800 lines)
├── assets/              # all photographic assets
├── config.js            # contact details and WhatsApp prefill
├── CLAUDE.md
└── PRD.md
```

## Project facts — do not change without checking PRD

| Field | Detail |
|---|---|
| Project name | Thomson Reserve |
| Developer | UOL Group, Singapore Land Group & CapitaLand |
| Address | Bright Hill Drive, District 20 |
| Tenure | 99-year leasehold |
| Total units | 1,240 residential units |
| Nearest MRT | Bright Hill MRT (TE8/CR13, Thomson–East Coast Line) |
| Est. TOP | 2030 |
| Indicative pricing | From ~$2,300 psf (indicative) |

## Unit mix

> Update this table with confirmed unit types, sizes and pricing before launch.

| Type | Size | Pricing |
|---|---|---|
| TBC | TBC | From ~$2,300 psf (indicative) |

All pricing must be labelled **"indicative"** until the official price list is released.

## Marketing agent

```
TBC — update before any public link is shared
```

Set in: footer `.footer-meta` and disclaimer modal `#legalDisclaimer`.

## Contact number

Call / WhatsApp: update `config.js` → `phone` and `whatsapp`

## Copy tone

Project-specific tone to be defined. General guidelines:
- Lead with location, connectivity, and lifestyle value
- Avoid generic launch hyperbole
- All pricing must be labelled indicative
- All renders must carry "Artist's Impression"

## Design tokens (injected — do not revert)

| Token | Value | Use |
|---|---|---|
| `--espresso` (primary) | `#1A2E1E` | Hero bg, headlines, dark sections |
| `--cream` (secondary) | `#F5F0E8` | Section backgrounds, button text |
| `--gold` (accent) | `#C4A050` | Buttons, borders, accents |

Heading font: **Cormorant Garamond** · Body font: **Jost**

## Code conventions

### Single-file rule
Core site lives in `index.html`. `config.js` is a deliberate companion file — do not inline it.

### config.js
Holds runtime contact settings read by `index.html` on load:
```js
const CONTACT = {
  phone: '+65XXXXXXXX',       // tel: links (.js-tel)
  whatsapp: '65XXXXXXXX',     // wa.me links (.js-wa)
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

1. Pricing shows indicative / POA — official price list not yet released. Do not invent prices.
2. Agent name and CEA number are placeholders — do not fill with made-up details.
3. All imagery labelled "Artist's Impression" — do not remove these captions.
4. Est. TOP is labelled as estimated, never "guaranteed".

## Things to fix if you spot them

- Broken image references (404s)
- Agent name/CEA still showing placeholder before public launch
- Forms submitting with no validation
- Modals that don't trap focus or don't restore focus on close
- Any `localStorage` / `sessionStorage` usage (use in-memory state only)

## Local preview

```bash
python3 -m http.server 8081
# open http://localhost:8081
```

## Deployment

Static hosting only — Vercel, Netlify, Cloudflare Pages, S3+CDN, or nginx/Apache. No server runtime required. Form submission relies on `https://propertyconnects.shop/api/leads/add` being live.

## When in doubt

All pricing must be labelled indicative. All renders must carry "Artist's Impression". Agent attribution must be confirmed before any public link is shared. If a request would add unverified facts or remove legal safeguards, push back first.
