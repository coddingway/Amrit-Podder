# Gift Guide — Shopify theme (Ecomexperts hiring test)

A pixel-perfect **"Gift Guide"** page built on top of Shopify's [Dawn](https://github.com/Shopify/dawn) theme (v16.1.1), implemented from the provided Figma design.

The page is made of **two new sections built from scratch** — no Dawn sections, snippets, JavaScript or base CSS are reused — plus a quick-view popup with a working **Add to cart**.

**Live page:** https://ecomexperts-dtgarlx9.myshopify.com/pages/gift-guide
*(the store is password-protected)*

---

## Features

### 1. Banner section — `sections/gift-guide-banner.liquid`
- Top bar (logo, tagline, **CHOOSE GIFT** button), hero (illustration, heading, copy, **SHOP NOW** button) and bottom strip.
- **Every text is editable in the theme customizer**, including optional shorter mobile copy.
- **Animated buttons**: a fill sweeps across on hover/focus and the arrow slides — black → yellow, yellow → black.
- **Mobile**: hamburger menu built on native `<details>` / `<summary>` (no JavaScript).

### 2. Grid section — `sections/gift-guide-grid.liquid`
- **Six product blocks**, each product **selectable in the customizer**.
- A "+" hotspot per block, with its position adjustable in the customizer (desktop).
- 3 columns on desktop, 2 columns on mobile.

### 3. Quick-view popup — `assets/gg-grid.js`
- Native `<dialog>` (focus trap, Esc, backdrop click, ✕).
- Shows the product **name, price, description and variants**, rendered **dynamically from the product data**:
  - **Color** options → button group with a colour swatch bar
    (Shopify native swatch → Figma palette → CSS colour name → neutral grey).
  - Other options (e.g. **Size**) → accessible custom dropdown ("Choose your size").
- **Add to cart** via the AJAX Cart API (`/cart/add.js`).
- **Auto-add rule**: when the added variant has the options **Black** and **Medium (M)**, the **Soft Winter Jacket** is added to the cart in the same request.
  The product and the trigger values are section settings.

### Constraints followed
- Vanilla JavaScript only — **no jQuery**.
- **No Dawn sections or components** — the page uses its own layout (`layout/gift-guide.liquid`) without Dawn's header, footer, `base.css` or `global.js`.
- Code is commented, scoped (`gg-` CSS prefix) and Online Store 2.0 / theme-editor compatible (custom element re-initialises on section reload).

---

## Files added

| File | Purpose |
|---|---|
| `layout/gift-guide.liquid` | Standalone layout; self-hosted fonts from Figma (**Jost**, **Lustria**) |
| `templates/page.gift-guide.json` | Page template wiring the two sections |
| `sections/gift-guide-banner.liquid` | Banner section |
| `sections/gift-guide-grid.liquid` | Grid section + popup markup |
| `snippets/gg-button.liquid` | Animated button (link or `<button>`) |
| `snippets/gg-icon.liquid` | Inline SVG icons exported from Figma (`currentColor`) |
| `snippets/gg-product-data.liquid` | Compact product JSON for the popup (pre-formatted prices, swatches) |
| `assets/gg-banner.css`, `assets/gg-grid.css`, `assets/gg-button.css` | Section styles |
| `assets/gg-grid.js` | Popup, variant selection, add to cart, auto-add rule |
| `assets/gg-hero-*.svg` | Hero illustrations exported from Figma (desktop + mobile) |
| `assets/gg-jost.woff2`, `assets/gg-lustria.woff2` | Fonts (SIL Open Font License) |

---

## Setup

1. Connect the repository to the store with the **Shopify GitHub integration** (Online Store → Themes → Import → Connect from GitHub) and publish the branch.
2. In **Online Store → Pages**, create a page (e.g. "Gift Guide") and set its **Template** to `gift-guide`.
3. In the theme customizer, pick the six products in the **Gift Guide grid** section and the product to auto-add (defaults: the six products from the design and *Soft Winter Jacket*).

### Local development

```bash
shopify theme dev --store <your-store>.myshopify.com
```

```bash
shopify theme check
```

---

## Branches

- `master` — clean Dawn v16.1.1 (as downloaded from the store).
- `development` — Gift Guide implementation; merged into `master` via pull request.

---

Built on [Dawn](https://github.com/Shopify/dawn) by Shopify — see `LICENSE.md`.
