# PRD — {{PROJECT_NAME}} Landing Page

**Status:** Draft — update before launch
**Developer:** {{DEVELOPER}}
**Last reviewed:** — update with actual date

---

## 1. Summary

A single-page marketing site for **{{PROJECT_NAME}}**, a {{TENURE}} residential development at {{ADDRESS}}, {{DISTRICT}}, Singapore, developed by **{{DEVELOPER}}**. The site exists to capture qualified buyer enquiries and route them to the developer-appointed marketing agent.

This is not a brochure. It is the digital first impression — and for many buyers, the only impression before they decide whether to request a showflat appointment.

### Project at a glance

| Field | Detail |
|---|---|
| Project name | {{PROJECT_NAME}} |
| Developer | {{DEVELOPER}} |
| Address | {{ADDRESS}}, {{DISTRICT}} |
| Tenure | {{TENURE}} |
| Total units | {{UNIT_COUNT}} residential units |
| Nearest MRT | {{NEAREST_MRT}} |
| Estimated TOP | {{EST_TOP}} |
| Indicative pricing | {{PRICE_FROM}} |

---

## 2. Audience

### Primary
> Update with project-specific buyer profile before launch.

Likely HDB upgraders and families looking for a private property in {{DISTRICT}}. They are comparing connectivity, school proximity, and PSF value across 2–4 new launches.

What they want to know in 60 seconds:
1. Where is it (district, street, MRT proximity)?
2. Tenure ({{TENURE}}) and what that means for price?
3. Who built it ({{DEVELOPER}}) and what is their track record?
4. What does it look like and what layouts are available?
5. What does a typical unit cost ({{PRICE_FROM}})?

### Secondary
> Update with project-specific secondary audience before launch.

Investors and upgraders in the surrounding district looking for rental yield plays near {{NEAREST_MRT}}.

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

---

## 4. Scope (v1.0)

### In scope

- **Hero** — editorial split layout, three-image carousel, headline + lede + dual CTA
- **Highlights** — 3-card project overview (scale, schools, MRT)
- **Floor plans** — unit mix table with indicative sizing and pricing
- **Lifestyle** — nature and amenities section
- **Location** — aerial site plan, proximity table (Transit / Schools / Lifestyle)
- **Developer** — {{DEVELOPER}} card with logo and track record
- **Enquiry form** — name, mobile, email, typology preference, message, DNC consent
- **Legal modals** — Disclaimer and Privacy Policy as full-text scrollable overlays
- **Footer** — brand block, navigation, contact, legal links

### Out of scope for v1.0

- Floor plan downloads / e-brochure delivery
- Interactive site plan with hotspot units
- Virtual tour / 360° showflat
- Multi-language (English-only)
- Live availability board
- Mortgage / TDSR calculator

---

## 5. Functional Requirements

### FR-1: Hero must communicate five key facts within first scroll
- Project name ({{PROJECT_NAME}})
- Address ({{ADDRESS}}, {{DISTRICT}})
- Tenure ({{TENURE}})
- Unit count ({{UNIT_COUNT}} residences)
- A primary CTA ("Book a Showflat Visit")

### FR-2: Image carousel
- 3 images, auto-advancing every 6.5 seconds
- Pauses on hover and when tab is hidden
- Keyboard, click, and swipe support
- Respects `prefers-reduced-motion`

### FR-3: Enquiry form
- Required: full name, mobile, email, DNC consent
- Optional: typology preference, message
- Inline validation on blur
- Successful submission shows toast and resets form

### FR-4: Legal modals
- Disclaimer and Privacy Policy accessible from footer at all times
- Close via button, ESC key, or backdrop click
- Focus trapped and restored correctly

### FR-5: Mobile responsiveness
- Layout reflows cleanly between 320px and 1920px
- All tap targets ≥ 44×44px

### FR-6: Performance
- Total page weight < 1.5MB
- LCP < 2.5s on 4G
- No render-blocking JS

---

## 6. Content Requirements

### Unit mix
> Replace with confirmed unit types, sizes and pricing from developer.

| Type | Size | Notes |
|---|---|---|
| TBC | TBC | — |

All pricing indicative; show "From $X" where available, otherwise "POA."

### Location proximity
> Update with project-specific MRT, school, and lifestyle data.

**Transit**
- {{NEAREST_MRT}} — nearest MRT

**Schools** — update with schools within 1–2 km

**Lifestyle & amenities** — update with nearby malls, parks, and amenities

### Copy tone
> Update with project-specific tone guidelines.

Lead with location, connectivity, and lifestyle. Avoid launch hyperbole.
- All pricing must be labelled indicative
- All renders must carry "Artist's Impression"

---

## 7. Non-Functional Requirements

### Brand & visual
- Primary colour: `{{PRIMARY_COLOR}}`
- Secondary colour: `{{SECONDARY_COLOR}}`
- Accent colour: `{{ACCENT_COLOR}}`
- Heading font: {{FONT_HEADING}} · Body font: {{FONT_BODY}}

### Accessibility (WCAG 2.1 AA target)
- Colour contrast ≥ 4.5:1 for body text, 3:1 for large text
- Keyboard navigable end-to-end
- ARIA roles for carousel, modals, form errors
- `prefers-reduced-motion` honoured

### Compliance
- DNC consent checkbox mandatory before submit (PDPA)
- Privacy policy and disclaimer one click away
- Marketing agent attribution in footer and disclaimer
- Pricing labelled "indicative" with "Artist's Impression" on all renders

---

## 8. Technical Requirements

- Single static HTML file (`index.html`)
- All assets in `assets/` directory
- No build step, no bundler
- Deployable to any static host (Vercel, Netlify, Cloudflare Pages, S3+CDN)
- Form submission wired to handler before production launch
- Project URL: {{PROJECT_URL}}

---

## 9. Risks & Open Questions

| # | Risk / question | Mitigation |
|---|---|---|
| R-1 | Form posts nowhere — no backend wired yet | Must integrate with CRM / email handler before launch |
| R-2 | Pricing not yet publicly released | Label all pricing "indicative — {{PRICE_FROM}}" or "POA" |
| R-3 | Imagery is artist's impression | "Artist's Impression" caption mandatory on all renders |
| R-4 | TOP estimated {{EST_TOP}} — may shift | Label as "Est. {{EST_TOP}}" — never "guaranteed" |
| R-5 | Marketing agent attribution not yet confirmed | Placeholder in footer — must be filled before public launch |
| R-6 | DNC compliance language may need legal review | Recommend PDPA-aware legal review before launch |

---

## 10. Out of scope (parking lot for v1.1+)

- Floor-plan PDF download via email gate
- Interactive site plan with unit availability
- Mortgage / TDSR calculator
- Multi-language (Mandarin, Bahasa)
- Backend submission with email + CRM webhook
- Self-hosted fonts
- Virtual showflat / 360° tour
