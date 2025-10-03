# VAAMG Carbon Footprint Calculator (DOS / DEFRA 2025)

A lightweight, static web app (single `index.html`) to calculate VAAMG’s GHG emissions for DOS framework requirements using **DEFRA 2025** conversion factors.

> ❗️The app does **not** bundle DEFRA factors. You load them yourself (CSV/XLSX) to ensure you’re using the authoritative dataset.

## Features
- Import DEFRA Full Set (CSV/XLSX) or paste CSV.
- Data entry screens: Electricity, Gas, Business Travel, Commuting, Cloud/IT, Purchased Services, Hotels, Couriers.
- Auto‑calculations with unit handling and annual **Scope 1/2/3** roll‑up.
- **CRP summary**: baseline vs most‑recent year and % reduction.
- Saves to your browser’s **localStorage**; export/import JSON; export **Results CSV**.
- No charts (kept intentionally minimal).

## Quick start (GitHub Pages)
1. Create a public repo (e.g., `vaamg-carbon-app`).
2. Add files:
   - `index.html` (the app)
   - `README.md` (this file)
   - `DEFRA_2025_Full_template.csv` (starter template)
3. Settings → **Pages** → Source: *Deploy from a branch* → Branch: `main` → Folder: `/root`.
4. Open `https://<your-username>.github.io/vaamg-carbon-app/`.

## Loading DEFRA 2025 factors
1. Download the **Full set** workbook from GOV.UK and open the master table.
2. Prepare a CSV with **exact three columns** (case-insensitive headers are okay):
   - `Activity`
   - `Unit`
   - `Factor (kgCO2e per unit)`
3. In the app → **Load file (CSV/XLSX)** or **Paste CSV**.

> The app looks up emission factors by the **Activity** string. If your activity names differ, you can still use the app, but ensure you include the activities you actually use (see below).

### Activity keys used by the app (must exist in your data to avoid fallbacks)
- `UK Electricity - location-based grid average`
- `Natural gas`
- `Passenger car - petrol, average`
- `Passenger car - diesel, average`
- `Passenger car - battery electric (BEV)`
- `Passenger car - hybrid`
- `Motorcycle - average`
- `Taxi`
- `Rail - national rail`
- `Bus - local`
- `Bus - coach`
- `Short-haul flight (economy)`
- `Long-haul flight (economy)`
- `Ferry - foot passenger`
- `Hotel stay - average`
- `Courier - small package (road)`

### Units expected
- Electricity/Gas: `kWh`
- Cars/Taxi/Motorcycle/Train: `mile`
- Bus (local/coach): `passenger mile`
- Flights (short/long haul): `passenger km`
- Ferry: `passenger km`
- Hotel: `night`
- Courier: `kg_km`

## Data entry tabs
- **Electricity_Use**: Year, kWh, Notes → EF × kWh / 1000 → tCO2e (Scope 2)
- **Gas_Use**: Year, kWh, Notes → EF × kWh / 1000 → tCO2e (Scope 1)
- **Business_Travel/Commuting**: Year, Mode, Distance, Unit (miles/km). App handles conversions for flights/ferry (km) vs. land modes (miles).
- **Cloud_Services/Purchased_Services**: Spend‑based proxy factors (kgCO2e/£).
- **Hotels**: Nights × factor / 1000.
- **Couriers**: kg × distance (km) × factor / 1000 (auto converts miles → km).

## Fallbacks
Until you load DEFRA, the app uses conservative placeholder factors. A star `*` next to a factor indicates fallback in use. Load the full dataset to remove fallbacks.

## Export/Import
- **Export Data**: saves inputs + the currently loaded factors to JSON.
- **Import Data**: restores a previous session.
- **Export results (CSV)**: annual Scope 1/2/3 and total.

## Privacy
All data stays in your browser. No server or tracking.

## Roadmap (optional)
- Supplier-specific electricity (market‑based), T&D/WTT lines for electricity Scope 3.
- Download full workbook (XLSX) of all tabs.
- Accessibility tweaks & keyboard shortcuts.

---
**Tip:** Start with `DEFRA_2025_Full_template.csv` in this repo and then paste/replace the factors with the official values.

