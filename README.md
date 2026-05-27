# bradymanning.com

Personal website for Brady Manning — Product Leader, energy industry veteran, and builder of Virtual Power Plants.

**Live site:** [bradymanning.com](https://bradymanning.com)

---

## About the Project

This site is a deliberate product decision, not just a portfolio. The goal was to build something that reflects how I think about product: clear users in mind (readers, recruiters, energy & technology peers, collaborators), vibrant and well structured.

The design direction, premium editorial meets energy infrastructure, was intentional. The site should communicate what I work on (energy infrastructure) before a word is read, then reward the reader who goes deeper.

A few choices worth noting:

**Single-file architecture.** Everything lives in `index.html` — HTML, CSS, and JS together. This keeps the project zero-dependency, trivially deployable, and fast. There's no build step, no bundler, no framework. For a personal site with no dynamic data needs, a framework would have been overhead without benefit.

**Dark mode as primary.** Most personal sites default to light. Dark-primary reinforces the energy/infrastructure aesthetic and feels intentional rather than default.

---

## Tech Stack

| Layer | Choice |
|---|---|
| Structure | Semantic HTML5 |
| Styling | Custom CSS with CSS custom properties (dark/light theming) |
| Interactivity | Vanilla JS |
| Icons | Inline SVGs (custom ICONS map — no external dependency) |
| Fonts | Google Fonts — Lato + DM Sans |
| Analytics | Cloudflare Web Analytics (privacy-first, no cookies) |
| Hosting | GitHub Pages |

---

## File Structure

```
bradymanning.com/
├── index.html                  # Main site — all HTML, CSS, JS in one file
├── 404.html                    # Custom 404 page with three energy-themed games
├── games.html                  # Standalone VPP Arcade page
├── assets/
│   ├── favicon.svg             # Negawatt wave — primary favicon
│   ├── favicon.ico             # Legacy fallback
│   ├── favicon-96x96.png       # PNG favicon
│   ├── apple-touch-icon.png    # 180×180 iOS home screen icon
│   ├── web-app-manifest-192x192.png
│   ├── web-app-manifest-512x512.png
│   ├── og-image.png            # 1200×630 Open Graph image
│   └── gm-energy-portal.png    # GM Energy project card screenshot
├── site.webmanifest            # PWA manifest
├── robots.txt                  # Crawl directives
├── sitemap.xml                 # XML sitemap for search engines
├── og-image-generator.html     # Dev tool for regenerating og-image.png (not deployed content)
└── PROJECT_TRACKER.md          # Running change log — every commit documented
```

Sections of `index.html` (in order):
- **Energy Canvas** — Fixed HTML Canvas behind the hero; energy network visualization with nodes, edges, and moving pulses. Mouse proximity spawns extra pulses. Fades on scroll.
- **Hero** — Name, typewriter cycling through roles, bio, two CTAs, social links.
- **About** — VPP narrative framing + four animated stat cards.
- **Experience** — Alternating timeline: GoodLeap → Fluence → GM Energy → NRG → Entergy.
- **Projects** — Live previews, screenshots, and sparkline demos.
- **Writing** — Filter-tab blog card grid; 5 of 6 posts are placeholder ("Coming soon").
- **Contact** — Personal note + LinkedIn CTA with animated concentric rings.
- **Footer** — Tagline, three-column grid (brand / site nav / Negawatt Weekly).

---

## Running Locally

No install required. Open `index.html` in a browser, or use a local server:

**VS Code + Live Server:**
1. Open the repo in VS Code
2. Right-click `index.html` → *Open with Live Server*
3. Site hot-reloads on save at `localhost:5500`

**Python (alternative):**
```bash
python -m http.server 8000
# Open localhost:8000
```

---

## Deployment

Deploys automatically via GitHub Pages on every push to `main`. Changes are live within ~60 seconds.

```bash
git add index.html
git commit -m "your message"
git push origin main
```

---

---

# Design System

The visual language of bradymanning.com. Use this as the reference when adding new sections, components, or pages.

---

## Brand Identity

### Wordmark
`BM` — set in Lato 800, gradient fill (cyan → violet, 135°). Used in the nav and as the conceptual logo mark. Not a full logomark — relies on typographic weight and the gradient to establish identity.

### Favicon / Icon Mark
The **negawatt wave** — a monochromatic green (`#00ff88`) SVG wave derived from the Negawatt brand. Lives at `/assets/favicon.svg`. Used across all pages and as the PWA icon at multiple sizes (96px, 192px, 512px).

The wave was chosen over a "BM" text mark because shape silhouettes outperform letterforms at 16×16px favicon size. The green matches `--accent-cyan` exactly, tying the favicon to the site's accent system.

### Voice & Tone
- Texas-rooted but globally credible
- Ambitious without being boastful — the numbers speak
- Substantive over decorative — every word earns its place
- First person, direct, no hedging
- "Howdy" is intentional; the energy industry narrative is the spine

---

## Color System

All colors are defined as CSS custom properties on `:root` (dark theme) and `[data-theme="light"]`. Dark is the primary experience; light is a supported secondary.

### Dark Theme (Primary)

| Token | Hex / Value | Usage |
|---|---|---|
| `--bg-primary` | `#07090f` | Page background, canvas backdrop |
| `--bg-secondary` | `#0d1120` | Section backgrounds (experience, writing) |
| `--bg-card` | `#0f1525` | Card surfaces |
| `--bg-card-hover` | `#141a2e` | Card hover state |
| `--text-primary` | `#e8eaf6` | Headlines, high-emphasis text |
| `--text-secondary` | `#8892b0` | Body copy, descriptions |
| `--text-muted` | `#4a5578` | Labels, dates, metadata |
| `--accent-cyan` | `#00ff88` | Primary accent — CTAs, active states, highlights |
| `--accent-violet` | `#8b5cf6` | Secondary accent — gradient partner to cyan |
| `--accent-cyan-dim` | `rgba(0,255,136,0.12)` | Subtle backgrounds behind cyan elements |
| `--accent-violet-dim` | `rgba(139,92,246,0.12)` | Subtle backgrounds behind violet elements |
| `--border` | `rgba(255,255,255,0.06)` | Default card/component borders |
| `--border-accent` | `rgba(0,255,136,0.30)` | Hover/active border on cards |
| `--nav-bg` | `rgba(7,9,15,0.85)` | Frosted nav backdrop |
| `--glow-cyan` | `0 0 30px rgba(0,255,136,0.25), 0 0 60px rgba(0,255,136,0.1)` | Cyan glow on hover |
| `--glow-violet` | `0 0 30px rgba(139,92,246,0.25), 0 0 60px rgba(139,92,246,0.1)` | Violet glow on hover |

### Light Theme

| Token | Hex / Value | Notes |
|---|---|---|
| `--bg-primary` | `#f0f2fa` | |
| `--bg-secondary` | `#e8eaf5` | |
| `--bg-card` | `#ffffff` | |
| `--bg-card-hover` | `#f5f7ff` | |
| `--text-primary` | `#0a0f2e` | |
| `--text-secondary` | `#3d4466` | |
| `--text-muted` | `#5d6680` | WCAG AA compliant (5.1:1 on `#f0f2fa`) |
| `--accent-cyan` | `#00cc6a` | Darker green for light-bg contrast |
| `--accent-violet` | `#6d28d9` | |
| `--border` | `rgba(0,0,0,0.12)` | |
| `--border-accent` | `rgba(0,204,106,0.35)` | |

### Gradients

| Name | Value | Usage |
|---|---|---|
| Brand gradient | `linear-gradient(135deg, #00ff88, #8b5cf6)` | BM wordmark, buttons, stat numbers, section title accents |
| Hero name | `linear-gradient(160deg, #e8eaf6 0%, #8892b0 100%)` | Hero `<h1>` text fill |
| Footer tagline | `linear-gradient(135deg, var(--text-primary), var(--text-secondary))` | Footer tagline text |
| Timeline connector | `linear-gradient(to bottom, transparent, #00ff88, #8b5cf6, transparent)` | Vertical timeline line |

### Timeline Dot Colors
Each experience entry has a distinct dot color, receding from most recent (brightest) to oldest (deepest violet):

| Position | Company | Color |
|---|---|---|
| 1 | GoodLeap | `#00ff88` |
| 2 | Fluence Energy | `#00d4aa` |
| 3 | GM Energy | `#5b7cf6` |
| 4 | NRG Energy | `#7464ee` |
| 5 | Entergy | `#8b5cf6` |

---

## Typography

### Typefaces

| Family | Source | Role |
|---|---|---|
| **Lato** | Google Fonts, weight 900 | Display, headings, buttons, labels, nav |
| **DM Sans** | Google Fonts, weights 300/400/500/300i | Body copy, descriptions, UI |
| `DM Mono` / `Courier New` | System fallback | Hero status label (monospace flavor) |

### Type Scale

| Name | Element | Size | Weight | Family | Notes |
|---|---|---|---|---|---|
| Hero name | `.hero-name` | `clamp(2.8rem, 6vw, 6.5rem)` | 800 | Lato | Letter-spacing -0.04em |
| Section title | `.section-title` | `clamp(2.5rem, 5vw, 4.5rem)` | 800 | Lato | Letter-spacing -0.03em |
| Contact title | `.contact-title` | `clamp(3rem, 7vw, 7rem)` | 800 | Lato | Letter-spacing -0.04em |
| Typewriter | `.hero-typewriter` | `clamp(1.1rem, 2.5vw, 1.5rem)` | 700 | Lato | Accent-cyan color |
| Project name | `.project-name` | `1.4rem` | 800 | Lato | Letter-spacing -0.02em |
| Timeline company | `.timeline-company` | `1.15rem` | 800 | Lato | Accent-cyan color |
| Post title | `.post-title` | `1.15rem` | 800 | Lato | |
| Stat number | `.stat-number` | `2.2rem` | 800 | Lato | Gradient fill |
| Nav logo | `.nav-logo` | `1.4rem` | 800 | Lato | Gradient fill |
| Button | `.btn` | `0.9rem` | 700 | Lato | Uppercase, letter-spacing 0.04em |
| Section label | `.section-label` | `0.75rem` | 600 | DM Sans | All-caps, letter-spacing 0.2em, cyan |
| About body | `.about-text p` | `1.05rem` | 300 | DM Sans | Line-height 1.8 |
| Hero bio | `.hero-bio` | `clamp(1rem, 1.8vw, 1.2rem)` | 300 | DM Sans | Line-height 1.7 |
| Timeline bullets | `.timeline-bullets li` | `0.88rem` | 300 | DM Sans | Line-height 1.6 |
| Post summary | `.post-summary` | `0.88rem` | 300 | DM Sans | |
| Project desc | `.project-desc` | `0.9rem` | 300 | DM Sans | |
| Tags / badges | `.project-tag`, `.post-tag` | `0.7rem` | 600 | DM Sans | All-caps, letter-spacing 0.08–0.1em |
| Nav links | `.nav-links a` | `0.875rem` | 500 | DM Sans | All-caps, letter-spacing 0.04em |
| Typewriter prefix | `.hero-typewriter-prefix` | `clamp(1.1rem, 2.5vw, 1.5rem)` | 300i | DM Sans | Italic |

---

## Spacing & Layout

### Container

```css
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 32px;   /* → 0 20px at ≤600px */
}
```

Nav inner max-width: `1300px` (slightly wider to accommodate all nav items).

### Section Padding

| Breakpoint | Padding |
|---|---|
| Default (desktop) | `120px 0` |
| `≤ 900px` | `80px 0` |

### Border Radius

| Value | Usage |
|---|---|
| `8px` | Buttons, hamburger button, skip link |
| `12px` | Stat cards, filter tabs (100px = pill) |
| `14px` | Game preview cards (404/games pages) |
| `16px` | Post cards, timeline cards |
| `20px` | Project cards |
| `50%` | Timeline dots, theme toggle button |

### Nav

- Height: `68px`
- Backdrop: `blur(20px)` frosted glass
- Switches to hamburger at `≤ 900px`

---

## Breakpoints

| Breakpoint | Behavior |
|---|---|
| `> 900px` | Desktop: full nav, 2-col about, 2-col timeline, 2-col projects, 3-col posts |
| `≤ 900px` | Tablet/mobile: hamburger nav, single-col timeline, single-col projects/posts, 2-col footer |
| `≤ 600px` | Mobile: tighter container padding (20px), stacked hero CTAs, single-col footer |

---

## Motion & Animation

### Global Transition

```css
--transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1)
```

Applied to: color changes, border-color, box-shadow, transform on hover states.

### Named Animations

| Name | Duration | Usage |
|---|---|---|
| `blink` | `1s step-end infinite` | Typewriter cursor |
| `float` | `3s ease-in-out infinite` | Hero scroll hint chevron |
| `dot-pulse-1…5` | `2s ease-out infinite` | Timeline dot glow rings (per-entry color) |
| `timeline-pulse-travel` | `5s linear infinite` | Traveling pulse down the timeline connector |
| `ring-expand` | `4s ease-out infinite` | Contact section concentric rings (3 staggered) |
| `fade-in` (class) | `0.7s cubic-bezier(0.4,0,0.2,1)` | Scroll-triggered entrance — opacity 0→1, translateY 40px→0 |

### Scroll Animations
- **Fade-in:** `IntersectionObserver` at `threshold: 0.12` — staggered `transitionDelay` per batch
- **Stats count-up:** `IntersectionObserver` at `threshold: 0.4` — 1.8s cubic ease-out via `requestAnimationFrame`
- **Hero canvas fade:** Opacity driven by `window.scrollY / 300` on scroll

### Performance
- Hero canvas and sparkline pause via Page Visibility API (`visibilitychange`) when tab is hidden
- Hero canvas disabled entirely when `prefers-reduced-motion: reduce`
- Canvas uses batched single `beginPath()` draw calls (separate for dim/active edges, cyan/violet pulses)

---

## Components

### Buttons

**Primary** — gradient fill, white text, cyan glow shadow:
```css
background: linear-gradient(135deg, var(--accent-cyan), var(--accent-violet));
color: #fff;
box-shadow: var(--glow-cyan);
```
Hover: `translateY(-2px)`, stronger glow.

**Outline** — transparent, muted border:
```css
background: transparent;
border: 1px solid var(--border);
color: var(--text-primary);
```
Hover: cyan border, cyan text, cyan glow, `translateY(-2px)`.

Both share: `padding: 14px 28px`, `border-radius: 8px`, `Lato 700`, `0.9rem`, `letter-spacing: 0.04em`, `display: inline-flex`, `gap: 8px`.

### Cards

**Stat Card** (`.stat-card`)
- Background: `var(--bg-card)`, border: `var(--border)`, radius: `12px`
- 2px gradient top border (cyan → violet)
- Hover: accent border, cyan glow, `translateY(-4px)`

**Project Card** (`.project-card`)
- Radius: `20px`, flex column, demo zone (220px tall) + body
- Hover: accent border, cyan glow, `translateY(-6px)`
- Demo zone variants: iframe preview, image, sparkline, placeholder icon

**Post Card** (`.post-card`)
- Radius: `16px`, padding: `28px`
- Hover: accent border, cyan glow, `translateY(-4px)`
- Whole card is clickable (JS delegates to inner `.post-read` anchor)
- Posts with `link: "#"` show "Coming soon" instead of "Read →"

**Timeline Card** (`.timeline-card`)
- Radius: `16px`, padding: `28px 32px`
- Alternating left/right layout (desktop), single column (mobile)
- Hover: accent border, cyan glow, `translateY(-4px)`

### Section Header Pattern
All sections use the same three-element header:
```html
<p class="section-label">Category</p>        <!-- cyan, all-caps, letter-spaced -->
<h2 class="section-title fade-in">Title</h2> <!-- large Lato, scroll-animated -->
<p class="section-subtitle fade-in">…</p>    <!-- muted body, max-width 600px -->
```

### Filter Tabs
`.filter-tab` — pill shape (`border-radius: 100px`), horizontal scroll on mobile (`overflow-x: auto`, `flex-wrap: nowrap`). Active tab: gradient fill, white text, transparent border.

### Tags / Badges
`.project-tag` — violet-tinted dim background, violet text, violet border, all-caps, `0.7rem`.
`.post-tag` — cyan text, no border, all-caps, `0.7rem`.

---

## Iconography

Icons are rendered via an inline `ICONS` map in JS — no external dependency, no network request. Each returns a complete `<svg>` string via `icon(name, size)`.

### Available Icons

| Key | Used In |
|---|---|
| `sun` | Theme toggle (dark mode) |
| `moon` | Theme toggle (light mode) |
| `menu` | Hamburger (closed state) |
| `x` | Hamburger (open state) |
| `chevron-down` | Hero scroll hint |
| `linkedin` | Connect / Message on LinkedIn buttons, social links |
| `zap` | GoodGrid project card icon |
| `bar-chart-2` | GM Energy project card icon |
| `shopping-cart` | Texas Energy Rate Shopper card icon |
| `book-open` | Goodreads social link |
| `arrow-right` | "Read →" post links, "Explore →" project links |
| `clock` | "Coming soon" label on projects/posts |

### Usage
```javascript
icon('arrow-right', 14)
// Returns full <svg class="icon" ...> string for use in innerHTML
```

SVG attributes: `fill="none"`, `stroke="currentColor"`, `stroke-width="2"`, `stroke-linecap="round"`, `stroke-linejoin="round"`, `aria-hidden="true"`.

### Brand Social Icons
LinkedIn, GitHub, and Substack use custom inline SVGs in `renderSocial()` (fill-based, not stroke) — these are NOT in the ICONS map.

---

## Open Graph & Social Meta

| Tag | Value |
|---|---|
| `og:title` | Brady Manning — Staff PM, VPP Builder |
| `og:description` | Product leader building the future of distributed energy… |
| `og:image` | `/assets/og-image.png` (1200×630) |
| `og:image:width` | `1200` |
| `og:image:height` | `630` |
| `twitter:card` | `summary_large_image` |
| `twitter:site` | `@negawatt_news` |
| `twitter:creator` | `@bradymanning16` |
| `theme-color` (dark) | `#07090f` |
| `theme-color` (light) | `#f0f2fa` |

The OG image (`/assets/og-image.png`) was generated via `/og-image-generator.html` using the site's energy grid canvas + negawatt wave watermark. Regenerate by opening that file in Chrome and using DevTools "Capture node screenshot" on the `#og` element.

---

## Accessibility

- **Skip link:** `<a href="#about" class="skip-link">` — visually hidden until focused, slides in from top
- **ARIA roles:** `nav[role="navigation"]`, `footer[role="contentinfo"]`, `role="list"` on timeline, `role="tablist"` on filter tabs
- **`aria-label`** on all icon-only buttons (theme toggle, hamburger, social links)
- **`aria-hidden="true"`** on all decorative SVGs, canvases, and ring elements
- **`aria-live="polite"`** on typewriter element
- **`prefers-reduced-motion`:** hero canvas disabled, stats count-up skips animation
- **Color contrast:** `--text-muted` in light mode (`#5d6680` on `#f0f2fa`) passes WCAG AA at 5.1:1
- **Post cards:** whole card is clickable; keyboard/screen reader users reach the inner anchor directly

---

## Content Architecture

All editable content lives in `CONTENT_CONFIG` at the top of the `<script>` block in `index.html`. Render functions (`renderStats`, `renderExperience`, `renderProjects`, `renderPosts`, `renderSocial`) pull from this object — no content is hardcoded in HTML (except the About section body copy and footer tagline).

```javascript
CONTENT_CONFIG = {
  social:     { linkedin, github, goodreads, substack },
  hero:       { name, typewriterPrefix, typewriterPhrases[], bio, ctaPrimary, ctaSecondary },
  stats:      [ { number, label } ],
  experience: [ { company, role, date, bullets[] } ],
  projects:   [ { name, icon, tags[], desc, previewUrl|imageUrl|demoType, link, target, rel } ],
  posts:      [ { title, date, tag, summary, link, target, rel } ],
}
```

---

## Contact

[LinkedIn](https://linkedin.com/in/brady-manning) · [Substack](https://newsletter.bradymanning.com) · [negawatt.news](https://negawatt.news)
