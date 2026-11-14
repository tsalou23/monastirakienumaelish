# Monastiraki × Enuma Elish — Athens Metro × Tokyo

Design prototype to port into the Shopify theme. Live design: https://claude.ai/artifact/86vun2eAk4k74gPY2k6jYt

- `design/Main.dc.html` — full storefront (hero, rail, campaign, grid, cart, footer). Markup + CSS + logic (`class Component`) in one file.
- `design/Garment.dc.html` — SVG garment-on-hanger illustration (placeholder until real product photos).
- `design/asset-map.json` — maps every `/_blob/<id>` URL in the design to its local file here.
- `assets/hero-frames/f001–f092.webp` — train video (7.0s–18.45s) at 8 fps, 810×1440, for the scroll-scrubbed hero canvas.
- `assets/photos/` — the 6 platform photos (1200px web versions; `full/` = 1350×1800).
- `docs/BRIEF.md` — the original creative brief.

Placeholders: product names, prices, fabrics, shipping times and station names are invented — replace with real Shopify data.

## Project layout

```
theme/      Shopify theme — the only folder that is pushed to the store
  layout/     theme.liquid (shell, overlay + cart drawer), password.liquid
  sections/   header, train-hero, clothing-rail, gap-strip, campaign, collection-grid, footer,
              main-* page sections, ee-product-data (internal, fetched by JS)
  snippets/   product-data (per-product JSON + visuals), product-json, product-photo,
              garment (SVG placeholder), product-grid, campaign-img, fonts
  assets/     enuma.css (tokens in :root), enuma.js, self-hosted woff2 fonts,
              hero-f001–276.webp (24 fps train), photo-*.jpg, hoodie-*.webp
seed/       GraphQL + JSON used to create the 8 Drop 01 products and the drop-01 collection
design/     original design artifact (reference only)
assets/     source media (video and generated frame folders are git-ignored)
```

## Workflow

```bash
cd theme
shopify theme check --path .
shopify theme push --store monastirakienumaelish.myshopify.com --theme 163065692262 --allow-live
```

- `config/settings_data.json` is in `.shopifyignore`, so pushes never overwrite theme-editor edits.
  Pull editor changes first if you edited templates in the admin: `shopify theme pull --only templates/*.json`.
- Product visuals: product image 1 = front, image 2 = side. Products without images fall back to
  `assets/hoodie-front.webp` / `hoodie-side.webp` on the rail, overlay and cart.
- Fonts are self-hosted (Commissioner, JetBrains Mono; Latin + Greek). Japanese uses system fonts.
