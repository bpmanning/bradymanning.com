# Project Tracker — bradymanning.com

Running log of every meaningful change, decision, and rationale.
Entries are **newest-first**. Never overwrite — append new entries at the top under a new date/commit heading.

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
