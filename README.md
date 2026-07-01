# Spark Repair Estimator

Mobile-first repair cost estimator PWA for house flippers. Built for the Spark Homes Developer Contest.

## Approach

Vanilla JavaScript with a modular event-driven architecture. Uses `localStorage` for project/state persistence and IndexedDB for photo storage. The UI is fully responsive and optimized for one-handed use in the field.

## Libraries Used

- **SheetJS (xlsx-js-style)** – Excel export
- **JSZip** – ZIP packaging for exports

## How to Run Locally

1. Clone this repository
2. Open `index.html` in any modern browser
3. No server, build tools, or dependencies required – it's fully self-contained

## Features

- 75+ repair items across 19 collapsible groups
- Multi-room support (Bathrooms, Bedrooms, Living Areas)
- Photo capture with IndexedDB persistence
- ZIP export with Excel breakdown + photos
- Price overrides (per-project + global CSV upload)
- Deal Analyzer (creative addition – calculates profit, ROI, and 70% rule)

## Live Demo

