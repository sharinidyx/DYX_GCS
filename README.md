# DYX-GCS Mobile

A Ground Control Station (GCS) mobile application for controlling and monitoring autonomous rovers in real-time. Built with React Native and Expo.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Running the App](#running-the-app)
- [Connecting to the Rover](#connecting-to-the-rover)
- [App Screens](#app-screens)
- [Environment Configuration](#environment-configuration)

---

## Prerequisites

Before running the app, make sure you have the following installed:

- **Node.js** (v18 or above) — [Download](https://nodejs.org)
- **npm** (comes with Node.js)
- **Expo Go** app on your Android/iOS device — install from Play Store or App Store
- The **DYX rover backend** running and accessible on the same network

---

## Installation

```bash
# 1. Clone the repository
git clone https://github.com/sharinidyx/DYX_GCS.git
cd DYX_GCS

# 2. Install dependencies
npm install
```

---

## Running the App

```bash
# Start the development server
npm start
```

A QR code will appear in the terminal. Scan it with:
- **Android** — Expo Go app
- **iPhone** — Camera app (then tap the banner)

### Other run options

```bash
npm run android    # Run on connected Android device or emulator
npm run ios        # Run on iOS simulator (Mac only)
npm run web        # Run in browser
```

---

## Connecting to the Rover

1. Ensure your phone and the rover backend are on the **same Wi-Fi network**
2. Open the app → go to the **Rover Discovery** tab (last icon)
3. Enter the backend IP and port (default: `http://192.168.1.102:5001`)
4. Tap **Connect** — the status indicator will turn green when connected

> The app will automatically try fallback IPs if the primary connection fails.

---

## App Screens

### 1. Dashboard
- Shows vehicle **armed/disarmed** status, flight mode, and system health
- Displays **live GPS position**, altitude, and RTK fix type
- Connection status indicator at the top

### 2. Marking Plan (Path Plan)
Used to plan the rover's mission before sending it.

| Action | How |
|---|---|
| Add waypoint | Tap on the map |
| Draw a survey grid | Use the grid tool in the toolbar |
| Draw a circle pattern | Use the circle tool |
| Reorder waypoints | Drag in the waypoint sidebar |
| Set failsafe mode | Tap the failsafe selector (Strict / Relax) |
| Import waypoints | Tap Import → select a file |
| Export waypoints | Tap Export → share/save |
| Start mission | Tap **Start Mission** in the ops panel |

### 3. Mission Progress (Mission Report)
Monitors the rover during an active mission.

| Feature | Description |
|---|---|
| Waypoint table | Shows each waypoint with live status (Pending / Active / Done) |
| Distance display | Real-time distance to the current waypoint (Karney geodesic algorithm) |
| Mission map | Live rover position overlaid on the mission path |
| Mission controls | Start / Pause / Resume / Stop |
| RTK Injection | Configure NTRIP profile for RTK corrections |
| Export report | Download mission log as Excel file |

### 4. Mission Analytics
- View charts and graphs from completed missions
- Analyse historical performance metrics

### 5. Telemetry
- Raw live telemetry data streamed from the rover
- Useful for debugging and monitoring sensor values

### 6. Rover Discovery
- Manage backend connection
- Set or change the backend IP/URL at runtime
- Test connectivity

---

## Environment Configuration

Create a `.env` file in the project root (copy from `.env.example`):

```env
# Backend URLs (optional — can also be set in the app UI)
EXPO_PUBLIC_ROS_HTTP_BASE=http://192.168.1.102:5001
EXPO_PUBLIC_ROS_WS_URL=ws://192.168.1.102:5001/socket.io
```

> The backend URL can also be changed at runtime from the **Rover Discovery** screen without restarting the app.

---

## Tech Stack

| Area | Technology |
|---|---|
| Framework | React Native + Expo |
| Language | TypeScript |
| Navigation | React Navigation (Bottom Tabs) |
| Maps | react-native-maps |
| Real-time | Socket.IO |
| HTTP | Axios |
| Geodesic math | geographiclib (Karney algorithm) |
| Export | ExcelJS |
| State | React Context + AsyncStorage |

---

## Team Notes

- Always make sure the **rover backend is running** before opening the app
- The app persists the last used backend IP — you don't need to re-enter it every session
- If the map doesn't load waypoints, try **pull-to-refresh** on the Mission Progress screen
- For RTK accuracy, configure the NTRIP profile in Mission Progress → RTK Injection before starting a mission
- Mission logs can be exported as `.xlsx` from the Mission Progress screen after a mission ends
