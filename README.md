# Louisiana Live Weather Map

An interactive, public-facing web map for **current weather conditions and short-term forecasts across Louisiana**, powered by the **National Weather Service (NWS)** and designed for **education, research, and situational awareness**.

This project integrates real-time observations, radar, alerts, administrative boundaries, and official NWS forecasts into a single lightweight web application that runs entirely on free infrastructure.

---

## 🌦️ What This Map Does

Users can:

- Click **anywhere in Louisiana** to view:
  - Current observed conditions (from the nearest reporting station)
  - Hourly forecast for that exact location
  - A direct link to the **official NWS MapClick forecast**
- Click **statewide weather station pins** to explore conditions at specific stations
- Toggle live layers:
  - Radar (MRMS Base Reflectivity)
  - Active NWS alerts
  - Louisiana state boundary
  - Parish boundaries
  - Statewide NWS station locations
- Hover over parishes and stations to see names
- Zoom seamlessly with fast performance, even with hundreds of stations

---

## 🗺️ Data Sources (Authoritative & Free)

All weather data comes from **official U.S. government sources**:

- **National Weather Service Web API**
  - Forecasts, observations, stations, alerts
  - https://www.weather.gov/documentation/services-web-api
- **NWS MRMS Radar (WMS)**
  - Base reflectivity
- **Administrative boundaries**
  - Louisiana state and parish GeoJSON files

No private APIs, no scraped data, no paid services.

---

## ⚙️ How It Works (High-Level)

### Frontend
- **Leaflet.js** for interactive mapping
- **Leaflet MarkerCluster** for fast station rendering
- Runs entirely in the browser (no backend server required)

### Smart Caching via Netlify
To ensure reliability during high-traffic events (e.g., hurricanes):

- All NWS API requests are routed through a **Netlify serverless cache proxy**
- Responses are cached for appropriate durations:
  - Stations: 24 hours
  - Points metadata: 1 hour
  - Observations: 2 minutes
  - Alerts: 1 minute
- This:
  - Prevents NWS rate limiting
  - Dramatically improves load speed
  - Keeps the site stable during storms

---

## 📁 Repository Structure

```text
/
├── index.html
├── README.md
├── louisiana_state_boundary.geojson
├── louisiana_parishes.geojson
├── netlify.toml
└── netlify/
    └── functions/
        └── nws.js
