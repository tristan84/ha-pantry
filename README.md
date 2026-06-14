# My Pantry for Home Assistant

A fast, phone-friendly **pantry / freezer / fridge inventory** app that lives
right inside Home Assistant. Tap to add, tap +/- to adjust quantities, scan
barcodes, and see low-stock / out-of-stock at a glance. Your data is stored in
your own Home Assistant and shared across every device that opens it.

> No cloud account, no external server, no API token. The app is served by this
> integration and talks only to your own HA instance.

> Tracking a workshop or garage too? See the sister integration **[Stash](https://github.com/trstan84/ha-stash)** — same app, tool/hardware categories.

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg)](https://github.com/hacs/integration)
[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=trstan84&repository=ha-pantry&category=integration)

## Features

- 📦 Categories with sub-categories (Freezer / Fridge / Pantry / Drinks / Meds / Cleaning / …)
- ✏️ **Add, edit and delete your own categories and sub-categories** (⚙︎ in the header) — icon, colour and all. Your layout syncs across devices.
- 🏷️ **Plain-word item icons** that render correctly on every phone (no missing-glyph boxes)
- ➕➖ One-tap quantity adjust, low-stock thresholds, out-of-stock alerts
- 📷 Barcode scanning (looks products up via OpenFoodFacts)
- 🔄 Real-time sync — open it on any phone/tablet and see the same list
- 🗄️ Data stored privately in Home Assistant (`.storage`), nothing leaves your network
- 💾 **Backup & restore** — automatic on-device snapshots with one-tap restore, plus downloadable full backup files and CSV import/export

## Installation

### 1 · Add the repository to HACS

[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=trstan84&repository=ha-pantry&category=integration)

Click the button above (it opens HACS with this repo pre-filled) → **Download**.
Or do it manually: HACS → **⋮** → **Custom repositories** → add
`https://github.com/trstan84/ha-pantry` as an **Integration**, then download it.

Then **restart Home Assistant**.

### 2 · Add the integration

[![Open your Home Assistant instance and start setting up a new integration.](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=pantry)

Click the button above, or go to **Settings → Devices & Services → Add
Integration → My Pantry**, and press **Submit** — there's nothing to configure.
A **My Pantry** item then appears in your sidebar. Done.

### Manual installation (no HACS)

Copy `custom_components/pantry` into your HA `config/custom_components/` folder,
restart, then add the integration as in step 2 above.

## How it works

- Setup generates a private **webhook id** for your install.
- The app is served at `/pantry-app/index.html` and shown as a sidebar panel.
- It reads/writes inventory **and your category layout** via `GET`/`POST` to
  `/api/webhook/<your-id>`, which the integration persists in HA storage. Empty
  pushes are ignored, so a fresh device can never wipe an existing list.

## Notes

- **Barcode scanner & camera:** browsers only allow the camera over HTTPS (or
  `localhost`). If you open HA over plain `http://`, scanning won't start —
  use HTTPS / Nabu Casa, or add items manually. Because the panel runs in an
  iframe, you can also open `/pantry-app/index.html` directly in a tab if your
  browser blocks the camera inside the panel.
- **Multi-device:** the last device to save wins (simple last-write-wins). Fine
  for a household sharing one list.

## License

MIT
