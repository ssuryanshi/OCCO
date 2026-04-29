# OCCO — Real-Time RFID Vehicle Tracking System

> **Summer Internship Project — Indian Army (Pine Eagles) | 2025**
> Built and presented as part of a summer internship with the Indian Army. This system replaces the legacy Python/XAMPP prototype with a secure, scalable, full-stack solution for real-time military vehicle monitoring.

---

## Team

Developed by a team of five interns:

- Disha Jain
- Shourya Mishra
- Rahul Agarwal
- **Suryanshi Singh**
- Arinjay Jain

---

## The Problem

Design and develop a secure, real-time military vehicle tracking system with a robust backend and an intuitive frontend. The system must replace the existing Python/XAMPP prototype with a scalable architecture that supports:

- Automated RFID-based checkpoint tracking
- Alert generation for missed or delayed scans
- Encrypted data handling
- Real-time visualizations through a user-friendly interface

The previous implementation lacked a secure and scalable architecture to support these critical functionalities, hindering its effectiveness and reliability in high-security operational environments.

---

## Our Solution

A secure, real-time RFID-based military vehicle tracking system built on a structured SQL backend and an interactive Next.js frontend. The system automates checkpoint tracking, detects missed or delayed scans, and visualizes vehicle movement through an intuitive dashboard. Data is securely stored and transmitted. The system is designed for deployment on secure infrastructure with support for data syncing from locally cached scans in offline environments.

---

## Key Features

### Real-Time RFID Tracking
- Live vehicle feed with 3-second polling intervals
- Per-lane status indicators (active / maintenance / blocked)
- Search by RFID tag, BA number, unit name, or checkpoint ID
- Pause/resume live stream without losing history

### Lane Visualization
- Visual map of 4 lanes (L1–L4), each with 10 checkpoints
- Vehicle category differentiation (Category A / Category B)
- Click-to-inspect vehicle detail popups with speed and checkpoint position

### Data Visualisation Charts
- Lane-wise traffic distribution (pie chart)
- Vehicle type breakdown (Type A / Type B)
- Per-lane vehicles-per-checkpoint bar charts (L1, L2, L3)
- Auto-refreshes every 10 seconds from the Flask analytics service

### Checkpoint-wise Movement Logs
- Full timestamped movement history per vehicle
- Logs include: RFID, BA number, unit, formation, lane, checkpoint, purpose

### Scan History and Filtering of Vehicles
- Filter logs by unit, formation, vehicle type, purpose, and lane
- Multi-field search across all movement records

### Vehicle Path Simulation
- Simulate vehicle movement across checkpoints for testing and demonstration

### Interactive Dashboard
- Unified tabbed interface with refresh controls and live status indicators
- Excel data upload for batch ingestion of scan logs
- Built-in database health monitor, tester, and debug panel

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Next.js 15, React 19, TypeScript |
| UI Components | Radix UI, shadcn/ui, Tailwind CSS |
| Charts | Recharts |
| Backend API | Next.js API Routes + Flask (Python) |
| Database | MySQL (`occo_db`) |
| Data Ingestion | `xlsx` (Excel parsing), `mysql2` |

---

## Architecture

```
Browser (Next.js Frontend)
        |
        |--- /api/*          (Next.js API Routes — DB queries via mysql2)
        |--- localhost:8000  (Flask service — Excel ingestion + analytics endpoints)
                |
                +--- MySQL: occo_db
                        |
                        +--- Vehicle_Details  (RFID, BA_NO, Type, Unit, Formation, Purpose)
                        +--- logs             (rfid, cpid, timestamp)
                        +--- checkpoints      (cpid, lane)
```

### Database Schema (Summary)

| Table | Key Columns |
|---|---|
| `Vehicle_Details` | `rfid`, `BA_NO`, `Type_of_Veh`, `Unit`, `Formation`, `Lane`, `No_of_Trps`, `Purpose` |
| `logs` | `rfid`, `cpid`, `timestamp` |
| `checkpoints` | `cpid`, `lane` |

---

## Getting Started

### Prerequisites

- Node.js 18+
- Python 3.9+ with Flask
- MySQL server with `occo_db` database

### 1. Install frontend dependencies

```bash
npm install
```

### 2. Configure MySQL

Update the database credentials in the API route files to match your local MySQL setup:

```ts
const dbConfig = {
  host: "localhost",
  user: "root",
  password: "<your_password>",
  database: "occo_db",
}
```

### 3. Start the Flask backend

```bash
python app.py
# Runs on http://localhost:8000
```

### 4. Start the Next.js frontend

```bash
npm run dev
# Runs on http://localhost:3000
```

---

## Dashboard Tabs

| Tab | Purpose |
|---|---|
| **Upload Data** | Upload `.xlsx` RFID log files for batch ingestion |
| **Overview** | Lane visualization + traffic distribution side by side |
| **Analytics** | Full analytics charts — lane, type, and per-lane bar charts |
| **Filter Logs** | Query movement logs with advanced filters |
| **Live Tracking** | Real-time vehicle feed with search and lane filter |
| **Database Test** | Verify database connectivity and record counts |
| **Debug** | Raw debug panel for data inspection |

---

## APM Highlights

This system applies Application Performance Monitoring (APM) principles to physical asset tracking in a military context:

- **Availability monitoring** — database connection health checked every 5 seconds with live status indicator
- **Real-time data pipelines** — 3s live tracking refresh, 10s analytics refresh
- **Structured logging** — all vehicle movements are timestamped and associated with checkpoint and lane metadata
- **Graceful degradation** — Preview Mode with mock data activates automatically if the database is unreachable, ensuring the UI remains functional
- **Missed-scan detection** — architecture supports flagging of vehicles that fail to register at expected checkpoints
- **Observability** — dedicated debug and database test panels for full operational transparency

---

## Future Goals

- Enable data transfer via **WiMax** for remote/field connectivity
- Introduce **predictive analytics** for route and delay forecasting
- Enable **downloadable audit trails** and system logs
- Ensure **secure data backup** and hardened storage mechanisms

---

## Project Context

This project was developed and presented during a **Summer Internship with the Indian Army (Pine Eagles) in 2025**. The goal was to build a practical, deployable monitoring tool that digitizes RFID-based vehicle movement logging at a military establishment, replacing the existing Python/XAMPP prototype with a production-ready system. The platform handles real operational data including vehicle BA numbers, unit and formation codes, troop counts, and movement purpose classifications — sourced directly from the Army's existing RFID infrastructure.

---

## Author

**Suryanshi Singh**
Summer Intern — Indian Army, 2025
