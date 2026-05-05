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
| Styling | Custom CSS with CSS variables (dark/light theming) |
| Interactivity | Vanilla JS |
| Icons | [Lucide](https://lucide.dev/) |
| Fonts | Google Fonts — DM Sans + Lato |
| Hosting | GitHub Pages |

---

## Structure

```
bradymanning.com/
└── index.html       # The entire site — HTML, CSS, and JS in one file
```

Sections (in order):
- **Hero** — name, typewriter animation cycling through roles, CTAs,
- **Energy Canvas** — resembles a distribution energy grid with moving electrons
- **About** — bio, career summary
- **Experience** — career timeline: GoodLeap → Fluence → GM Energy → NRG → Entergy
- **Projects** — GoodGrid (Texas REP), GM Energy VPP Portal, ERCOT Energy Data, Book Analytics
- **Writing** — Substack essays on energy markets, VPPs, leadership, and product
- **Contact** — LinkedIn CTA

---

## Running Locally

No install required. Open `index.html` in a browser, or use a local server for accurate behavior:

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

The site deploys automatically via GitHub Pages on every push to `main`.

```bash
git add index.html
git commit -m "your message"
git push origin main
```

Changes are live within ~60 seconds.

---

## Contact

[LinkedIn](https://linkedin.com/in/bradymanning) · [Substack](https://newsletter.bradymanning.com)
