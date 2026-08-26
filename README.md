Weather App

A minimal, single-file weather app built with vanilla HTML, CSS, and JavaScript. Searches any city worldwide and displays current conditions alongside a 5-day forecast, powered by the OpenWeatherMap API.

Preview

Cream-and-black design — typographic temperature hero, monospaced data stats, 5-day forecast strip with today highlighted.

Features
Current temperature, feels-like, and weather condition
4-stat grid — humidity, wind speed, visibility, pressure
5-day forecast strip with daily high/low and condition icons
Today's forecast card inverted for quick at-a-glance reading
Inline error handling for unknown cities
Keyboard support — press Enter to search
Responsive down to mobile (420px max-width)
Zero dependencies — one .html file, no build step
Getting Started
1. Get an API key

Sign up for a free account at openweathermap.org. The free tier covers both endpoints used here (/weather and /forecast).

Note: New API keys can take up to 2 hours to activate.

2. Add your key

Open weather-app.html and find this line near the top of the <script> block:

js
const API_KEY = 'YOUR_OPENWEATHERMAP_API_KEY';

Replace YOUR_OPENWEATHERMAP_API_KEY with your actual key.

3. Open in a browser
bash
open weather-app.html
# or just double-click the file

No server required. Works directly from the filesystem.

API Endpoints Used
Endpoint	Purpose
GET /data/2.5/weather	Current conditions — temp, humidity, wind, visibility, pressure
GET /data/2.5/forecast	3-hour forecast slots (40 entries) used to build the 5-day strip

Both calls are made in parallel via Promise.all to keep load time fast.

The forecast groups entries by day and picks the slot closest to noon as the representative reading. High/low per day are derived from all available slots for that day.

Design Tokens

The UI is driven by a two-colour CSS custom property system — no framework, no utility classes.

Token	Value	Role
--cream	
#F2ECD8	Page background, primary surface
--cream-mid	
#E8E1CC	Input background, forecast cards
--cream-deep	
#D5CEBD	Borders, dividers, grid gaps
--ink	
#080808	Primary text, button fill, focus ring
--ink-soft	
#2A2A2A	Button hover state
--ink-muted	
#888070	Country tag, condition label, stat units
--ink-faint	
#B8B0A0	Placeholders, feels-like, low forecast temps

Typography: DM Sans (UI) and DM Mono (numeric data) — both loaded from Google Fonts.

File Structure
weather-app.html   ← everything: markup, styles, and script in one file
README.md
Extending

Add °F toggle — convert cur.main.temp client-side rather than changing the API units param, so you don't need a second request.

Geolocation — call navigator.geolocation.getCurrentPosition on load and hit /weather?lat=&lon= instead of ?q=.

Hourly chart — the /forecast response already returns 40 three-hour slots; feed them into a <canvas> chart for an hourly breakdown.

Dark mode — invert the token values under @media (prefers-color-scheme: dark).

License

MIT
