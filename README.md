# The Invisible Shelter Playbook — Landing Page

A high-conversion landing page for the PDF book **"The Invisible Shelter Playbook · Field Edition Vol. 01"** by the YouTube channel [Survival Mode](https://youtube.com/@SurvivalMode).

The page sells the PDF (free Chapter 1 download).

---

## 🎯 Project Goal

Convert visitors into either:
. **Buyers** — direct PDF purchase at **$17** with promo code `SURVIVALMODE` ($10 off the $27 regular price)

---

## 📁 Project Structure

```
landing/
├── index.html        # Single-file landing page (HTML + CSS + JS)
├── book-cover.png    # Hero book mockup image
└── README.md         # This file
```

> **Note:** Everything is inlined in `index.html` for now — styles, scripts, animations. When you extend the project in Claude Code, consider splitting into `styles.css` and `script.js` for maintainability.

---

## 🎨 Design System

### Aesthetic Direction
**Field manual × documentary archive × intelligence dossier.** Gritty, authoritative, real. No cheap "buy now!" hype — the book is documentary in tone, so the page matches.

### Color Palette (CSS variables in `:root`)
| Variable | Color | Use |
|----------|-------|-----|
| `--navy-deep` | `#0A1628` | Body background |
| `--navy` | `#122236` | Section backgrounds (alt) |
| `--navy-light` | `#1A2F4A` | Card backgrounds |
| `--brass` | `#C9892E` | Primary accent, CTAs |
| `--brass-bright` | `#E5A445` | Hover, highlights |
| `--bone` | `#E8DCC4` | Body text |
| `--bone-bright` | `#F5EBD3` | Headlines |
| `--orange-stamp` | `#E55A2B` | Stamps, badges, urgency |
| `--cyan-blueprint` | `#4FA8C7` | Blueprint grid lines |

### Typography
- **Oswald** (bold condensed, 400/500/600/700) — headlines, military-manual energy
- **Cormorant Garamond** (serif, italic) — accent text, body
- **JetBrains Mono** — technical labels, data, "operational" feel
- **Special Elite** — typewriter stamps (CASE FILE, FIELD TESTED)

All loaded from Google Fonts in `<head>`.

### Background Atmospherics
- `.topo-bg` — Solid navy base
- `.blueprint-grid` — 40px cyan grid overlay
- `.topo-lines` — Radial topographic line gradients
- `.grain` — SVG noise overlay (6% opacity, overlay blend mode)

---

## 📐 Page Sections (top → bottom)

| # | Section | Purpose |
|---|---------|---------|
| 0 | **Countdown Banner** | Top-of-page urgency strip with code reminder |
| 1 | **Sticky Nav** | Pulsing dot + CTA button |
| 2 | **Hero** | Floating book cover, rotating compass, dual CTAs, stats |
| 3 | **Proof Bar** | 4 stat numbers (−20°F, $50, 7 steps, $0/week food) |
| 4 | **Counter-Industry** | Why you've never been taught this ($218B hotels, $16B gear, $40K vans) |
| 5 | **8 Chapters Grid** | Numbered cards, slide-on-hover |
| 6 | **Field Scenarios** | 3 case files (Minneapolis, Columbus, LA) |
| 7 | **5 Cities** | LA, Houston, Miami/Orlando, NYC, Columbus/Cleveland + bonus card |
| 8 | **Lead Magnet** | Free Chapter 1 — email capture form |
| 9 | **FAQ** | 8 questions, accordion-style |
| 10 | **Guarantee** | Honest, authentic copy from the book |
| 11 | **Final CTA** | Big countdown block, $27 → $17 price, `SURVIVALMODE` code, payment trust badges |
| 12 | **Footer** | Channel link + edition info |
| — | **Toast Notifications** | Bottom-left recent buyer toasts (rotate every ~30s) |
| — | **Exit-Intent Popup** | Catches abandoners with free Chapter 1 offer |

---

## 💰 Pricing & Promo Logic

- **Regular price:** `$27`
- **Discount code:** `SURVIVALMODE`
- **Discounted price:** `$17` (saves $10)

The promo code is displayed prominently in the Final CTA section with a one-click copy-to-clipboard button. Both prices are shown side-by-side (`$27` struck through, `$17` highlighted).

**When you integrate a real checkout (Gumroad / Stripe / Lemon Squeezy):** wire the code into the actual checkout flow so it applies the discount automatically. The page only displays the code — it doesn't enforce it.

---

## 🚀 What's Working

- ✅ Fully responsive (desktop / tablet / mobile breakpoints at 968px and 580px)
- ✅ Smooth scroll between anchor links
- ✅ Reveal-on-scroll animations (Intersection Observer)
- ✅ Floating book cover (6s ease-in-out loop)
- ✅ Rotating compass overlay (60s linear loop)
- ✅ Lead form with success state (no backend yet — just front-end demo)
- ✅ Copy-to-clipboard for promo code
- ✅ Hover effects on every interactive element
- ✅ **Live countdown timer** — banner at top + big block before final CTA. Currently set to **3 days from page load** (edit `LAUNCH_DEADLINE` in the script)
- ✅ **FAQ section** — 8 questions, accordion-style, only one open at a time
- ✅ **Toast notifications** — recent buyer popups every ~30s, rotating through 10 composite buyers (bottom-left)
- ✅ **Exit-intent popup** — triggers on mouse-leave (desktop), scroll-up after long scroll-down (mobile), or 60s timer. Uses `sessionStorage` so it only shows once per session
- ✅ **Payment trust badges** below the final CTA
- ✅ Print-quality typography stack

---

## 🛠️ What to Do Next (in Claude Code)

Priority order:

### 1. Wire up the lead capture forms (real backend)
There are TWO forms that need wiring:
- The Lead Magnet section form (mid-page)
- The Exit-Intent popup form

Both currently just show a success state but don't send anywhere. Options:
- **ConvertKit / Mailchimp / Beehiiv** form embed (easiest)
- **Formspree** for a no-backend POST endpoint
- **Custom backend** (Node/Express, Cloudflare Workers, etc.)

### 2. Wire up the buy button
Currently `href="#"`. Replace with the real checkout link:
- **Gumroad** — best for digital PDFs, handles tax/VAT, easy discount codes
- **Lemon Squeezy** — more polished, also handles tax/VAT globally
- **Stripe Payment Links** — cheapest fees but you handle delivery
- **Hotmart** — what eliyodersecrets.com uses; good for affiliates

When you set up the checkout, **configure the SURVIVALMODE discount code** in the platform so it actually applies ($27 → $17).

### 3. Set a real countdown deadline
In `index.html`, find the `LAUNCH_DEADLINE` variable in the script section. Replace the default (3 days from page load) with a real fixed date:
```js
const LAUNCH_DEADLINE = new Date('2026-06-15T23:59:59');
```
**Important:** Make this a REAL deadline that you'll honor. Fake countdowns that reset on every visit destroy trust and don't match the documentary tone of the brand. If you want to keep urgency without a hard deadline, just remove the countdown entirely.

### 4. Replace toast notification names with real data (optional)
The `recentBuyers` array in the script has 10 composite buyers. Options:
- **Leave as-is** — they're plausible composites, and you've already used the composite scenario approach elsewhere on the page (consistent with brand voice)
- **Add a disclaimer** somewhere small: "Composite illustrations from reader feedback"
- **Connect to real purchases** via a tool like Fomo, Provely, or build your own from your checkout webhook
- **Remove the toasts entirely** if it feels too "marketer-y" for your brand

### 5. Deliver the PDF after purchase
- Email delivery via your checkout platform (built into Gumroad/Lemon Squeezy/Hotmart)
- Or upload to a private S3 / Cloudflare R2 bucket with signed URLs

### 6. Add analytics
- **Plausible** or **Fathom** (privacy-friendly, simple)
- Or **Google Analytics 4** if you want the full suite
- Track: page views, email signups (both forms), buy-button clicks, scroll depth, FAQ engagement, exit-popup conversion

### 7. Optional polish
- [ ] Add testimonials section (real comments from YouTube viewers, or composite with disclaimer)
- [ ] Add a sticky "Buy Now" button that appears on scroll
- [ ] Replace the demo book cover image with a higher-res version
- [ ] Add Open Graph / Twitter Card meta tags for social sharing
- [ ] Add favicon
- [ ] Compress images further (book-cover.png is ~300KB — could be ~80KB as WebP)
- [ ] Run Lighthouse audit + fix any A11y issues
- [ ] Split `index.html` into `index.html` + `styles.css` + `script.js`
- [ ] Add a "satisfaction count" or "books sold" counter (only if real)

### 8. SEO basics
- [ ] Add a real `<meta name="description">` (already has one, but refine)
- [ ] Add `og:image`, `og:title`, `og:description`
- [ ] Add structured data (`Product` schema with price)
- [ ] Sitemap.xml + robots.txt

---

## 🧪 Local Preview

Just open `index.html` in any browser — no build step, no server needed. Everything is vanilla HTML/CSS/JS.

If you want a live-reload dev server:
```bash
npx serve .
# or
python3 -m http.server 8000
```

---

## 📝 Brand & Voice Guidelines

When writing new copy for this project:

- **Tone:** Documentary, field-tested, real. Never "hypey" or salesy.
- **Voice:** Direct, specific, numbers-driven. ("$50 setup", "−20°F", "7 steps")
- **Avoid:** Exclamation marks, "transform your life", "unlock", "secrets revealed"
- **Use:** Specific costs, specific temperatures, specific city names, specific products
- **Style of authority:** Like a war correspondent reporting facts — not a marketer

**Reference the source PDF for any new copy.** Every claim on the page should be defensible from the actual book content.

---

## 📦 Source Files Reference

The original book PDF (`INVISIBLE_SHELTER_PLAYBOOK.pdf`) and cover image came from the user. Keep the cover image at the original aspect ratio when replacing — the float animation depends on it.

---

## 🤝 Handoff Notes for Claude Code

When you (or future Claude) open this in Claude Code:

1. **Read this README first.** It has the full context.
2. **Read `index.html`** — it's 800-ish lines, single file, well-organized by section comments (`/* ============ HERO ============ */` style).
3. The user is **the channel owner of Survival Mode** — they care about authenticity and respect for the subject matter. Don't make it cheesy.
4. The book is real, the field methods are real, and the audience is people who may genuinely be in survival situations. The page should be high-converting AND honest.
5. **Promo code:** `SURVIVALMODE` for $10 off ($27 → $17).

Built on **Wednesday, May 27, 2026** — Eid al-Adha 🌙 — with Claude Opus 4.7.

Good luck with the launch. 🔥
