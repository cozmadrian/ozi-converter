# WatchMeFly UTM to OziExplorer Converter

A purely client-side web application designed for Hot Air Balloon competition pilots. It extracts truncated UTM coordinates (e.g., `5484/2762`) from WatchMeFly PDF task sheets, mathematically reconstructs them based on the geographical region, and generates a timestamped `.txt` file ready for native import into OziExplorer.

## Features
* **100% Offline Processing:** Once loaded, the page processes PDFs entirely within the browser. No files are uploaded to any server.
* **Interactive Prefix Auto-Detection:** Click anywhere on the map near your competition area to automatically calculate and populate the correct UTM Zone, Letter, and grid prefixes.
* **Visual Waypoint Validation:** Upon loading the PDF, all generated coordinates are instantly plotted on the map, and the viewport auto-zooms to fit the targets. This allows pilots to visually confirm the UTM prefixes are correct before importing into their GPS.
* **Smart Task Binding:** Associates extracted targets with the closest preceding task name (e.g., `17_MDD_P1`).
* **Timestamped Output:** Files are generated with a `YYYY-MM-DD_HH-MM-SS` suffix to prevent overwriting data between morning and evening flights.
* **Memory Retention:** Remembers your UTM prefixes across sessions via Local Storage.

## How to use (For Pilots)
1. Open the [Web App URL] in your browser (Chrome/Safari).
2. **Step 1:** Click on the map near your competition center. The system will automatically calculate your UTM Zone and prefixes (the digits omitted by the competition director). You can also edit these manually if needed.
3. **Step 2:** Tap the "Choose File" button and select your downloaded WatchMeFly Task Sheet PDF.
4. **Step 3:** Review the map. The view will snap to your targets. If they are in the correct country/region, tap "Generate Text File (.txt)". 
5. Open OziExplorer, go to **Load** -> **Import Waypoints from Text File**, and select the generated file.

## Technical Details
* Uses `pdf.js` for strict client-side text extraction.
* Uses `proj4js` to dynamically compute true UTM grids from map coordinates and vice-versa.
* Uses `Leaflet.js` with OpenStreetMap for free, API-keyless interactive mapping.

## Deployment on GitHub Pages
This app requires no backend server. 
1. Fork or clone this repository.
2. Go to your repository **Settings** -> **Pages**.
3. Under "Branch", select `main` and click **Save**.
4. Your site will be live within 60 seconds.
