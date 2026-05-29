# PRD — Lentor Gardens Residences Landing Page

**Status:** In progress (v1.0)
**Owners:** Marketing — TBD (ERA Realty)
**Last reviewed:** April 2026

---

## 1. Summary

A single-page marketing site for **Lentor Gardens Residences**, a 99-year leasehold residential development at Lentor Garden, District 26 (Upper Thomson / Mandai), Singapore, developed by **Kingsford Development**. The site exists to capture qualified buyer enquiries and route them to the developer-appointed marketing agent.

This is not a brochure. It is the digital first impression — and for many buyers, the only impression before they decide whether to request a showflat appointment.

### Project at a glance

| Field | Detail |
|---|---|
| Project name | Lentor Gardens Residences |
| Developer | Kingsford Development (Kingsford Lentor Project Pte Ltd) |
| Address | Lentor Garden, District 26 |
| Planning area | Mandai / Upper Thomson |
| Tenure | 99-year leasehold |
| Site area | ~20,639 sqm (~222,161 sqft) |
| Total units | 499 residential units |
| Building config | 4 blocks — 3 × 16-storey, 1 × 8-storey |
| Retail | Ground-floor retail shops + integrated childcare |
| Nearest MRT | Lentor (TE5, Thomson–East Coast Line) |
| Estimated TOP | Q4 2029 |

---

## 2. Audience

### Primary
**HDB upgraders and young families in the North**, ages 28–50, looking for a first or second private property in an established residential corridor. They have shortlisted 2–4 new launches in the D26/D20 corridor and are comparing connectivity, school proximity, and psf value.

What they want to know in 60 seconds:
1. Where is it (district, street, MRT proximity)?
2. Tenure (99-year vs freehold) and what that means for price?
3. Who built it and what is their track record?
4. What does it look like and what layouts are available?
5. What does a typical unit cost?

### Secondary
**Investors and upgraders from the Ang Mo Kio / Bishan / Thomson belt** looking for a rental-yield play close to Lentor MRT and within the TE line catchment.

**Overseas Singaporeans / regional investors** browsing on mobile, often via WhatsApp link. Decision-making lag is longer; they need to feel the product is serious enough to justify a viewing trip.

---

## 3. Goals & Success Criteria

### Primary goal
**Capture qualified buyer enquiries** with sufficient context to enable a same-day callback or showflat appointment booking.

### Success metrics

| Metric | Target | How measured |
|---|---|---|
| Form submission rate (visitors → submitted enquiries) | ≥ 4% | Form analytics |
| Form completion rate (form-starts → submits) | ≥ 60% | Form analytics |
| Mobile-first session share | Track only — expect 60–75% | Web analytics |
| Time on page (median) | ≥ 90 seconds | Web analytics |
| Bounce rate | ≤ 55% | Web analytics |
| Lighthouse Performance (mobile) | ≥ 85 | Lighthouse CI |
| Lighthouse Accessibility | ≥ 95 | Lighthouse CI |

### What we are explicitly **not** optimising for
- Search engine ranking for broad terms ("Singapore condo," etc.) — this is a one-off marketing page, not a content portal.
- Animation/interactivity for its own sake.
- Selling the unit on the page — the goal is the showflat appointment, not the sale.

---

## 4. Scope (v1.0 — current)

### In scope

- **Hero** — editorial split layout, three-image carousel, headline + lede + dual CTA, project specs strip
- **Overview** — full project narrative, 4-stat strip (499 units, 4 blocks, Lentor MRT, 2029 TOP)
- **Gallery** — three asymmetric "plates" with captions
- **Residences** — unit mix table (2BR, 3BR, 4BR, 5BR Strata Terrace) with indicative sizing and pricing
- **Location** — aerial site plan, three-column proximity table (Transit / Schools / Lifestyle)
- **Developer** — Kingsford Development card with logo and track record meta
- **Enquiry form** — name, mobile, email, typology preference, message, DNC consent
- **Legal modals** — Disclaimer and Privacy Policy as full-text scrollable overlays
- **Footer** — brand block, navigation, contact, legal links

### Out of scope for v1.0

- Floor plan downloads / e-brochure delivery (planned v1.1)
- Interactive site plan with hotspot units
- Virtual tour / 360° showflat
- Multi-language (English-only)
- Live availability board ("X units left")
- Mortgage / TDSR calculator
- Agent attribution beyond the assigned ERA Realty agent

---

## 5. Functional Requirements

### FR-1: Hero must communicate the five key facts within first scroll

The hero must convey, without scrolling on a 13" laptop or a typical iPhone viewport:
- Project name (Lentor Gardens Residences)
- Address (Lentor Garden, District 26)
- Tenure (99-year leasehold)
- Typology range (2–5 BR, 499 residences)
- A primary CTA ("Book a Showflat Visit")

### FR-2: Image carousel
- 3 images, auto-advancing every 6.5 seconds
- Pauses on hover and when tab is hidden
- Keyboard, click, and swipe support
- Slide indicator + slide number ("01 / 03") visible at all times
- Respects `prefers-reduced-motion` (no auto-advance, no Ken Burns drift)

### FR-3: Enquiry form
- Required: full name, mobile, email, DNC consent
- Optional: typology preference, message
- Inline validation on blur
- Submit button disabled state when invalid
- Successful submission shows toast ("Thank you. Our team will be in touch shortly.") and resets form
- Form data must be capturable — production deployment must wire to a backend endpoint or mailto fallback

### FR-4: Legal modals
- Disclaimer and Privacy Policy must be accessible from the footer at all times
- Modals open via overlay; close via close button, ESC key, or clicking the backdrop
- Body content is scrollable independently of the page
- Focus is moved to the close button on open and restored to the trigger on close

### FR-5: Mobile responsiveness
- Layout reflows cleanly between 320px and 1920px
- All tap targets ≥ 44×44px
- Hero image moves below the headline at <860px
- Unit table reflows from multi-column to stacked 2-column at <780px
- Navigation collapses (centre links hidden) at <880px

### FR-6: Performance
- Total page weight < 1.5MB including all images, fonts, and HTML
- Largest Contentful Paint (LCP) < 2.5s on a Moto G4 / 4G connection
- No render-blocking JS
- Fonts loaded from Google Fonts via `<link>` (optimise to self-hosted in v1.1 if performance budget is tight)

---

## 6. Content Requirements

### Unit mix

| Type | Size | Notes |
|---|---|---|
| 2-Bedroom | 646 – 732 sqft | — |
| 3-Bedroom | 872 – 1,012 sqft | — |
| 4-Bedroom | 1,184 – 1,356 sqft | — |
| 5-Bedroom Strata Terrace | 1,496 sqft | Limited units |
| Retail | 463 – 474 sqft | Ground-floor, not for residential sale |

All pricing indicative; show "From $X" where available, otherwise "POA."

### Location proximity table

**Transit**
- Lentor MRT (TE5) — ~5 min walk
- Springleaf MRT (TE4) — ~1 stop
- Mayflower MRT (TE6) — ~1 stop
- Bright Hill MRT (TE7/CR13) — ~2 stops (future interchange)
- CTE / SLE expressway access — direct

**Schools (within 1–2 km)**
- Anderson Primary School
- Mayflower Primary School
- Ang Mo Kio Primary School
- CHIJ St. Nicholas Girls' School (within 1 km)
- Presbyterian High School
- Yio Chu Kang Secondary School
- Nanyang Polytechnic

**Lifestyle & amenities**
- Lentor Modern Integrated Mall — adjacent
- Thomson Plaza — ~10 min drive
- AMK Hub — ~10 min drive
- Lentor Hillock Park — adjacent
- Thomson Nature Park — nearby
- Lower Peirce Reservoir Park — nearby
- Central Catchment Nature Reserve — nearby
- Orchard Road / CBD — ~15 min drive

### Copy tone
Grounded, considered, nature-adjacent. The project sits beside a hillock park and is positioned as a calm, well-connected retreat from the city. Lean into greenery, community, and long-term family value. Do not overpromise on exclusivity — 499 units is a mid-scale development. Avoid generic launch hyperbole.

Examples:
- ✅ "Where the treetops begin and the city remains within reach."
- ✅ "A considered address in Singapore's most quietly coveted corridor."
- ✅ "Four blocks, one neighbourhood, one nature park at the door."
- ❌ "Don't miss out on this once-in-a-lifetime opportunity!"
- ❌ "Hottest new launch in D26!"

### Mandatory legal / content elements
- Marketing agent attribution: name, CEA registration, agency name, agency licence number
- "Artist's Impression" caption on all rendered imagery
- Disclaimer modal accessible at all times
- Privacy Policy modal accessible at all times
- DNC consent checkbox on enquiry form

---

## 7. Non-Functional Requirements

### Brand & visual
- Nature-meets-urban aesthetic — greens, warm off-whites, deep charcoals
- Accent colour: TBD (suggest muted sage green or warm earth tone to echo the "gardens" branding)
- No gold, no glass-morphism, no purple gradients

### Accessibility (WCAG 2.1 AA target)
- Colour contrast ≥ 4.5:1 for body text, 3:1 for large text
- Keyboard navigable end-to-end
- ARIA roles for carousel, modals, form errors
- Focus visible on all interactive elements
- No motion-induced disorientation (`prefers-reduced-motion` honoured)

### Compliance
- DNC consent checkbox is mandatory before submit (PDPA)
- Privacy policy and disclaimer must be one click away
- Marketing agent attribution shown in footer and disclaimer
- Pricing labelled "indicative" with "Artist's Impression" on all renders

### Browser support
- Last 2 versions of Chrome, Safari, Firefox, Edge
- iOS Safari 15+
- Android Chrome on Android 10+

---

## 8. Technical Requirements

- Single static HTML file (`lentor-garden.html`)
- All assets in a sibling `assets/` directory
- No build step, no bundler
- No backend dependency in the file itself
- Deployable to any static host (Vercel, Netlify, Cloudflare Pages, S3+CDN)
- Form submission must be wired to a real handler before production launch

---

## 9. Risks & Open Questions

| # | Risk / question | Mitigation |
|---|---|---|
| R-1 | Form posts nowhere — no backend wired yet | Must integrate with a CRM / email handler before launch |
| R-2 | Pricing not yet publicly released | Label all pricing "indicative — from $X" or "POA"; update when official price list drops |
| R-3 | Imagery is artist's impression; legal exposure if buyers expect identical reality | "Artist's Impression" caption is mandatory on all renders; reinforced in disclaimer copy |
| R-4 | TOP estimated Q4 2029 — may shift | Label as "Est. 2029" and avoid using "guaranteed" language |
| R-5 | Marketing agent attribution not yet confirmed | Placeholder in footer; must be filled before any public link is shared |
| R-6 | DNC compliance language may need legal review | Form copy mirrors industry standard; recommend PDPA-aware legal review before launch |
| R-7 | Kingsford track record less prominent than UOL/SingLand — buyers may be unfamiliar | Include a developer section with completed project names and tenure in Singapore |

---

## 10. Out of scope (parking lot for v1.1+)

- Floor-plan PDF download via email gate
- Interactive site plan with unit availability
- Mortgage / TDSR calculator
- Multi-language (Mandarin, Bahasa)
- Backend submission with email + CRM webhook
- Self-hosted fonts
- Optimised hero image variants (srcset + AVIF)
- A/B testing of CTA copy
- Virtual showflat / 360° tour
