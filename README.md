# 🌦️ Nimbus Weather Card

![Nimbus Weather Card](https://github.com/maxfok/nimbus-weather-card/raw/main/Screen_Recording_2026-05-09_at_7_59_24_AM.gif)

A beautiful, Apple Weather‑inspired custom card for Home Assistant with smooth particle effects, dynamic backgrounds, and full moon phase support.

🔗 **GitHub**: https://github.com/alpha520098/nimbus-weather-card<br>
📦 **HACS**: Search "Turool Weather Card"

---

## ✨ Features

- **Stunning visuals** – gradient backgrounds, floating particles (rain, snow, fog, clouds, wind, lightning)
- **Dynamic day/night** – automatically switches between sun/moon, starry sky, and colour‑shifting gradients
- **Moon phases** – renders realistic waxing/waning moons with NASA texture and all 8 phases
- **Shooting stars** – on clear nights, a random star detaches and streaks across the sky, then fades back in
- **Feels‑like temperature** – shows apparent temperature when available
- **Smart units** – automatically converts °C/°F reading native entity attributes
- **Multilingual** – English, Spanish, German, Dutch (and more via PR!)
- **Hourly/Daily forecast toggle** – tap the forecast bar to switch view
- **Custom tap action** – navigate, call-service, url, or more-info
- **Clock & date panel** – optional, togglable
- **Custom local sensors** – add up to 8 Home Assistant entities and display their live state, unit, label, and icon below the weather details/forecast
- **HACS compatible** – one-click install via custom repository

---

## 🆕 What's new in v2.3.2

"https://github.com/maxfok/nimbus-weather-card/raw/main/Screen_Recording_2026-05-09_at_7_59_24_AM.gif"

This release focuses on Home Assistant usability: custom local sensors can be added from the editor or YAML, and the card registration has been fixed while keeping the earlier atmosphere and forecast-modal polish.

### 🧩 Home Assistant Local Sensors
Add your own Home Assistant entities under **Local Sensors** in the visual editor, or configure them in YAML with `local_sensors`. They display below the details/forecast with live state, unit, label, and icon.

### 🌅 Slow Background Cross-Fade
Sky gradients now transition with a slow 3-minute cross-fade instead of an abrupt change. Sunrise, golden hour, daytime, and night phases blend naturally as sun elevation changes. The card also schedules a refresh around key sun-elevation thresholds so the sky updates at the right moment.

### 🌌 Aurora Borealis
Clear nights in the Arctic latitude zone can show a soft aurora overlay with layered green, blue, and purple ribbons. Enabled via `latitude_zone: arctic` in your card config.

```yaml
type: custom:turool-weather-card
entity: weather.home
latitude_zone: arctic
```

### ⚡ Lightning Flash Effect
Thunderstorm conditions now include a sky-flash overlay that briefly illuminates clouds, rain, and droplets. Bolt and flash fading is slower and the secondary flash delay is longer, so strikes feel more natural.

### 📊 Forecast Modal Polish
- Haptic feedback on open/close
- Tap backdrop to close
- Swipe down from handle to close
- Escape key support on desktop
- Improved accessibility (`role="dialog"`, `aria-modal`, `aria-hidden`)
- Larger modal handle
- Better mobile gesture handling (no background scroll bleed)

### 🌠 Shooting Stars
On clear nights, a random star detaches and streaks diagonally across the sky every 4–14 seconds, then fades back into place.

### 🔧 Small Improvements
- Refined night gradient colour
- Improved layer ordering for backgrounds, aurora, effects, lightning, droplets, and content
- Moon remains visible when condition is explicitly `clear-night`
- Internal timer cleanup when card is removed or rebuilt
- Removed leftover debug logs

---

## 📋 Changelog

### v2.3.2
- ✨ **Home Assistant local sensors** — add your own entities from the visual editor or YAML and display them on the card alongside the forecast.
- ✨ **Forecast + sensors together** — local sensors no longer require disabling the forecast.
- 🐛 Fixed custom element registration so Home Assistant can load `custom:turool-weather-card` reliably, with `custom:nimbus-weather-card` retained as a backwards-compatible alias.

### v2.3.0
- ✨ **Slow background cross-fade** — sky gradients blend over ~3 minutes between elevation zones
- ✨ **Aurora Borealis** — soft aurora overlay for `latitude_zone: arctic` on clear nights
- ✨ **Lightning flash effect** — sky illumination during thunderstorms, slower/more natural timing
- ✨ **Forecast modal polish** — haptic feedback, swipe-to-close, backdrop tap, Escape key, accessibility improvements
- ✨ **Shooting stars** — existing stars detach, streak, and fade back in on clear nights
- 🐛 Moon remains visible when condition is explicitly `clear-night`
- 🔧 Internal timer cleanup, improved layer ordering, removed debug logs

### v2.2.0
#### 🌅 Sky & Sun
- New multi-phase sky gradient system with smooth colour interpolation
- 7 elevation zones: deep night → nautical dawn → blue hour → sunrise/sunset → golden hour → morning → daytime → midday
- Extended sun elevation range to −30°..90°

#### 🌙 Moon
- Moon auto-detected from `sensor.moon_phase` (no config needed)
- Moon fixed to top-right corner — no longer goes offscreen on short cards
- More precise phase calculation using UTC time

#### 📊 Forecast Modal
- Tap the forecast bar to swap between daily ↔ hourly view
- `tap_action` support: More Info, Navigate, Open URL, None

#### 📱 Mobile
- Dedicated mobile cloud rendering for sharper display on touch devices
- Better cloud detection for rainy, pouring, snowy-rainy conditions

#### 🌡️ Thermometer
- Redesigned icon matching the style of humidity, wind and pressure icons

#### 🐛 Bug Fixes
- High/Low always shows daily values even when hourly forecast is selected
- `clear-night` condition now correctly shows sun icon during daytime (fixes KNMI / NL Weather integration)

### v2.0.1
- ✨ **Multilingual support** — English, Spanish, German (thanks u/R3x10 & u/super-gando!)
- ✨ Language selector in card editor
- 🐛 Fix: HACS update notifications now work correctly (missing `filename` in hacs.json)
- 🐛 Fix: Forecast icons correctly show day/night per hour (no more moon at 1pm!)
- 🐛 Fix: Sun entity takes priority over weather state for day/night detection

### v2.0.0 — Complete rewrite 🎉
- ✨ Animated rain with wind skew (based on `wind_bearing`)
- ✨ Glass window droplets for rainy conditions
- ✨ SVG cloud layers with per-condition opacity
- ✨ Snow animation with 3-layer canvas and sine-wave sway
- ✨ Lightning with midpoint-displacement branching bolt algorithm
- ✨ Autumn leaf gusts for windy conditions
- ✨ Dynamic solar gradient based on `sun.sun` elevation
- ✨ NASA moon texture with full 8-phase rendering
- ✨ Moon hemisphere rotation based on latitude

---

## 🔧 Installation

### Via HACS (recommended)
1. Open HACS → Frontend
2. Click the three-dot menu (⋮) → **Custom repositories**
3. Add URL: `https://github.com/alpha520098/nimbus-weather-card`
4. Category: **Dashboard**
5. Click **Add**, then find **Turool Weather Card** and install

### Manual
1. Download `turool-weather-card.js`
2. Copy to `/config/www/turool-weather-card.js`
3. Add as a custom resource: `Settings → Dashboards → Resources → Add`
   - URL: `/local/turool-weather-card.js`
   - Type: JavaScript module

---

## ⚙️ Configuration

```yaml
type: custom:turool-weather-card # custom:nimbus-weather-card also works as an alias
entity: weather.forecast_home
sun_entity: sun.sun          # optional but recommended
moon_entity: sensor.moon     # optional, for moon phases
language: en                 # en | es | de | nl
show_clock: true             # optional clock/date panel
show_local_sensors: true
local_sensors:
  - entity: sensor.outdoor_temperature
    name: Outdoor
    icon: mdi:thermometer
  - entity: sensor.rain_today
    name: Rain Today
    icon: mdi:weather-pouring
tap_action:
  action: navigate
  navigation_path: /lovelace/weather
```

### All options

| Option | Default | Description |
|---|---|---|
| `entity` | required | Your weather entity |
| `sun_entity` | `sun.sun` | For accurate day/night detection |
| `moon_entity` | — | Moon phase sensor |
| `language` | `en` | `en`, `es`, `de`, `nl` |
| `show_clock` | `false` | Show clock & date panel |
| `show_details` | `true` | Show humidity, wind, pressure |
| `show_local_sensors` | `true` | Show configured `local_sensors` below weather details/forecast |
| `local_sensors` | `[]` | Up to 8 Home Assistant entities to display; each supports `entity`, optional `name`, and optional `icon` |
| `tap_action` | more-info | Standard HA tap action |
| `ufo_easter_egg` | `false` | 🛸 You'll know when you see it |
| `latitude_zone` | — | `arctic` for aurora borealis on clear nights |

---


## 🧩 Add your own sensors

You can add sensors from the visual card editor under **Local Sensors**, or directly in YAML with `local_sensors`. The card reads each entity's current Home Assistant state and `unit_of_measurement`, so temperature, rain, UV, air quality, battery, and other sensor entities can be shown without creating a new weather provider.

```yaml
type: custom:turool-weather-card
entity: weather.forecast_home
show_forecast: true
show_local_sensors: true
local_sensors:
  - entity: sensor.backyard_temperature
    name: Backyard
    icon: mdi:thermometer
  - entity: sensor.home_humidity
    name: Indoor Humidity
    icon: mdi:water-percent
  - entity: sensor.wind_gust
    name: Gusts
    icon: mdi:weather-windy
```

If an entity is temporarily `unknown` or `unavailable`, Nimbus displays `--` until Home Assistant provides a new value.

---

## 🌍 Add your language

Translations are just a few lines of JSON. Open a Pull Request!  
See existing translations in the source for the format.

---

## 🐛 Bugs & Feature Requests

Open an issue on [GitHub](https://github.com/maxfok/nimbus-weather-card/issues) or comment on the [HA Community thread](https://community.home-assistant.io/t/nimbus-weather-card/997259).

---

## ❤️ Support

If you like Nimbus, consider giving it a ⭐ on GitHub!
