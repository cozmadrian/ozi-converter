# WatchMeFly Universal OziExplorer (.wpt) Converter

A purely client-side, mobile-responsive web application designed for Hot Air Balloon competition pilots. It extracts truncated UTM coordinates (e.g., `5484/2762` or `0396-9349`) and target altitudes from WatchMeFly PDF task sheets, mathematically reconstructs them based on the geographical region, and generates a timestamped `.wpt` file using strict OziExplorer spacing and datetime formatting.

## Features
* **Space-Tolerant Coordinate Extraction (NEW):** Prioritizes coordinate discovery even when PDF rendering engines corrupt the formatting. The algorithm scans the document for any `XXXX/YYYY`, `XXXX-YYYY`, `XXXX.YYYY`, and smoothly ignores invisible spaces artificially injected by the PDF font kerning (e.g., extracting `83 10 / 3475` perfectly as `8310/3475`).
* **Live Coordinate Debugging Logger (NEW):** Features a live terminal interface that outputs every single target detected, printing the raw text it read, its X/Y coordinates on the physical PDF page, and which task it mathematically bound the coordinate to.
* **True 2D Spatial Association Engine:** Abandons flawed left-to-right text reading. It now physically maps the X/Y location of every character on the page. When a coordinate is found, the engine calculates which Task Name is physically directly *above* it within its specific column, ensuring targets are never stolen by adjacent tasks in complex multi-column layouts.
* **Language-Agnostic CIA Rule Engine:** Task identification relies primarily on the universal CIA Sporting Code rule numbers (`15.1` for PDG, `15.15` for MDD, etc.). This makes the tool fully functional regardless of the language used on the task sheet.
* **Isolated Target Numbering:** Separates global file indexing from individual task targeting. If Task 19 has multiple coordinates, they will be elegantly named `T19_HWZ_P1`, `T19_HWZ_P2`, and `T19_HWZ_P3`.
* **Column-Isolated Altitude Extraction:** Applies 2D spatial filtering to altitude discovery, ensuring feet/FT numbers are safely bound to their respective coordinates.
* **Strict Template Output:** Generates native `.wpt` files in Decimal Degrees (WGS84). Calculates real-time OziExplorer epoch timestamps (Days since Dec 30, 1899) and precisely mimics spacing/formatting required by legacy and modern navigation hardware.
* **100% Offline Processing:** Once loaded, the page processes PDFs entirely within the browser. No files are uploaded to any server. 

## How to use (For Pilots)
1. Open the [Web App URL] in your browser (Chrome/Safari).
2. **Step 1:** Use the map's search bar (magnifying glass icon) to find your competition city, OR simply click on the map. The system will automatically calculate your UTM Zone and prefixes (the digits omitted by the competition director). You can also edit these manually if needed.
3. **Step 2:** Tap the "Choose File" button and select your downloaded WatchMeFly Task Sheet PDF.
4. **Step 3:** Review the map and the debug log. The view will snap to your targets and display their intelligently generated names (e.g., `T21_PDG_P1`) and altitudes automatically. If everything is correct, tap "Generate Waypoints (.wpt)". 
5. Open OziExplorer and load the newly generated `.wpt` file directly.

## Technical Details
* Uses `pdf.js` for strict client-side text extraction.
* Uses `proj4js` to dynamically compute true UTM grids from map coordinates and convert them mathematically to WGS84 Decimal Degrees.
* Uses `Leaflet.js` & `Leaflet-Control-Geocoder` with OpenStreetMap (Nominatim) for free, API-keyless interactive mapping and searching.

## Deployment on GitHub Pages
This app requires no backend server. 
1. Fork or clone this repository.
2. Go to your repository **Settings** -> **Pages**.
3. Under "Branch", select `main` and click **Save**.
4. Your site will be live within 60 seconds.
