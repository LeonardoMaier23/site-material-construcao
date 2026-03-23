# CLAUDE.md — AI Assistant Guide for site-material-construcao

## Project Overview

**ConstroBR Materiais de Construção** is a Brazilian building materials e-commerce website. The entire site is a single self-contained static HTML file (`construcao-br.html`) with all CSS and JavaScript embedded inline. There is no build system, no framework, and no dependencies beyond a Google Fonts CDN import.

---

## Repository Structure

```
site-material-construcao/
├── construcao-br.html   # Complete website (2,272 lines, ~75KB)
├── README.md            # Minimal project title only
└── CLAUDE.md            # This file
```

---

## Technology Stack

| Layer      | Technology                         |
|------------|-------------------------------------|
| Markup     | HTML5 (semantic elements)           |
| Styling    | Vanilla CSS3 with custom properties |
| Scripting  | Vanilla JavaScript (no libraries)   |
| Fonts      | Google Fonts CDN (Barlow family)    |
| Build      | None — deploy the HTML file as-is   |

There is no `package.json`, no Node.js toolchain, no TypeScript, no linter, and no formatter configured.

---

## File Organization: construcao-br.html

The file follows this top-to-bottom structure:

| Lines (approx) | Section                        |
|----------------|--------------------------------|
| 1–1346         | `<head>`: meta, fonts, `<style>` (all CSS) |
| 1347–1425      | Header & navigation bar        |
| 1426–1475      | Hero section                   |
| 1476–1575      | Trust bar                      |
| 1576–1693      | Product cards                  |
| 1695–1724      | Promotional banners            |
| 1725–1965      | Construction calculators       |
| 1966–2015      | Services section               |
| 2016–2060      | Customer reviews               |
| 2062–2073      | Newsletter / email capture     |
| 2075–2162      | Footer                         |
| 2163–2197      | Floating WhatsApp button       |
| 2198–2272      | `<script>` (all JavaScript)    |

HTML sections are separated by `<!-- Section Name -->` comments — preserve these.

---

## Design System

### Color Palette (CSS custom properties)

```css
--orange:       #E84B0C  /* primary brand color */
--orange-dark:  #C43C07
--orange-light: #FF6B35
--yellow:       #F5A623
--dark:         #1A1208
--dark2:        #2C1F0E
--dark3:        #3D2C14
--mid:          #6B4E2A
--sand:         #C8A96E
--sand-light:   #E8D5B0
--cream:        #FAF5EC
--white:        #FFFFFF
--gray:         #888070
--gray-light:   #F0EBE0
--green:        #2D7D3A
--red:          #C0392B
```

Always use these variables — never hardcode hex colors in new CSS.

### Typography

- Font family: `Barlow`, `Barlow Condensed`, `Barlow Semi Condensed` (Google Fonts)
- Weights used: 400, 500, 600, 700, 800, 900
- All text is in Portuguese (Brazilian)

### Layout

- Max-width container: `1400px`
- Primary layout tools: CSS Grid and Flexbox
- Hero grid: `grid-template-columns: 1fr 320px`
- Desktop-first approach (no explicit mobile breakpoints observed)

---

## Naming Conventions

### CSS Classes

- **kebab-case** for all class names
- Examples: `.hero-main`, `.prod-card`, `.footer-col-title`, `.trust-bar`
- Component-scoped prefixes (e.g., `prod-` for product, `calc-` for calculator)

### HTML IDs

- Short abbreviations for calculator inputs: `aw` (alvenaria-width), `ah` (alvenaria-height)
- Descriptive IDs for panels: `calc-alvenaria`, `calc-tinta`, `calc-concreto`, `calc-piso`

### JavaScript

- camelCase function names: `calcAlvenaria()`, `calcTinta()`, `switchTab()`, `addCart()`
- No external libraries, no modules, no classes — plain procedural functions

---

## JavaScript Functionality

All JS is in the closing `<script>` block (approx. lines 2198–2272):

| Function            | Purpose                                         |
|---------------------|-------------------------------------------------|
| `calcAlvenaria()`   | Brickwork calculator (bricks, cement, sand)     |
| `calcConcreto()`    | Concrete/floor mix volume calculator            |
| `calcTinta()`       | Paint quantity calculator (liters, cans)        |
| `calcPiso()`        | Tile/flooring calculator with waste factor      |
| `showCalc(id)`      | Toggle display of calculator panels             |
| `switchTab(idx)`    | Switch active tab in product sections           |
| `updateCountdown()` | Countdown timer for promotional offers          |
| `addCart(btn)`      | Visual cart-add feedback on product buttons     |
| `addToCart()`       | Alert notification for cart action              |

---

## Business Context

- **Brand**: ConstroBR Materiais de Construção (founded 2008)
- **Language**: All content is in Portuguese (pt-BR)
- **Market**: Brazil — uses BRL (R$), PIX, boleto, LGPD compliance
- **Product categories**: Cimento & Argamassa, Ferramentas, Hidráulica, Elétrica, Acabamentos, Madeiras, Tintas, EPI & Segurança, Jardim & Área Externa
- **Scale**: 45K+ products, 500+ brands, 250K+ customers

---

## Development Workflow

### Making Changes

Since there is no build system, editing is direct:

1. Open `construcao-br.html` in a text editor
2. Make changes to HTML, CSS (in `<style>`), or JS (in `<script>`)
3. Open the file in a browser to verify (file:// or any local HTTP server)
4. Commit and push

### Running Locally

Any static server works:

```bash
# Python (no install needed)
python3 -m http.server 8080

# Node (npx, no install needed)
npx serve .
```

Then open `http://localhost:8080/construcao-br.html`.

### No test suite, no linter, no formatter

There are no automated checks. Verify changes visually in a browser.

---

## Git Conventions

- Default development branch: `master`
- Feature branches follow the pattern `claude/<description>-<id>`
- Commit messages should be descriptive (e.g., `Fix paint calculator unit conversion`)

---

## Key Constraints & Warnings

- **Do not introduce external JS dependencies** — the site intentionally has no npm ecosystem. If adding interactivity, use vanilla JS.
- **Do not split the file** without a clear migration plan — the single-file approach is intentional for simplicity of deployment.
- **Preserve section comments** (`<!-- Section Name -->`) as they serve as navigation landmarks.
- **Always use CSS variables** for colors — never hardcode hex values.
- **Content language is pt-BR** — all user-facing text additions must be in Portuguese.
- **LGPD compliance** is referenced in the footer — be mindful when adding any analytics, tracking, or data collection features.
- **CNPJ/company data** (12.345.678/0001-90) appears to be a placeholder — do not treat it as real business data.
