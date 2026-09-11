# 🚚 Vehicle Dispatch Tracker

A browser-based Single Page Application (SPA) for managing and tracking vehicle dispatch orders. Built with vanilla HTML/CSS/JS and sql.js — no server, no build process, no database installation required.

![Status](https://img.shields.io/badge/status-active-success)
![License](https://img.shields.io/badge/license-MIT-blue)

---

## 📋 Overview

Track, manage, and optimize fleet dispatch operations from a single HTML file. All data is stored locally in your browser using SQLite (via sql.js) and synchronized to IndexedDB for persistence.

---

## ✨ Features

### 📦 Order Management
- **Single & Bulk Entry** — Add orders one-by-one or via the grid-based multiple entry form
- **Full CRUD** — Create, read, update, and delete orders with automatic audit logging
- **Duplicate Detection** — Warns on duplicate ERP-style order numbers
- **Field Validation** — Required field checks and date logic (ETA must be ≥ dispatch date)
- **Fleet Validation** — Head and attachment numbers validated against fleet registry
- **Address Book Validation** — Driver badge and customer number validated against address book

### 📒 Address Book
- **Driver & Customer Registry** — Store and reuse driver and customer details
- **CSV Import/Export** — Bulk manage entries via CSV
- **Type Filtering** — Quick filter between drivers and customers
- **Order Form Integration** — Select entries directly from order forms

### 🚛 Fleet Management
- **Fleet Registry** — Track tractor heads (H-) and attachments (ET-, CT-, B-)
- **CRUD Operations** — Add, edit, delete fleet units with branch assignment
- **CSV Import/Export** — Bulk manage fleet units via CSV
- **Order Integration** — Select fleet units directly from order forms
- **Validation** — Orders can only use registered fleet units

### 🗺️ Route Mapping
- **Leaflet Integration** — Visualize order routes on an interactive map
- **Multiple Tile Styles**:
  - 🗺️ OpenStreetMap (Wikimedia)
  - 🌍 OSM Standard
  - 🛰️ Esri Satellite Hybrid (with labels)
  - 🎨 CartoDB Voyager (with API key)
- **OSRM Routing** — Road-based route calculation and distance measurement
- **Reverse Geocoding** — Auto-fill location names from coordinates via Geoapify
- **Map Style Selector** — Switch map styles directly from the map view

### 📊 Analytics & Reports
- **Status Distribution** — Doughnut chart with count/percentage labels
- **Daily Dispatch Trend** — Line chart of orders over time
- **Dispatch by Branch** — Horizontal bar chart
- **Customer Performance** — Top 10 customers by order volume

### 🖨️ Print & Export
- **Print/PDF Reports** — Filtered, paginated reports in portrait/landscape
- **Excel Export** — Export filtered orders to `.xlsx`
- **JSON/SQL Backup** — Full database export and restore

### ⚡ Productivity
- **Keyboard Shortcuts** — `Alt+N` (new order), `Alt+M` (monitor), `Alt+F` (search), `Esc` (close modal)
- **Column Customization** — Rename columns and toggle visibility
- **Bulk Operations** — Multi-row entry with confirmation
- **Auto-scroll Modals** — Modals open scrolled to top

### 🖥️ Monitoring
- **Tabbed Monitor** — In Progress / Completed / Cancelled views
- **Branch Filtering** — Filter by reporting terminal
- **Real-time Status** — Latest tracking status per order via SQLite view

### 🔒 Data & Security
- **Local-First** — All data stays in your browser
- **IndexedDB Persistence** — Automatic backup to browser storage
- **Audit Trail** — Full history of create/update/delete/import/export actions
- **No External Accounts** — No login, no cloud sync, no tracking

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| **Frontend** | Vanilla HTML5, CSS3, JavaScript (ES6+) |
| **Styling** | Tailwind CSS (CDN) + custom CSS |
| **Database** | SQLite via [sql.js](https://github.com/sql-js/sql.js) |
| **Persistence** | IndexedDB (automatic sync) |
| **Maps** | Leaflet + OSRM + Geoapify |
| **Charts** | Chart.js v4 |
| **Export** | ExcelJS |

---

## 🚀 Getting Started

### Prerequisites
- A modern web browser (Chrome, Firefox, Edge, Safari)
- No server or build process required

### Installation

1. Clone or download this repository:
```bash
git clone https://github.com/bernando-minguita/Vehicle-Dispatch-Tracker.git
```

2. Open `index.html` in your browser:
```bash
# Windows
start index.html

# macOS
open index.html

# Linux
xdg-open index.html
```

That's it. The app initializes with sample data on first load.

---

## 📖 Usage

### Adding Orders
- **Single Order**: Click **Add Order** or press `Alt+N`
- **Multiple Orders**: Click the dropdown next to **Add Order** → **Add Multiple Orders**
- Fill in required fields (marked with `*`). The app validates dates and required fields before saving.
- Use the **Fleet** button next to Head/Attachment fields to select from registered fleet units.

### Managing Fleet
- Click **Fleet** in the header to open the fleet management modal
- Add tractor heads (H-*) and attachments (ET-*, CT-*, B-*)
- Import/export fleet data via CSV
- Fleet units are validated when creating or updating orders

### Tracking Orders
- Expand any order row to see tracking history
- Click the **+** button to add tracking updates with location, status, and remarks
- Use the **Track** button to visualize the route on the map

### Monitoring
- Click **Monitor** to see orders grouped by status
- Use the branch/terminal filter to narrow results
- Click **Reporting by Terminal** to enable branch-based filtering

### Analytics
- Click **Charts** to view status distribution, trends, and performance metrics
- Charts respect the active month and branch filters

### Printing/Exporting
- Click **Print Report** to generate a formatted report
- Use **Export → Excel** or **Export → JSON** for data exports
- **Database → Export Backup** creates a `.sqlite` file for safekeeping

---

## ⚙️ Configuration

Access settings via the **Settings** button:

- **Branch** — Set your active branch (Dammam, Riyadh, Jeddah)
- **Active Month** — Filter orders by month
- **Time Format** — Toggle between 12h and 24h time display
- **CARTO API Key** — Optional key for CartoDB Voyager map tiles
- **Geoapify API Key** — Required for reverse geocoding and routing
- **Password Lock** — Enable app lock with SHA-256 hashing and auto-lock timeout (1–30 minutes)

Settings are saved to `localStorage` and persist across sessions.

---

## 🗺️ Map Styles

| Style | Description | Key Required |
|-------|-------------|--------------|
| 🗺️ OpenStreetMap | Default Wikimedia tiles | No |
| 🌍 OSM Standard | Standard OSM tile server | No |
| 🛰️ Esri Hybrid | Satellite imagery with labels | No |
| 🎨 CartoDB Voyager | Clean vector-style tiles | Yes |

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Alt + N` | Open new order modal |
| `Alt + M` | Open monitor modal |
| `Alt + F` | Focus search input |
| `Esc` | Close topmost modal |

*Shortcuts are suppressed when typing in text fields.*

---

## 🗂️ Data Storage

| Layer | Purpose |
|-------|---------|
| **SQLite (sql.js)** | In-memory database with full SQL support |
| **IndexedDB** | Persistent backup of the SQLite binary |
| **localStorage** | Settings, map preferences |

> **Note**: Data is stored locally in your browser. Clearing browser data will reset the app. Use **Database → Export Backup** to preserve your data.

---

## 🔒 Privacy

- No data is sent to external servers (except tile/geocoding requests)
- No accounts, no login, no telemetry
- All order data, tracking history, and audit logs remain in your browser
- Sample data is fictional and randomized

---

## 🧪 Testing

No automated tests are included. The app is manually tested on:
- Chrome (latest)
- Firefox (latest)
- Edge (latest)

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Make your changes
4. Test thoroughly in multiple browsers
5. Submit a pull request

---

## 📄 License

MIT License — feel free to use this project for personal or commercial purposes.

---

## 🙋 Support

For issues, questions, or feature requests, please open an issue on GitHub.

---

*Built with ❤️ for fleet operations teams*
