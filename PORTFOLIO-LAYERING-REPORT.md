# Portfolio Layering Report

Date: 2026-04-26
Scope: layer founder + literary material onto the existing four-project hub
without removing AI-GameFriend, Lupino, NexTool, or Hardfeldt Moberg
Consulting from the public structure.

## What was added

### 1. New `#om-mig` section (between hero and `#work`)
- `<section id="om-mig">` with section-label "Om mig" / "About".
- Three paragraphs in the existing visual style:
  - Lead pull-quote on the accent border-left (14 år socialtjänst, 4
    parallella projekt sedan 2024, 2 manuskript på 4 månader).
  - Body paragraph anchoring the four projects to social work background.
  - Body paragraph linking the AXIOM literary work to LATENT methodology.
  - Closing one-liner: lives in Kista, responds to email same day.
- Discoverable from the nav (added "Om mig" as the first nav item).

### 2. AXIOM imprint mark inside `#literature`
- New `.imprint-mark` element above the existing section-label: `AXIOM`
  in serif caps with a thin accent border (premium-restrained, not loud).
- New `.imprint-tagline` below the section-title framing AXIOM as the
  literary signature with the existing genre line.
- The three book cards (Mörkret vissa bär, Att födas och dö tom,
  Hortus Gratia) are unchanged.

### 3. Methodology renamed Metodologi → LATENT
- Nav label: "Metodologi" → "LATENT".
- Section-label inside `#method`: "Metodologi" → "LATENT".
- New section-desc explains what LATENT means in one sentence so visitors
  who land here cold understand the term immediately.
- **Section ID stays `#method`** — every inbound link / external bookmark
  pointing to `#method` continues to resolve correctly. This is the
  navigation-safety condition you asked for.

### 4. Footer made useful
- New `.footer-links` row above the existing © Kista line: Om mig, Arbete,
  AXIOM, LATENT, Mejl, LinkedIn, NexTool, Lupino.
- Existing `© 2026 Pan Hardfeldt · Kista, Stockholm` line preserved exactly
  — geographic identity unchanged per your instruction.

## What was preserved (deliberately untouched)

- All four `#work` cards: AI-GameFriend, Lupino, Hardfeldt Moberg
  Consulting AB, NexTool. Same order, same hrefs.
- All inbound-link destinations:
  - `https://getnextool.com/ai-gamefriend` (AI-GameFriend card)
  - `https://lupino.se` (Lupino card + footer)
  - `https://getnextool.com` (NexTool card + footer)
  - `mailto:pan@hardfeldtmoberg.se` (Consulting card + Contact + footer)
  - `https://linkedin.com/in/panhardfeldt` (Contact + footer)
- Hero section, hero portrait wiring (`<img src="portrait.jpg">`),
  "Söker du" anchor row.
- Contact section (`#contact`), contact buttons, secondary links.
- All three literature cards verbatim.
- All five LATENT principle cards + Föreläsning / Workshop CTAs (still
  pointing to `mailto:pan@hardfeldtmoberg.se?subject=Föreläsning|Workshop`).
- Language toggle (SV/EN) and the JS that drives it.
- Reveal-on-scroll IntersectionObserver wiring.
- The `--accent: #c8a46e` premium dark visual identity.

## What was NOT added (out of scope per your instructions)

- No hype copy. No superlatives.
- No private business strategy exposure.
- No removal of revenue/project paths.
- No favicon / og:image / twitter:image / Schema.org JSON-LD additions
  (separate concern — flagged earlier when wiring portrait.jpg).

## Technical changes

| File | Lines before | Lines after | Delta |
|---|---|---|---|
| `index.html` | 920 | 1022 | +102 (new section + CSS) |

CSS additions (inside the existing `<style>`):
- `.about-grid`, `.about-lead`, `.about-body` — Om mig layout
- `.imprint-mark`, `.imprint-tagline` — AXIOM badge + tagline
- `.footer-links` — useful footer row, mobile-flex-wrap-friendly

JS: no changes. The existing `setLang()` only swaps `textContent` of
`[data-sv]` elements, so I deliberately kept all new `data-sv` /
`data-en` attribute values as plain text (no inline `<a>` tags inside
attribute strings — they would have been HTML-stripped on language
switch).

## Build / mobile check

- **No build step** (static single-file HTML — no Node, no Vite, no
  Astro). "npm run build" doesn't apply here.
- **Mobile (375px) check**: existing `@media (max-width: 768px)`
  rules cover hero collapse + nav hide + portrait resize. New CSS
  follows the same pattern (single-column grids, flex-wrap rows,
  no fixed widths). Visual confirmation requires a browser pass —
  not done via headless tooling in this commit.
- **HTML balance**: `<section>` open/close pairs verified, no orphan
  tags, no `data-sv` attributes containing raw HTML.

## Anchor link integrity

| Anchor | Resolves to | Status |
|---|---|---|
| `#om-mig` (nav, footer) | new `<section id="om-mig">` | ✓ |
| `#work` (nav, footer, hero) | existing `<section id="work">` | ✓ |
| `#literature` (nav, footer, hero) | existing `<section id="literature">` | ✓ |
| `#method` (nav, footer) | existing `<section id="method">` | ✓ (renamed label, ID kept) |
| `#contact` (nav, hero) | existing `<section id="contact">` | ✓ |
| `#ai-gamefriend` (hero, footer indirectly) | existing `<div id="ai-gamefriend">` | ✓ |
| `#consulting` (hero) | existing `<div id="consulting">` | ✓ |

## Commit + push status

This pass is committed on the current branch (`main`). **Not pushed.**
You'll need to `git push` (or tell me to) before the live site
updates. Per your instruction: "Do not push or create PR unless I
explicitly ask."
