# WatchMeFly UTM to OziExplorer Converter

A purely client-side, mobile-responsive web application designed for Hot Air Balloon competition pilots. It extracts truncated UTM coordinates (e.g., `5484/2762`) from WatchMeFly PDF task sheets, mathematically reconstructs them based on the geographical region, and generates a timestamped `.txt` file ready for native import into OziExplorer.

## Features
* **Built-in Search Bar:** Search for any city or region globally. The map instantly navigates there and auto-calculates the correct UTM Zone, Letter, and required Grid Prefixes for your competition.
* **Mobile & Tablet Optimized:** The UI automatically scales and stacks into a single column for narrow Android/iOS devices. Buttons and inputs feature expanded touch targets for in-flight operation.
* **100% Offline Processing:** Once loaded, the page processes PDFs entirely within the browser. No files are uploaded to any server. (Note: The map and search functions require internet, but PDF extraction and UTM reconstruction work offline using cached data).
* **Interactive Prefix Auto-Detection:** Click anywhere on the map near your competition area to automatically populate the UTM fields.
* **Visual Waypoint Validation:** Upon loading the PDF, all generated coordinates are instantly plotted on the map, and the viewport auto-zooms to fit the targets. This allows pilots to visually confirm the UTM prefixes are correct before importing into their GPS.
* **Smart Task Binding:** Associates extracted targets with the closest preceding task name (e.g., `17_MDD_P1`).
* **Timestamped Output:** Files are generated with a `YYYY-MM-DD_HH-MM-SS` suffix to prevent overwriting data between morning and evening flights.
* **Memory Retention:** Remembers your UTM prefixes across sessions via Local Storage.

## How to use (For Pilots)
1. Open the [Web App URL] in your browser (Chrome/Safari).
2. **Step 1:** Use the map's search bar (magnifying glass icon) to find your competition city, OR simply click on the map. The system will automatically calculate your UTM Zone and prefixes (the digits omitted by the competition director). You can also edit these manually if needed.
3. **Step 2:** Tap the "Choose File" button and select your downloaded WatchMeFly Task Sheet PDF.
4. **Step 3:** Review the map. The view will snap to your targets. If they are in the correct country/region, tap "Generate Text File (.txt)". 
5. Open OziExplorer, go to **Load** -> **Import Waypoints from Text File**, and select the generated file.

## Technical Details
* Uses `pdf.js` for strict client-side text extraction.
* Uses `proj4js` to dynamically compute true UTM grids from map coordinates and vice-versa.
* Uses `Leaflet.js` & `Leaflet-Control-Geocoder` with OpenStreetMap (Nominatim) for free, API-keyless interactive mapping and searching.

## Deployment on GitHub Pages
This app requires no backend server. 
1. Fork or clone this repository.
2. Go to your repository **Settings** -> **Pages**.
3. Under "Branch", select `main` and click **Save**.
4. Your site will be live within 60 seconds.
