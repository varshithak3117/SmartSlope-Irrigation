# SmartSlope – Smart Irrigation Management System for Sloping Arecanut Plantations

**SmartSlope** is a modern, responsive, precision agriculture platform designed specifically for managing irrigation across multiple sloping agricultural lands, with special optimization for **sloping arecanut (betel nut) plantations**.

---

## 🌾 The Problem: Sloping Agricultural Land & Gravity

On sloping plantations, water naturally flows downhill due to gravity:
- **Upper Slope (Zone 1)** dries rapidly due to high sunlight, gravity drainage, and thin topsoil crust, leading to severe moisture stress.
- **Middle Slope (Zone 2)** experiences moderate infiltration.
- **Lower Slope (Zone 3)** accumulates downhill water and silt, leading to waterlogging, nutrient saturation, and deadly fungal root rot (*Phytophthora meadii* / Koleroga disease).
- **Surface Runoff:** Over-irrigation on slopes causes fertile topsoil erosion, fertilizer leaching, and massive water wastage (up to 40% lost in traditional flood irrigation).

**SmartSlope solves this problem** by dividing every registered land into three independently monitored and actuated zones, detecting surface runoff, synchronizing with Open-Meteo rain forecasts, and empowering farmers with Kannada voice alerts.

---

## 🚀 Key Features

### 1. Multi-Land Management (Dynamic 2+ Fields)
- Register any number of fields (comes pre-seeded with 3 realistic arecanut estates: Sringeri, Thirthahalli, and Sirsi).
- Fields can be added, edited, inspected, and removed after confirmation.
- **Automatic 3-Zone Creation:** Adding a new land automatically initializes Zone 1 (Upper), Zone 2 (Middle), and Zone 3 (Lower).
- Each land operates with completely isolated telemetry, valve controls, water meters, and safety thresholds.

### 2. Three-Zone Independent Monitoring
Every land displays three dedicated zone cards:
- **Zone 1 – Upper Slope:** Monitors crest soil moisture %, valve status, dry conditions, and runoff risks.
- **Zone 2 – Middle Slope:** Monitors central terrace moisture and controls drip laterals independently.
- **Zone 3 – Lower Slope:** Monitors valley basin moisture, prevents water accumulation, and blocks pumping if saturation occurs.
- Displays soil moisture %, status (Dry, Normal, Wet), valve status (Open/Closed), irrigation status (Running/Paused/Stopped), runoff status, soil temperature, and last update timestamp.
- Direct manual controls: **Start**, **Pause**, and **Stop** buttons with immediate response.

### 3. Slope Cross-Section Interactive Diagram
- Visual 2.5D elevation cross-section showing hill gradient from +18m elevation down to the 0m valley basin.
- Illustrates gravitational downflow, sub-surface seepage, and drainage contour trenches.

### 4. Automatic Irrigation & Runoff Safety System
- Intelligent moisture threshold control: Starts when soil dries below configured threshold; stops when target moisture is reached.
- **Runoff Emergency Interlock:** If surface runoff is detected:
  1. Valve immediately closes within milliseconds.
  2. Audible voice alert sounds in Kannada and English.
  3. Visual critical warning banner is displayed identifying the land and zone.
  4. Irrigation is locked out until infiltration soak completes or farmer manually clears the lock.
- Safety cutoffs for sensor timeouts, communication loss, and max run durations.

### 5. Weather Forecast Integration (Open-Meteo API)
- Real-time weather data retrieved for each land's geographic coordinates in Karnataka.
- Displays temperature, humidity, wind speed, rain probability %, and expected precipitation (mm).
- **Smart Weather Irrigation Advisor:** Automatically recommends delaying irrigation by 18–24 hours when heavy rainfall is forecasted, saving thousands of liters of reservoir water.
- Graceful offline fallback if network is interrupted.

### 6. Kannada & English Voice Alerts (ಧ್ವನಿ ಎಚ್ಚರಿಕೆಗಳು)
- Uses Web SpeechSynthesis API to speak alerts aloud to farmers:
  - *“ಭೂಮಿ 1, ವಲಯ 1 ರಲ್ಲಿ ಮಣ್ಣಿನ ತೇವಾಂಶ ಕಡಿಮೆಯಾಗಿದೆ.”*
  - *“ಭೂಮಿ 2 ರಲ್ಲಿ ನೀರು ಹರಿದುಹೋಗುವಿಕೆ ಪತ್ತೆಯಾಗಿದೆ. ನೀರಾವರಿಯನ್ನು ನಿಲ್ಲಿಸಲಾಗಿದೆ.”*
  - *“ಮಳೆ ಮುನ್ಸೂಚನೆ ಇದೆ. ನೀರಾವರಿ ಅಗತ್ಯವನ್ನು ಪರಿಶೀಲಿಸಿ.”*
- Language toggle between **ಕನ್ನಡ (Kannada)** and **English**.
- Voice toggle (Enable/Mute) and interactive **Test Alert** button.
- Floating visual subtitle banner ensures alerts are visible on devices without native Kannada TTS engines.

### 7. Water Usage Analytics & CSV Export
- Interactive charts powered by **Chart.js**:
  - 24-Hour & 7-Day Soil Moisture Trends across Zone 1, 2, and 3.
  - Water consumption breakdown per zone (Liters).
  - Water conservation ratio: SmartSlope vs traditional slope flooding baseline (~41% water saved).
- One-click **Export CSV Log** button generating complete spreadsheets of timestamps, land names, zones, water applied, and trigger reasons.

### 8. Rule-Based Smart Recommendations
- Identifies the exact land and zone, explains agronomic reasons, and suggests actionable solutions (e.g. adjust upper drip emitter, delay for rain, clear lower drainage trench).

### 9. Interactive Hardware Simulator (Demo Mode) & ESP32 Gateway
- **Demo Mode:** Physical slope simulation running directly in the browser. Models real gravitational percolation, solar evaporation, and interactive buttons to inject runoff or drought events.
- **ESP32 Gateway Mode:** Connects to real field microcontrollers via REST API (`POST /api/telemetry`, `GET /api/control/:landId`).

---

## 📂 Project Structure

```
SmartSlope/
├── index.html                 # Complete responsive Single Page Application
├── css/
│   └── styles.css             # High-end agricultural design system & animations
├── js/
│   ├── config.js              # Initial plantation seeds, districts, constants
│   ├── voice.js               # Kannada & English SpeechSynthesis engine & subtitles
│   ├── weather.js             # Open-Meteo weather API integration & rain advisor
│   ├── irrigation.js          # Slope-aware irrigation logic & runoff safety locks
│   ├── analytics.js           # Chart.js graphs, water savings math, CSV export
│   ├── simulator.js           # Live demo simulator (gravity flow, runoff injection)
│   └── app.js                 # UI controllers, multi-land CRUD, recommendations
├── server.js                  # Node.js Express backend & persistent REST API
├── package.json               # Backend dependencies
├── esp32/
│   ├── esp32_smartslope.ino   # Production-ready Arduino C++ sketch for ESP32
│   └── WIRING_GUIDE.md        # Complete schematic, pinout, and solar wiring guide
└── README.md                  # System documentation
```

---

## ⚡ How to Run

### Option 1: Direct Browser Launch (Zero Installation)
Simply double-click or open `index.html` in any modern web browser (Google Chrome, Microsoft Edge, Mozilla Firefox, or Safari).
- All features run client-side with persistent storage (`localStorage`).
- Demo mode simulator immediately activates.
- Open-Meteo weather and Kannada/English voice alerts work out of the box.

### Option 2: Running with Node.js Express Backend
1. Ensure Node.js is installed.
2. Open a terminal in this directory.
3. Install dependencies:
   ```bash
   npm install
   ```
4. Start the backend server:
   ```bash
   npm start
   ```
5. Open your browser at `http://localhost:3000`.

---

## 🔌 Hardware Setup (ESP32)

To connect real hardware in an arecanut plantation:
1. Open `esp32/esp32_smartslope.ino` in Arduino IDE.
2. Enter your plantation Wi-Fi credentials and server IP address.
3. Flash to an ESP32 board.
4. Follow `esp32/WIRING_GUIDE.md` for pin connections:
   - **GPIO 34:** Zone 1 Upper Soil Moisture Sensor
   - **GPIO 35:** Zone 2 Middle Soil Moisture Sensor
   - **GPIO 32:** Zone 3 Lower Soil Moisture Sensor
   - **GPIO 33:** Surface Runoff Sensor
   - **GPIO 25, 26, 27:** 12V Solenoid Valve Relays (Zones 1, 2, 3)

---

## 🛡️ License
MIT License. Developed for smart agricultural water conservation.
