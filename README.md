


# Spark Repair Estimator

A lightning-fast, offline-capable Progressive Web App (PWA) designed specifically for field agents to perform real estate walkthroughs and generate accurate repair estimates, regardless of internet connectivity.

## My Approach

My core philosophy was to build an estimator that feels incredibly premium, intuitive for one-handed mobile use, and entirely resilient to the harsh realities of field work (e.g., spotty cell service, large photo payloads). 

Key architectural decisions include:
*   **Zero-Build Vanilla Stack:** Built exclusively with pure HTML5, CSS3, and modern Vanilla JavaScript. By avoiding heavy frameworks like React or build tools like Webpack, I guarantee maximum performance, rapid load times, and universal compatibility.
*   **True Offline-First (PWA):** Equipped with a `manifest.json` and a fully configured Service Worker (`sw.js`). The app caches its assets on first load, meaning it functions perfectly in airplane mode or in basements with zero reception.
*   **Dual-Storage Persistence:** 
    *   **LocalStorage:** Handles lightweight, synchronous state management (project data, custom prices, checked items).
    *   **IndexedDB:** Dedicated exclusively to handling heavy base64 image strings. This completely prevents `localStorage` quota crashes (typically limited to 5MB) and offloads photo storage/retrieval to an asynchronous background thread, keeping the UI silky smooth.
*   **Event-Driven DOM:** I utilized a single, top-level event delegation pattern (`data-action`) on the document body. This drastically reduces memory leaks from ghost event listeners and makes adding dynamic rooms/items effortless.
*   **Frictionless Mobile UX:** Implemented large clickable item rows (no hunting for tiny checkboxes), sticky tab navigation, auto-collapsed groups with inline item previews, and haptic feedback to simulate the tactile feel of a native mobile app.

## Libraries Used

To keep the application as lean as possible, I rely entirely on the browser's native APIs, with only two CDN-delivered libraries specifically dedicated to handling the robust data export:

1.  **[XLSX-js-style](https://www.npmjs.com/package/xlsx-js-style) (`xlsx.bundle.js`):** Used to programmatically generate and beautifully format the detailed Excel spreadsheet (.xlsx) entirely within the browser.
2.  **[JSZip](https://stuk.github.io/jszip/) (`jszip.min.js`):** Used to compress the JSON metadata, the generated Excel file, and all associated high-resolution walkthrough photos into a single, cleanly organized `.zip` file for easy sharing.

## How to Run Locally

1. Clone this repository
2. Open `index.html` in any modern browser
3. No server, build tools, or dependencies required – it's fully self-contained


> **Note on Updates:** If you make changes to the source code while the Service Worker is active, the browser will continue to serve the cached version. To see your changes instantly, perform a **Hard Refresh** (`Cmd+Shift+R` or `Ctrl+Shift+R`), or increment the `CACHE_NAME` in `sw.js`.

## 💰 The Deal Analyzer (Creative Addition)

I went beyond building a simple clipboard replacement. I integrated a real-time **Deal Analyzer**, accessible via the floating action button (FAB) in the bottom right corner, transforming the app into a comprehensive investment command center.

Instead of guessing if a house is a good investment after generating the repair estimate, agents can know *while they are standing in the living room*.

**Features:**
*   **Live Sync:** The Deal Analyzer ties directly into the active project's state. Every time you check a repair item (e.g., adding a $3,500 furnace), the repair total inside the analyzer updates automatically.
*   **70% Rule Engine:** Instantly calculates the Maximum Allowable Offer (MAO) using the industry-standard formula: `(ARV * 0.70) - Repairs`.
*   **Automated Profit & ROI:** Input the After Repair Value (ARV) and Purchase Price, and the engine automatically calculates Holding Costs (defaulting to 10% of ARV) to spit out projected Profit margins and Return on Investment (ROI).
*   **Visual Deal Rating:** An immediate, color-coded badge evaluates the numbers on the fly:
    *   🟢 **Great:** ROI is 20%+ and Purchase Price is at or below MAO.
    *   🟡 **Marginal:** A deal that falls in the gray area—proceed with caution.
    *   🔴 **Avoid:** ROI is below 10% or the Purchase Price exceeds MAO by more than 10%.

## Live Demo
