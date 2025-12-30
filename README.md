# 🌊 Global Wave & Weather Buoy Data Visualization

A real-time visualization of global wave data and weather buoy measurements on an interactive map.

## Features

- **Real NOAA Buoy Data**: Displays real-time data from NOAA's National Data Buoy Center
  - Wave heights
  - Wind speed and direction
  - Air and water temperatures
  - Atmospheric pressure
  - Updated hourly from active buoys

- **Global Wave Forecasts**: Shows current wave conditions worldwide using NOAA WaveWatch III Global Wave Model
  - Significant wave heights (combined wind waves and swell)
  - Primary wave direction
  - Primary wave mean period
  - 20+ locations around the globe
  - Data from government-operated numerical wave model

- **Interactive Map**: Built with Leaflet.js
  - Color-coded markers based on wave height
  - Detailed popups with all measurements
  - Toggle between buoys, waves, or both
  - Auto-refresh every 5 minutes

- **Live Statistics**: Real-time dashboard showing:
  - Number of active buoys
  - Maximum wave height
  - Average wave height
  - Total data points

## Data Sources

This project uses 100% real data from U.S. Government public domain sources:

1. **[NOAA National Data Buoy Center (NDBC)](https://www.ndbc.noaa.gov/)** - Real-time weather buoy measurements
2. **[NOAA WaveWatch III](https://polar.ncep.noaa.gov/waves/wavewatch/)** - Global wave model forecasts via ERDDAP API

## How It Works

The application:
1. Fetches the list of active NOAA buoys from `activestations.xml`
2. Retrieves real-time data for ~60 buoys from NDBC with geographic distribution across Pacific, Atlantic, and other regions
3. **Wave data loads instantly** from pre-fetched JSON updated every 3 hours via GitHub Actions
4. Displays all data on an interactive map with color-coded markers
5. Auto-refreshes buoy data every 5 minutes

### Automated Data Updates

Wave forecast data is automatically updated every 3 hours using GitHub Actions:
- Workflow fetches latest data from NOAA WaveWatch III ERDDAP
- Saves to `data/wave-data.json`
- Commits and pushes to repository
- Page loads this pre-fetched data instantly (no CORS proxy needed!)
- Manual workflow trigger available in GitHub Actions tab

## API Endpoints Used

- **NOAA NDBC Active Stations**: `https://www.ndbc.noaa.gov/activestations.xml`
- **NOAA NDBC Real-time Data**: `https://www.ndbc.noaa.gov/data/realtime2/{station_id}.txt`
- **NOAA WaveWatch III ERDDAP**: `https://coastwatch.pfeg.noaa.gov/erddap/griddap/NWW3_Global_Best.json`
  - Fetched every 3 hours via GitHub Actions
  - Pre-cached in `data/wave-data.json` for instant loading

## Wave Height Color Legend

- 🟢 **Green**: 0-1m (Calm)
- 🟡 **Yellow**: 1-2m (Light)
- 🟠 **Orange**: 2-4m (Moderate)
- 🔴 **Red-Orange**: 4-6m (Rough)
- 🔴 **Red**: 6m+ (Very Rough)

## Usage

Simply open the page and the data will load automatically. Use the controls to:
- **Data Layer**: Choose to view NOAA Buoys, Wave Heights, or Both
- **Refresh Data**: Manually refresh the data at any time
- Click on any marker to see detailed information

## Technical Stack

- **Frontend**: HTML5, CSS3, JavaScript (Vanilla)
- **Mapping**: Leaflet.js
- **Data APIs**:
  - NOAA NDBC Real-time Data (via CORS proxy)
  - NOAA WaveWatch III via ERDDAP (pre-fetched)
- **Automation**: GitHub Actions (scheduled data updates)
- **Deployment**: GitHub Pages

## License

This project visualizes public domain data from NOAA (National Oceanic and Atmospheric Administration). All NOAA data is in the U.S. public domain and freely available for use.

## Credits

Data provided by:
- NOAA National Data Buoy Center (NDBC)
- NOAA National Weather Service - Marine Modeling and Analysis Branch (WaveWatch III)
- NOAA CoastWatch ERDDAP Server
- OpenStreetMap contributors (map tiles)
