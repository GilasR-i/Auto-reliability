# Recueil de Fiabilité — Véhicules de Tourisme & Utilitaires

An interactive, single-file web dashboard for automotive resale professionals in France. It catalogues **225 vehicles and engine variants** — passenger cars, utility vans, pick-ups, electric vehicles, no-license quadricycles, and standalone diesel engine profiles — with reliability scoring, repair cost estimates, and buy/resell price guidance.

🔗 **Démo en direct :** https://gilasr-i.github.io/Auto-reliability/

## What it does

For each entry, the tool surfaces:

- **Reliability score (1–10)** — colour-coded, based on manufacturer studies (ADAC Pannenstatistik), owner-feedback surveys (JD Power, Consumer Reports, UFC-Que Choisir, Honest John), and professional workshop/fleet feedback
- **Technical specs** — engine, transmission, drivetrain
- **Mileage alert threshold** — the point at which specific failures should be anticipated
- **Repair cost breakdown** — itemised cost ranges per likely failure (turbo, DSG mechatronics, timing chain, etc.)
- **Suggested buy price / target resale price** — indicative market ranges (2026)
- **Estimated gross margin** — colour-coded (good / correct / weak or at-risk), with explicit risk warnings on vehicles where a single major failure can wipe out the margin (e.g. Range Rover Ingenium timing chain, Renault dCi 1.6 wet timing belt)

## Sections

| Section | What it shows |
|---|---|
| **Overview** | KPI summary, best profitability opportunities |
| **Full catalogue** | Searchable/filterable/sortable card grid — filter by category, segment, **brand**, budget slider |
| **Profitability** | Vehicles ranked by estimated gross margin, high to low |
| **Comparator** | Side-by-side table for up to 3 selected vehicles |
| **Mileage buy/resell thresholds** | Horizontal range chart per vehicle, with mechanical vigilance markers |
| **Methodology & criteria** | How to read the data, its limits, suggested additional criteria |

## Coverage

- Full mainstream market: city cars, compacts, sedans/wagons, SUVs, premium/luxury, EVs, no-license quadricycles, pick-ups, and commercial vans
- Near-complete Peugeot and Renault ranges (current and historic models)
- Dedicated engine-family profiles (not tied to one body style): Peugeot/Citroën 1.6 HDi, 1.6 BlueHDi, 2.0 HDi/BlueHDi; Renault dCi 1.5, 1.6, 1.9, 2.0, 2.3, 3.0 V6

This is a curated, representative selection — not an exhaustive listing of every trim, model year, or engine code.

## Tech stack

Single self-contained `index.html` file:
- Vanilla HTML / CSS / JavaScript — no build step, no dependencies, no backend
- Data lives in a plain JS array inside the file (`DATA`) — easy to read, extend, or fork
- Google Fonts (Space Grotesk + Inter) loaded via CDN link

## Running locally

Just open the HTML file in any browser:

```bash
open index.html      # macOS
start index.html      # Windows
xdg-open index.html   # Linux
```

No server, no install, no dependencies.

## Deploying with GitHub Pages

1. Upload the HTML file to this repo (rename it to `index.html` if you want it served at the repo's root URL)
2. Go to **Settings → Pages**
3. Under "Build and deployment", set source to your default branch, folder `/ (root)`
4. Save — GitHub will publish the site at `https://<your-username>.github.io/<repo-name>/` within a minute or two

## Updating the data

All vehicle entries live in the `DATA` array near the top of the `<script>` block. Each entry follows this shape:

```js
{
  id: 1,
  cat: "tourisme",              // "tourisme" | "utilitaire"
  seg: "compacte",              // segment key, see SEGMENTS map
  name: "Toyota Corolla / Yaris (hybride)",
  era: "2018–2024, 12ᵉ-13ᵉ génération",
  score: 9,                     // 1–10 reliability score
  tech: "…",                    // technical summary
  alertKm: 150,                 // mileage alert threshold (thousands)
  alertText: "…",
  repairCosts: ["…", "…"],      // itemised repair cost strings
  achat: [60,100],              // recommended buy mileage window (thousands km)
  revente: 180,                 // recommended resale mileage ceiling (thousands km), or null
  watch: "…",                   // short vigilance summary
  prixAchat: [9000,12500],      // suggested buy price range (€)
  prixRevente: [15000,17500],   // target resale price range (€)
  risk: "…"                     // optional: explicit risk warning, shown as a red flag on the card
}
```

Brand is auto-detected from the `name` field for the brand filter (see `getBrand()` / `BRAND_PATTERNS` in the script for edge cases like "Land Rover", "DS", "MG", "Mazda2/3").

## Disclaimer

Prices, mileage thresholds, and repair costs are indicative ranges for a vehicle in good general condition, intended to support — not replace — professional judgement. Margins shown are **gross**, before refurbishment, inspection, transport, and commission costs. Vehicles flagged with a vigilance warning require a full mechanical inspection before purchase: a single unanticipated major failure can exceed the entire estimated margin.

## License

Add your preferred license here (e.g. MIT) if you plan to share or open-source this repository.
