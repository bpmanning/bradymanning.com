# Project Tracker — bradymanning.com

Running log of every meaningful change, decision, and rationale.
Entries are **newest-first**. Never overwrite — append new entries at the top under a new date/commit heading.

---

## 2026-06-07 — Add headshot to About section

**Commit:** `fb90484`

Added Brady's headshot to the About section right column, above the stat cards:

- **Layout:** Restructured about-grid from two `<div>` children to three explicit siblings — `about-col-left` (text), `about-photo-wrap` (photo), `about-stats-wrap` (stats). Desktop uses `grid-column`/`grid-row` to place photo top-right and stats below it, with text spanning full left column height.
- **Mobile:** Photo moves to `grid-row: 1` (top of About section), bio text to row 2, stats to row 3 — face first, then story, then numbers. Main responsive media query handles all three placements.
- **Styling:** `border-radius: 12px`, subtle cyan glow border (`box-shadow`), hover intensify effect, light mode variant. `loading="lazy"` for performance.
- `Brady_Manning_Photo.png` added to assets.

---

## 2026-06-07 — JSON-LD Person schema and sitemap update

**Commit:** `3a2d6e9`

SEO improvements targeting name+qualifier search queries rather than competing on bare "Brady Manning" (dominated by NFL content):

- **JSON-LD Person schema** added to `<head>` — tells Google who Brady is via structured data: name, jobTitle, description, TX address, sameAs links (LinkedIn, GitHub, newsletter, Medium), knowsAbout topics (VPPs, DERMS, BESS, demand response, ERCOT, product management, grid-edge technology), alumniOf (HEC Paris, Texas A&M).
- Target queries: "Brady Manning energy", "Brady Manning product manager", "Brady Manning VPP", "Brady Manning GoodLeap" — winnable niches vs. unwinnable bare-name NFL results.
- **sitemap.xml** lastmod updated from 2026-05-27 → 2026-06-07 on both URLs to prompt re-crawl.

---

## 2026-06-07 — Past-tense corrections for GoodLeap role

**Commit:** `431a0e2`

Fixed present-tense copy that implied Brady was still at GoodLeap:

- **About para 1:** "I'm a Staff Product Manager at GoodLeap, where I lead..." → "Most recently, I was Staff Product Manager at GoodLeap, where I led..."
- **About para 2:** Added GoodLeap to the company list (it was missing entirely); reordered to most-recent-first: GoodLeap, Fluence, GM Energy, NRG, Entergy.
- **Experience bullets (GoodLeap):** "Leading / Building / Driving" → "Led / Built / Drove"

---

## 2026-06-07 — Hide placeholder blog posts

**Commit:** `49362a8`

Writing section now only renders posts with a live link. `renderPosts()` filters `CONTENT_CONFIG.posts` to exclude any entry where `link` is `null` or `'#'` before building the grid. The five placeholder posts remain in config and will surface automatically once published. One live article ("The VPP Arms Race") now displays cleanly on its own.

---

## 2026-06-07 — Job search refresh: availability signals, resume download, copy updates

**Commit:** `fc4b8a4`

Overhauled the site to signal active job availability after Brady entered the job market:

- **Availability badge:** New pulsing green pill ("Open to new opportunities") added to the hero above the bio. Subdued styling — green dot with a `pulse-dot` keyframe animation, cyan-tinted border and background. Light mode variant included.
- **Hero bio:** Added third sentence — "I'm exploring my next chapter and looking to do the most consequential work of my career." — to signal intent without abandoning the existing personal voice.
- **Hero CTA:** Replaced two-button layout ("See My Work" + "Read My Writing") with a single "Download Resume" button (primary style, download icon) linking to `/assets/Brady_Manning_Resume.pdf`. Resume PDF added to repo.
- **Contact copy:** Replaced passive, generic copy with explicit job-search framing naming target areas: VPPs, data centers, DERMS, distributed energy resources, energy transition.
- **Page title:** `Brady Manning — Staff PM, VPP Builder` → `Brady Manning — Energy Product Leader | VPPs & Distributed Energy`
- **Meta description:** Rewritten in past tense; ends with "Open to new opportunities."
- **OG + Twitter title:** → `Brady Manning — Product Leader, Energy Innovator`
- **GoodLeap date:** `2025 – Present` → `Mar 2025 – Jun 2026`
- **Footer brand meta:** Removed `Staff PM, VPP Builder | GoodGrid · GoodLeap`; replaced with `Product Leader · Energy & VPPs`

---

## 2026-05-28 — Scroll-driven line-draw animations (About + Experience)

**Commit:** `9388766`

Added scroll-driven reveal animations to the vertical lines in the About and Experience sections:

- **Experience timeline:** `.timeline::before` converted to a faint `var(--border)` ghost track. A `.timeline-line-fill` DOM element (cyan→violet gradient) starts fully clipped and reveals top-to-bottom as you scroll through the section.
- **About section:** `.about-line-fill` div centered between the two about-grid columns (text vs. stats). Same clip-path reveal on scroll. Hidden on mobile where the grid is single-column.
- Both driven by one `requestAnimationFrame`-throttled scroll listener using `clip-path: inset(0 0 X% 0)` — no layout reflow, smooth at 60fps.
- `prefers-reduced-motion` users see both lines fully drawn immediately.

---

## 2026-05-27 — Footer redesign: tagline, 3-column layout, Negawatt CTA

**Commit:** `a152566`

Replaced the bare copyright-bar footer with a structured three-part layout:
- **Tagline row:** "Building tomorrow's grid with today's homeowners." — full-width, bold gradient text
- **Three-column grid:** (1) Brady Manning brand/identity, (2) Site nav with all 6 links stacked vertically (About → Games), (3) Negawatt Weekly description + subscribe link + social icons
- **Bottom bar:** Copyright only

Responsive: collapses to 2-column at ≤900px, single column at ≤600px.

---

## 2026-05-27 — Optimization batch: UX, SEO, accessibility, hygiene

**Commit:** `3b575ed`

Seven fixes from a fresh audit scan:

1. **Dead Writing links (#1):** `renderPosts()` now detects `link === "#"` and renders a "Coming soon" span (clock icon, same pattern as project cards) instead of a "Read →" link that silently scrolled to page top.
2. **meta theme-color (#2):** Added two `<meta name="theme-color">` tags — `#07090f` for dark preference, `#f0f2fa` for light. Mobile browsers use this to color the address bar.
3. **OG image dimensions (#4):** Added `og:image:width` (1200) and `og:image:height` (630) — improves rendering in Slack, Discord, and some LinkedIn preview scrapers.
4. **Sitemap lastmod (#3):** Updated both URLs from `2026-05-23` to `2026-05-27`.
5. **Skip link (#5):** Added `<a href="#about" class="skip-link">Skip to content</a>` at top of body with CSS that hides off-screen until focused — WCAG 2.1 AA keyboard accessibility requirement.
6. **Post card clickability (#6):** Click handler added to each `.post-card` — delegates to the inner `.post-read` anchor when the user clicks anywhere on the card outside of an `<a>` tag.
7. **Code hygiene (#7–9):** Renamed `html` → `socialHtml` in `renderSocial()` to eliminate variable shadowing; updated stale Lucide comment in CONTENT_CONFIG to reference the ICONS map; removed trailing slash from LinkedIn URL in Experience CTA to match Contact section.

---

## 2026-05-27 — Replace Lucide script with inline SVGs

**Commit:** `ac6422a`

Eliminated `lucide.min.js` (392KB) from `<head>`, which was synchronously blocking rendering on every page load. Replaced with an `ICONS` map and `icon(name, size)` helper function that returns SVG strings directly. All 12 icons (sun, moon, menu, x, chevron-down, linkedin, zap, bar-chart-2, shopping-cart, book-open, arrow-right, clock) are now hardcoded paths — zero network requests, zero parse overhead, zero render block. LinkedIn was never in Lucide v1.16.0 and was silently rendering nothing; now works correctly using a stroke-based path. Removed all 7 `lucide.createIcons()` calls and replaced every `<i data-lucide>` tag in both HTML and JS.

---

## 2026-05-22 — Social metadata, OG image, and asset reorganization

**Commit:** `f7f2029`

- Added full Open Graph + Twitter Card meta tags to `index.html`, `404.html`, and `games.html`
- Updated `<title>` on `index.html` to "Brady Manning — Staff PM, VPP Builder"
- Added `<link rel="canonical">` to all three pages
- Twitter handles: `twitter:creator` = `@bradymanning16`, `twitter:site` = `@negawatt_news`
- Added `assets/og-image.png` (1200×630) — generated via `og-image-generator.html` using the site's energy grid canvas and negawatt wave watermark
- Moved all favicon files from repo root to `assets/` and updated all `<link>` paths accordingly
- Fixed `site.webmanifest`: name ("Brady Manning"), theme/background color (`#07090f`), and icon paths updated to `/assets/`
- Added `og-image-generator.html` as a dev-only tool for regenerating the OG image

---

## 2026-05-24 — Add count-up animation to stats cards

**Commit:** `56f1397`

Refactored `renderStats()` to parse each stat string (e.g. `"100+ MW"`) into prefix, integer target, and suffix via regex, stored as `data-pre`, `data-target`, `data-suf` attributes. `IntersectionObserver` fires once when the stats grid hits 40% viewport visibility, triggering a 1.8s cubic ease-out count-up loop via `requestAnimationFrame`. Respects `prefers-reduced-motion` — skips animation and shows final values instantly if set. Fires once per page load; stays at final value on subsequent scroll.

---

## 2026-05-24 — Fix typewriter prefix and resume button label

**Commit:** `9d7bfb7`

Reverted typewriter prefix from "I'm an" back to "I'm a" (keeping "Energy Innovator" phrase as-is). Changed "Request Full Resume" button label to "Connect on LinkedIn" — the button links to LinkedIn, not a resume request form, so the label now matches the actual destination. Updated `aria-label` to match.

---

## 2026-05-24 — Pause canvas animations when tab is hidden

**Commit:** `a25512e`

Implemented Page Visibility API for the hero grid canvas and sparkline. Hero loop: replaced anonymous IIFE `(function loop(){...})()` with named `heroLoop()` function, storing the rAF ID in `heroRafId` — `visibilitychange` calls `cancelAnimationFrame` on hide and restarts on return. Sparkline: stored `setInterval` return value in `sparklineIntervalId` — `visibilitychange` calls `clearInterval` on hide and restarts the 1800ms interval on return. Prevents unnecessary CPU and battery drain when the tab is backgrounded, particularly on mobile.

---

## 2026-05-24 — Self-host Lucide icons, pin to v1.16.0

**Commit:** `439b693`

Downloaded `lucide.min.js` (v1.16.0, 392KB) to `assets/` and updated `index.html` script tag from `unpkg.com/lucide@latest` to `/assets/lucide.min.js`. Eliminates CDN dependency, unpinned `@latest` version risk, and the need for an SRI hash. `defer` intentionally omitted — `lucide.createIcons()` is called 6 times synchronously throughout the inline script. 12 icons in use: sun, moon, menu, x, chevron-down, linkedin, zap, bar-chart-2, shopping-cart, book-open, arrow-right, clock.

---

## 2026-05-24 — Add Cloudflare Web Analytics

**Commit:** `05117c2`

Added Cloudflare Web Analytics beacon script to `index.html`, `404.html`, and `games.html`. Privacy-first analytics — no cookies, no consent banner required under GDPR/CCPA. Tracks page views, referrers, countries, browsers, and devices. Free with no event caps. Dashboard accessible via Cloudflare account (same account used for negawatt.news).

---

## 2026-05-23 — Add robots.txt and sitemap.xml

**Commit:** `bc44e65`

Added `robots.txt` (allows all crawlers, blocks `og-image-generator.html`, references sitemap) and `sitemap.xml` (two public URLs: `/` at priority 1.0 and `/games` at priority 0.8, both with 2026-05-23 lastmod). 404.html and og-image-generator.html intentionally excluded from sitemap. Submit sitemap in Google Search Console to trigger immediate crawl.

---

## 2026-05-23 — Fix light mode CSS bugs and improve contrast

**Commit:** `7fc8793`

Three fixes to `[data-theme="light"]`:
- **CSS bug:** `rgba(#00cc6a, 0.35)` → `rgba(0, 204, 106, 0.35)` — invalid syntax was silently failing since launch; accent borders never rendered in light mode
- **Contrast:** `--text-muted` `#8892b0` → `#5d6680` — improves contrast ratio from ~3.2:1 to ~5.1:1 on the #f0f2fa background, passing WCAG AA (4.5:1 required)
- **Border visibility:** `--border` opacity `0.08` → `0.12` — 8% black was nearly invisible on light backgrounds

Also updated typewriter prefix to "I'm an" (index.html hero).

---

## 2026-05-23 — Fix typo and standardize game card descriptions

**Commit:** `e1a3554`

Fixed "Compat" → "Combat" typo in ERCOT Invaders card on games.html. Standardized all three game card descriptions to be identical across both 404.html and games.html: Invaders uses the longer "Combat heatwaves and freezes" version; Pac-Man uses "back to the bench" over the weaker "VPP aggregation" ending; Battery Snake was already consistent.

---

## 2026-05-22 — Add favicon (negawatt wave) across all pages

**Commit:** `3a04c45`

Added full favicon package generated via RealFaviconGenerator using the monochromatic green negawatt wave logo. Seven files added to repo root: `favicon.svg`, `favicon.ico`, `favicon-96x96.png`, `apple-touch-icon.png` (180×180), `web-app-manifest-192x192.png`, `web-app-manifest-512x512.png`, `site.webmanifest`. All five `<link>` tags added to `<head>` of `index.html`, `404.html`, and `games.html`.

**Design rationale:** The negawatt wave (monochromatic green, `#00ff88`) was chosen over a "BM" text mark — shape silhouettes outperform letter-based marks at 16×16px favicon size, and the green matches the site's `--cyan` accent exactly. The wave also carries existing brand equity from the Negawatt Substack with energy-industry audiences.

---

## 2026-05-22 — Center d-pad on mobile controls (Snake + Pac-Man)

**Commit:** `61bbe31`

The pause button was part of the flex centering calculation, pushing the d-pad left of true center. Fix: `position:relative` on `.mctrl`, then `.mctrl:has(.dpad) .cpause { position:absolute; right:14px; top:50%; transform:translateY(-50%) }` pulls the pause button out of the flex flow so the d-pad centers on its own. Defender controls unchanged (no dpad). Applied to both `404.html` and `games.html`.

---

## 2026-05-22 — 404.html: update subtitle and add scroll anchor

**Commit:** `6df26cc`

- Updated `.sub` text: "While you're here, pick a game. Scroll down to the play screen or Click here."
- Added `id="player"` to `.game-area` so `href="#player"` smooth-scrolls to the game player

---

## 2026-05-22 — Rename ERCOT Defender → ERCOT Invaders

**Commit:** `17165f5`

Updated all occurrences in `games.html` and `404.html`: card title, overlay initial HTML, and `showOverlay()` cfg object. 5 strings changed across 2 files.

---

## 2026-05-22 — games.html: "Click here" scroll anchor

**Commit:** `57c45c1`

Added `id="player"` to `.game-area` and updated the "Click here" link `href` from `"/"` to `"#player"`. Smooth-scrolls to the game player on click (leverages existing `scroll-behavior: smooth` on `html`).

---

## 2026-05-22 — Rename games page to /games; add to nav

**Commit:** `b3230b5`

- `git mv vppgames.html games.html` — URL is now `bradymanning.com/games`
- Added `<li><a href="/games">Games</a></li>` to desktop `.nav-links` (after Contact)
- Added `<a href="/games" class="mobile-link">Games</a>` to `.mobile-menu` (after Contact)

---

## 2026-05-22 — New page: vppgames.html (VPP Arcade)

**Commit:** `7316897`

### What was built
A dedicated games page at `bradymanning.com/vppgames`. Third page on the site alongside `index.html` and `404.html`. Contains all three energy games with a purpose-built hero section and 1.7× larger game cards.

### Hero copy
- Eyebrow badge (pulsing dot): `⚡ VPP ARCADE ⚡`
- Title: `Grid Games`
- Tagline: `Three games for people who think demand spikes sound like a personal challenge. The grid can handle itself for five minutes.`
- Note: `No utility background required — but it helps.` with link back to main site

### Card sizing (1.7× vs 404.html)
| Property | 404.html | vppgames.html |
|---|---|---|
| Card width | 180px | 306px |
| Preview height | 110px | 187px |
| Card-body padding | 12px | 20px |
| Internal gap | 8px | 14px |
| Name font | 0.82rem | 1.4rem |
| Desc font | 0.72rem | 0.9rem |
| Cards gap | 16px | 28px |
| Mobile stack breakpoint | ≤620px | ≤1040px |

### Game logic
All game logic (Defender, Snake, PacMan), HUD, overlay, mobile controls, keyboard input, and preview art are identical to 404.html — no divergence.

---

## 2026-05-22 — 404 page: game preview cards, HUD fix, P PAUSE, single-line headline

**Commit:** `e6c74fd`

### Game preview cards
Replaced the three plain selector buttons with full game cards. Each card contains:
- A mini canvas (`preview-cv`, 360×220 native / 180×110 displayed) with a static mid-game scene
- Game title with emoji
- One-line description
- "Play Now" button — same `.gbtn` element with existing click/active logic intact

Active card highlighted with cyan border + glow via `CSS :has(.gbtn.active)`.
Mobile (≤620px): cards stack to single column, max-width 340px.

**Preview scenes drawn by `drawPreviews()` (called once at init):**
| Game | Scene |
|---|---|
| Defender | Star field, 3×6 invader grid (red/orange/violet), cyan player ship, 3 city silhouettes, bullet in flight |
| Snake | Grid lines, 12-segment S-curve snake, "55 MW / 100 MW" progress bar, battery pickup icon |
| Pac-Man | 16×10 partial maze, pac-man with open mouth, red + violet ghosts, dots, glowing power pellets |

### HUD reset on game switch
`syncControls()` was updating the bottom instruction text but not the HUD row (score, lives, goal). Added `hud(0, 3, goalText)` call inside `syncControls()` so score resets to `0 MW`, lives show the correct symbol (◆/🔋/⚡), and goal text (`REACH 100 MW` / `EAT ALL BATTERIES` / `← → MOVE · SPACE FIRE`) updates immediately on game selection without waiting for the play button.

### P PAUSE instruction strings
Snake and Pac-Man bottom instruction strings were missing pause info. Updated to `Arrow keys to steer · P to pause` and `Arrow keys to move · P to pause`.

### Single-line 404 headline
Added `white-space:nowrap` and `max-width:none` to `.headline`. Dropped `clamp` floor from `1rem` to `0.78rem` so text scales down gracefully on narrow screens rather than overflowing.

---

## 2026-05-22 — Restore index.html after accidental overwrite

**Commit:** `8b4a964`

### Problem
Commit `463d20d` ("Remove .claude worktrees from tracking") inadvertently committed a stale local copy of `index.html` alongside the `.gitignore` changes. This wiped 290 lines of accumulated work from the file while the correct version existed in git history.

### Root cause
Brady's local repo had an older copy of `index.html` that hadn't received changes made in the Claude Code worktree. When `git add .` was run for the `.gitignore` change, the stale local file was staged and committed.

### Features wiped and restored
| Feature | Lost in | Restored from |
|---|---|---|
| Mobile energy canvas (hero section) | `463d20d` | `784e631` |
| Timeline pulse animation + dot intensity system | `463d20d` | `784e631` |
| Texas Energy Rate Shopper sparkline demo | `463d20d` | `784e631` |
| Writing filter tab horizontal scroll | `463d20d` | `784e631` |
| Substack social icon | `463d20d` | `784e631` |

### Fix
`git checkout 784e631 -- index.html` — restored from the last verified good commit (Substack icon addition). The 404 page commits between `784e631` and current HEAD only touched `404.html`, never `index.html`, so restoration was safe with no content loss.

### Prevention
Run `git pull` before committing any local file changes. Never assume the local working directory copy of `index.html` is current.

---

## 2026-05-08 — 404 page: ERCOT Defender, Battery Snake, VPP Pac-Man

**Commits:** `1e0da50`, `ca75a98`, `b59e139`, `f9e09fb`

### What was built
A custom 404 error page (`404.html`) with three energy-themed browser games:
- **ERCOT Defender** — shoot incoming demand spikes
- **Battery Snake** — grow battery capacity by collecting energy
- **VPP Pac-Man** — collect distributed energy resources

### Iterations
| Commit | Change |
|---|---|
| `1e0da50` | Initial 404 page with all three games |
| `ca75a98` | Refined version |
| `b59e139` | Refactored each game into its own namespace object to prevent state collisions between games |
| `f9e09fb` | Added pause functionality on both desktop (keyboard) and mobile; fixed mobile controls stacking vertically |

### Design decisions
- All three games in one file (`404.html`) — consistent with single-file site philosophy
- Namespace isolation prevents JS variable collisions across games
- Energy/grid metaphors throughout — consistent with site narrative

---

## 2026-05-04 — Substack social icon + writing section copy tweak

**Commits:** `784e631`, `f1eef3f`

### Substack icon (`784e631`)
Added Substack logo (SVG from Simple Icons) to both hero and footer social link rows, positioned after the Goodreads book icon. Links to `newsletter.bradymanning.com`.

**Implementation:** Added `substack` key to `CONTENT_CONFIG.social`, added `svgSubstack` inline SVG in `renderSocial()`, appended to the links array.

### Writing subtitle (`f1eef3f`)
Brady edited the writing section subtitle directly on GitHub: "leadership" → "product management" in the category description.

---

## 2026-04-29 — Mobile optimization batch

**Commits:** `ef9d1f8`, `9f29eda`, `5a2dd9b`, `d1a2af6`, `3e600d6`, `1023d4d`

### Hero canvas on mobile (`ef9d1f8`)

| Issue | Root cause | Fix |
|---|---|---|
| Canvas not showing on mobile | CSS `display: none` at `< 768px` + JS early return | Split media query; remove mobile JS gate |
| Overlay blocking canvas | Mask defaulted to `-400px` (no mouse on mobile) | Remove mask on mobile; top-down gradient overlay instead |
| Light mode canvas hidden | Overlay was solid `var(--bg-primary)` | Semi-transparent gradient for both desktop and mobile light mode |
| Canvas too heavy for mobile | 650 pulses, 45px cell size | Mobile config: 180 pulses, 62px cells |

Mobile overlay gradient (dark): `0.90 → 0.75 → 0.40` top-to-bottom.
Mouse/leave event listeners skipped on mobile (no cursor).

### Skills cloud removal + stats grid fix (`9f29eda`)
- **Removed** Core Skills tag cloud entirely from About section (HTML + CSS) — generic filler, no signal for Brady's audience
- **Fixed** stats grid: was dropping to 1-column at 600px (4 cards stacked = full screen). Now stays 2×2 at all sizes with tighter padding (16px) and font sizes (1.7rem number, 0.75rem label) on small screens

### Timeline pulse animation + dot intensity system (`5a2dd9b`, `d1a2af6`)

**Traveling pulse:**
- 8px circle animates top → bottom along connector line every 5 seconds
- Color shifts: cyan → teal → blue-violet → violet (matches connector gradient)
- Injected via JS after `renderExperience()` (which uses `innerHTML =` and would overwrite static HTML)
- Mobile: repositioned to `left: 16px` (line center = 20px, bubble width = 8px → 20 - 4 = 16px)

**Dot intensity system:**
Each of the 5 experience entries gets a distinct glow color and ring-pulse animation, top = most recent = brightest:

| Position | Company | Color |
|---|---|---|
| 1 | GoodLeap | Cyan `#00ff88` |
| 2 | Fluence Energy | Teal `#00d4aa` |
| 3 | GM Energy | Blue-violet `#5b7cf6` |
| 4 | NRG Energy | Violet-leaning `#7464ee` |
| 5 | Entergy | Violet `#8b5cf6` |

All 5 get equal glow intensity and ring pulse (2s ease-out infinite) — only color differs.

### Texas Energy Rate Shopper sparkline (`3e600d6`)
Replaced the `[Embed Demo Here]` placeholder in the project card with a live animated sparkline:
- Dark panel, "TX RETAIL ELECTRICITY" label, "● SIMULATED" badge
- Simulated $/MWh rates: range $40–$99, seeded at $65, random walk ±18 per tick
- Updates every 1.8 seconds via `setInterval`
- Bezier curve line with green gradient fill, live dot on latest point
- Price display in cyan→violet gradient using `CONTENT_CONFIG` flag `demoType: 'sparkline'`

### Writing filter tab scroll (`1023d4d`)
Filter tabs were `flex-wrap: wrap` — on mobile they'd break to multiple lines.

**Fix:** `overflow-x: auto`, `flex-wrap: nowrap`, hidden scrollbar (`scrollbar-width: none`), `-webkit-overflow-scrolling: touch` for iOS momentum. Each tab gets `flex-shrink: 0` and `white-space: nowrap`.

**Decision:** Kept "All" tab as part of the scroll row (not sticky). List is short enough (5 categories) that "All" never scrolls far off screen. Sticky "All" adds complexity and a visual seam without meaningful UX gain at this list size.

---

## 2026-04-27 — Content/style update

**Commit:** `7381870` — Direct edit via GitHub editor.

---

## 2026-04-24 — Timeline dot alignment fix

**Commits:** `5b718d6`, `f3b1b3b`, `dfdeb6f`

### Problem
Timeline dots were misaligned relative to the connector line on certain screen sizes — dots were positioned via grid column placement rather than absolute positioning.

### Fix (`5b718d6`)
Switched timeline dots to `position: absolute` with explicit `left: 50%` + `translateX(-50%)` on desktop, and `left: 12px; transform: none` on mobile. This centers dots precisely on the `::before` connector line regardless of card content height.

---

## 2026-04-23 — Content/style update

**Commit:** `9045f39` — Direct edit via GitHub editor.

---

## 2026-04-22 — Content/style update

**Commit:** `8e1c621` — Direct edit via GitHub editor.

---

## 2026-04-21 — Social icons + hero status label

**Commits:** `ccfaa64`, `be51140`

- **`ccfaa64`:** Added social icon links (LinkedIn, GitHub, Goodreads) to hero and footer. Custom inline SVGs for LinkedIn and GitHub (Lucide doesn't include brand icons); Lucide `book-open` for Goodreads.
- **`be51140`:** Updated hero status label text and adjusted its width/display behavior.

---

## 2026-04-20 — Interactive energy grid canvas

**Commits:** `3d2f991`, `85a6b51`

### What replaced what
Previous hero background: constellation/particle animation. Replaced with an energy network visualization that matches the VPP narrative.

### Canvas architecture (`3d2f991`)
- Grid of nodes with slight jitter (organic feel), connected by edges
- Two pulse types: cyan (`#00ff88`) and violet (`#8b5cf6`) at 42/58 ratio
- 650 target pulses, 850 max — constant density via one-in-one-out spawning
- Mouse proximity spawns extra pulses within 85px radius
- Overlay with radial mask: `transparent` at mouse → opaque background — creates a "torch" reveal effect
- Scroll fades canvas opacity as user scrolls past hero

### Tuning pass (`85a6b51`)
- Adjusted pulse speed range, line opacity levels
- Fixed light mode: overlay becomes semi-transparent (not full-cover) so canvas shows through
- Canvas disabled on `prefers-reduced-motion`

---

## 2026-04-19 — JS fixes, GM Energy project card, content updates

**Commits:** `50891b5`, `e725a1a`, `93e9186`, `359322a`

- **`50891b5`:** Fixed a JS syntax error causing hero loading flash
- **`359322a`:** Added GM Energy Smart Charging Portal project card; simplified GoodGrid to a static iframe (removed crossfade complexity)
- **`e725a1a`, `93e9186`:** Direct GitHub editor content updates

---

## 2026-04-17 — GoodGrid iframe preview, config-driven refactor, content polish

**Commits:** `fbcb917`, `c74fe23`, `b743b6d`, `8566c1`, `d28a9bb`

### GoodGrid live preview (`fbcb917`)
Added dual-iframe crossfade loop to the GoodGrid project card — two iframes alternate with a fade transition to simulate a live dashboard preview.

### Config-driven refactor (`c74fe23`)
Major structural change: moved all editable content (experience timeline, projects, stats) out of the render functions and into a `CONTENT_CONFIG` object at the top of the JS. Allows Brady to edit content without touching render logic.

### Other fixes
- `b743b6d`: Removed unused hero eyebrow CSS
- `8566c10`: Fixed hero section clipping on certain viewports; fixed light mode canvas behavior; fixed resume button
- `d28a9bb`: Fixed About section HTML structure; synced `$10B+` stat; added GoodGrid external link

---

## 2026-04-16 — Initial file uploads and resume PDF

**Commits:** `fbc15b8`, `bb8a809`, `d76e0cc`, `ca7598c`, `7d2c054`

Initial file uploads to the repository. Resume PDF added then removed from git tracking (large binary, not appropriate for version control). `index.html` content updates via GitHub editor.

---

## 2026-04-02 – 2026-04-03 — Site creation and early iterations

**Commits:** `54bb2c7`, `1e4dbea`, `768a9fa`, `542a05b`, `7e7aed1`, `8ac41b9`, `3778cdd`, `b717aee`, `937e923`, `bc94317`, `c263e71`, `4ea5aa2`

### Foundation
- `54bb2c7`: Initial commit
- `1e4dbea` / `7e7aed1`: CNAME created for `bradymanning.com` custom domain
- `768a9fa`: First `bradymanning.html` created
- `8ac41b9`: Renamed to `index.html` (required for GitHub Pages root)

### Early iterations (2026-04-02 – 2026-04-03)
Multiple rapid content and style iterations via GitHub editor as the site took shape. Sections built: Hero, About, Experience timeline, Projects, Writing, Contact. Dark/light mode toggle, typewriter animation, scroll-triggered fade-ins established in this period.
