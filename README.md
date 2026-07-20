# Mining Telemetry & Geotechnical Monitoring Platform

> **Enterprise field-data capture, telemetry, analytics, and geotechnical monitoring platform for underground mining operations.**
>
> Built with **Astro, React, Tailwind CSS, Supabase, Recharts, IndexedDB, ExcelJS and PWA technologies**.

![Status](https://img.shields.io/badge/Status-Production%20Project-success)
![Source](https://img.shields.io/badge/Source-Private-lightgrey)
![Platform](https://img.shields.io/badge/Platform-Web%20%2B%20PWA-blue)
![Domain](https://img.shields.io/badge/Domain-Mining%20Technology-orange)

> **Portfolio notice**  
> This repository is a public technical showcase of a private production project. Source code, credentials, internal operational data, proprietary documents, and sensitive infrastructure details are intentionally not included.
>
> The client/site is intentionally anonymized in this public version. Company or project branding should only be added if publication is authorized.

---

> 🖼️ **[PORTADA / HERO IMAGE]**  
> Suggested image: `assets/cover.png`  
> Recommended: full-width screenshot of the application home screen or module selector.

---

## Overview

This project is a modular telemetry and geotechnical monitoring platform designed for a real mining operational environment.

The platform centralizes field measurements, historical engineering data, analytics, geotechnical monitoring and reporting in a single web application. It was designed around a key operational challenge: **field personnel may work in areas with limited or no network connectivity**, while engineering and management teams require centralized, traceable and continuously updated information.

The system combines three main operational domains:

- **Hydraulic Flow Monitoring** — field capture and historical analysis of water-flow measurements.
- **2D Convergence Monitoring** — extensometric monitoring of tunnel deformation across multiple stations.
- **3D Convergence Monitoring (TLS / Surveying)** — spatial monitoring of tunnel deformation using 3D observations.

The result is a responsive platform that connects **mobile field workflows** with **desktop engineering dashboards**, while maintaining a centralized data layer and automated reporting capabilities.

---

## The Problem

Operational monitoring workflows in mining are often distributed across spreadsheets, manually maintained historical files, isolated field records and static reports.

This creates several challenges:

- Field measurements may be captured manually and later transcribed.
- Underground connectivity can be intermittent or unavailable.
- Historical datasets become difficult to explore and compare.
- Engineering calculations may be duplicated across spreadsheets and workflows.
- Traceability becomes harder when multiple people capture or modify information.
- Generating reports for engineering or management teams becomes repetitive.
- 2D and 3D monitoring datasets may live in separate files with different structures.

The goal of this project was to transform those disconnected workflows into a **modular digital monitoring platform**.

---

## The Solution

The application provides a centralized interface where field operators can capture measurements and engineering teams can analyze historical information through dedicated dashboards.

The platform was designed with a **feature-first modular architecture**, allowing each monitoring domain to evolve independently while sharing common infrastructure such as authentication, layout, database access and offline synchronization.

### Core capabilities

- Mobile-first field data capture.
- Desktop analytical dashboards.
- Offline measurement queue using IndexedDB.
- Automatic synchronization when connectivity returns.
- User authentication and access validation.
- Measurement traceability and audit metadata.
- Historical trend visualization.
- Engineering KPIs and alert states.
- Station-level drill-down analysis.
- PDF, PNG and Excel reporting.
- Clipboard export for tables and charts.
- Bulk report generation.
- Modular architecture for future monitoring domains.

---

> 🖼️ **[MODULE SELECTOR / HOME SCREEN]**  
> Suggested image: `assets/module-selector.png`

---

# Platform Modules

## 1. Hydraulic Flow Monitoring

The Flow Monitoring module digitizes the complete workflow for hydraulic measurements performed in the field.

An authenticated operator enters the measured **water velocity** and **water level** from a mobile device. The system looks up the corresponding cross-sectional area from a calibration dataset and automatically calculates the resulting flow rate.

The measurement is then stored in the centralized database together with traceability information.

### Main features

- Field measurement entry optimized for mobile devices.
- Automatic engineering calculation of flow rate.
- Real-time calculation preview before submission.
- Historical measurement database.
- Monthly aggregation and trend visualization.
- KPI cards for average, maximum and minimum flow.
- Drill-down from monthly summaries to individual measurements.
- Authenticated editing and deletion workflows.
- Measurement creator and timestamp traceability.
- Flexible filtering by year and month.
- Export to PNG, PDF and Excel.
- Configurable report content and visible columns.
- Copy tables directly to Word or Excel.
- Copy charts directly as images.

> 🖼️ **[FLOW DASHBOARD]**  
> Suggested image: `assets/flow-dashboard.png`  
> Show KPIs, monthly chart and historical table.

> 🖼️ **[FIELD DATA ENTRY — MOBILE]**  
> Suggested image: `assets/flow-mobile-entry.png`  
> Show the responsive mobile measurement form and real-time calculation preview.

---

## 2. 2D Tunnel Convergence Monitoring

The 2D Convergence module manages historical and new tunnel deformation measurements collected through extensometric monitoring stations.

The system provides a centralized view of monitored stations, historical trends and threshold-based alert states. Engineers can move from a high-level tunnel overview to an individual station and inspect measurements for each monitored chord.

### Main features

- Dashboard covering **86 monitoring stations**.
- More than **19,000 historical convergence measurements** managed in the platform.
- Station cards with current monitoring state.
- Threshold-based visual classification.
- Filtering by station status and measurement range.
- Station-level detail pages.
- Historical time-series visualization.
- Tunnel profile diagrams rendered with SVG.
- Per-chord monitoring and threshold comparison.
- Historical date selection.
- Navigation between monitoring stations.
- Field ingestion wizard for complete measurement sessions.
- Bulk insertion of measurements.
- Offline support for field sessions.
- Instrument certificate visualization.
- Summary and mass-export workflows.

The engineering calculation logic used by the module was implemented as reusable pure functions and validated against the existing historical dataset to ensure consistency with legacy results.

> 🖼️ **[2D CONVERGENCE DASHBOARD]**  
> Suggested image: `assets/convergence-2d-dashboard.png`  
> Show station cards, filters and alert states.

> 🖼️ **[2D STATION DETAIL]**  
> Suggested image: `assets/convergence-2d-station.png`  
> Show tunnel diagram, chord measurements and historical chart.

> 🖼️ **[2D FIELD INGESTION WIZARD]**  
> Suggested image: `assets/convergence-2d-ingestion.png`

---

## 3. 3D Convergence Monitoring — TLS / Surveying

A dedicated 3D convergence sub-module extends the platform to spatial tunnel monitoring workflows based on surveying observations and TLS-related datasets.

This module separates 3D monitoring from the extensometric 2D workflow while reusing the platform's shared authentication, layout and database infrastructure.

### Main features

- **10 dedicated 3D monitoring stations**.
- Approximately **21,000+ historical 3D measurement records**.
- Dashboard with station status and KPIs.
- Station-type filtering.
- Individual 3D station detail pages.
- Historical time-series analysis.
- Dynamic SVG tunnel diagrams.
- Paginated historical measurement tables.
- Support for station-specific monitoring configurations.
- Centralized database integration.

This separation allows 2D and 3D monitoring workflows to evolve independently without mixing their engineering logic or data models.

> 🖼️ **[3D CONVERGENCE DASHBOARD]**  
> Suggested image: `assets/convergence-3d-dashboard.png`

> 🖼️ **[3D STATION DETAIL]**  
> Suggested image: `assets/convergence-3d-station.png`

---

# Offline-First Field Workflow

One of the most important technical requirements was supporting measurements in underground areas where internet connectivity may be unavailable.

The application implements an offline workflow using a **Progressive Web App architecture, Service Worker caching and IndexedDB**.

```text
Field Operator
      │
      ▼
Mobile Web App / PWA
      │
      ├── Online ───────────────► Supabase
      │
      └── Offline
            │
            ▼
        IndexedDB Queue
            │
            │ Connectivity restored
            ▼
      Automatic Synchronization
            │
            ▼
          Supabase
```

### Offline workflow

1. The operator opens the application while connected.
2. Required application assets are cached by the Service Worker.
3. The operator enters the mine and loses connectivity.
4. Measurements continue to be captured normally.
5. Pending records are stored locally in IndexedDB.
6. The UI clearly indicates the number of pending measurements.
7. Once the device reconnects, the application automatically attempts synchronization.
8. Successfully synchronized measurements become available to the centralized dashboards.

This approach allows field workflows to continue without forcing operators to maintain parallel paper or spreadsheet processes solely because of connectivity limitations.

> 🖼️ **[OFFLINE MODE]**  
> Suggested image: `assets/offline-mode.png`  
> Show the offline banner and pending synchronization counter.

---

# High-Level Architecture

```text
┌──────────────────────────────────────────────────────────────┐
│                     Web Application                         │
│                 Astro + React + Tailwind                    │
└──────────────────────────────────────────────────────────────┘
                 │                         │
        Mobile Field Workflow      Desktop Engineering View
                 │                         │
                 ▼                         ▼
        ┌────────────────┐        ┌────────────────────┐
        │ Data Ingestion │        │ Analytics & KPIs   │
        │ Offline Queue  │        │ Charts & Drilldown │
        └────────────────┘        └────────────────────┘
                 │                         │
                 └────────────┬────────────┘
                              ▼
                  ┌──────────────────────┐
                  │      Supabase        │
                  │ Auth + PostgreSQL DB │
                  │ Views + RLS Policies │
                  └──────────────────────┘
                              │
             ┌────────────────┼─────────────────┐
             ▼                ▼                 ▼
      Flow Monitoring   Convergence 2D   Convergence 3D
             │                │                 │
             └────────────────┼─────────────────┘
                              ▼
                   Reports & Data Exports
                PDF · PNG · Excel · ZIP · Clipboard
```

> 🖼️ **[ARCHITECTURE DIAGRAM]**  
> Suggested image: `assets/architecture.png`  
> Replace the text diagram above with a polished architecture diagram if available.

---

# Technology Stack

| Layer | Technologies |
|---|---|
| Frontend | Astro, React |
| Styling | Tailwind CSS |
| Backend / Database | Supabase, PostgreSQL |
| Authentication | Supabase Auth |
| Data Visualization | Recharts, SVG |
| Offline Storage | IndexedDB |
| Offline Application | Service Worker, PWA Manifest |
| Reporting | ExcelJS, jsPDF, html-to-image |
| Data Exchange | Excel / XLSX, PNG, PDF, ZIP |
| Deployment | Vercel-compatible Astro deployment |
| Architecture | Feature-first modular structure |

---

# Engineering Highlights

## Modular feature-first architecture

The application is organized by business domain rather than by generic technical layer.

```text
src/
├── shared/
│   ├── components/
│   ├── config/
│   ├── lib/
│   └── styles/
│
├── modules/
│   ├── flow-monitoring/
│   ├── convergence-2d/
│   └── convergence-3d/
│
└── pages/
```

Each module owns its specific UI and engineering logic, while common functionality such as authentication, database access, layout and offline synchronization is shared.

This design makes it possible to add future monitoring modules without tightly coupling them to existing functionality.

---

## Centralized engineering logic

Engineering calculations are separated from presentation components and implemented as reusable functions.

This makes the calculations easier to:

- test,
- validate against historical datasets,
- reuse across forms and dashboards,
- maintain independently from the user interface.

For the 2D convergence workflow, calculation logic was cross-validated against **19,488 historical records with zero differences** during the validation process.

---

## Historical data migration

A significant part of the project involved transforming existing operational datasets into structured database tables suitable for real-time application workflows.

The platform currently manages datasets including:

| Dataset | Scale |
|---|---:|
| Hydraulic flow history | 1,200+ measurements |
| 2D convergence stations | 86 stations |
| 2D convergence history | 19,000+ measurements |
| 3D convergence stations | 10 stations |
| 3D convergence history | 21,000+ measurements |

> Figures represent a project snapshot and may continue to evolve as new field measurements are collected.

---

## Traceability and auditability

Measurements created through authenticated field workflows include metadata identifying the user and creation timestamp.

This provides a foundation for operational traceability and makes it possible to distinguish between historical imported data and measurements captured directly through the application.

---

## Reporting and interoperability

The platform was designed not only to visualize information but also to integrate with existing engineering reporting workflows.

Supported outputs include:

- Configurable PDF reports.
- High-resolution PNG reports.
- Multi-sheet Excel workbooks.
- Historical Excel exports with charts.
- Bulk station chart exports.
- ZIP packages for mass reporting.
- HTML/TSV clipboard tables for Word and Excel.
- PNG chart clipboard export for reports and presentations.

> 🖼️ **[REPORT EXPORT MODAL]**  
> Suggested image: `assets/report-export.png`

> 🖼️ **[EXPORTED REPORT EXAMPLE]**  
> Suggested image: `assets/report-example.png`

---

# User Experience Strategy

The platform intentionally separates two main usage contexts.

### Field operators

Optimized for mobile devices and fast data entry:

- Simple measurement forms.
- Real-time calculation previews.
- Offline operation.
- Clear synchronization status.
- Session-based measurement workflows.

### Engineering and management users

Optimized for desktop analysis:

- KPI dashboards.
- Historical charts.
- Filtering and drill-down.
- Station-level analysis.
- Report generation.
- Excel interoperability.

This allows a single platform to serve both operational data capture and higher-level technical analysis.

---

# Data Flow

```text
Measurement in Field
        │
        ▼
Validation + Engineering Calculation
        │
        ├── No Connection ──► IndexedDB Queue
        │                         │
        │                         └──► Auto-sync when online
        │
        ▼
Central PostgreSQL Database
        │
        ▼
Database Views / Aggregations
        │
        ├──► KPI Dashboards
        ├──► Historical Charts
        ├──► Station Detail
        └──► Reports & Excel Exports
```

---

# My Contribution

My work on this project covered the design and implementation of the platform across multiple layers:

- Application architecture and modularization.
- Frontend development with Astro and React.
- Responsive field and desktop user experiences.
- Supabase/PostgreSQL data architecture.
- Historical data migration and structuring.
- Authentication and access-control workflows.
- Offline-first field data capture.
- Engineering calculation implementation.
- Validation against historical datasets.
- Interactive dashboards and visualization.
- 2D and 3D convergence monitoring interfaces.
- Automated reporting and Excel generation.
- Data export and interoperability workflows.

The project required combining **software engineering, data engineering, surveying/geospatial knowledge and mining operational requirements** into a single production-oriented application.

---

# Key Challenges Solved

### Working without connectivity underground

Implemented a shared IndexedDB queue and automatic synchronization strategy that allows measurements to continue being captured offline.

### Migrating spreadsheet-based engineering history

Structured historical engineering datasets into relational tables while preserving compatibility with existing Excel-based operational workflows.

### Supporting different monitoring methodologies

Separated hydraulic, 2D convergence and 3D convergence logic into independent modules with shared infrastructure.

### Maintaining consistency with historical calculations

Isolated engineering formulas into reusable functions and validated results against legacy datasets.

### Generating professional engineering reports from the browser

Implemented configurable exports to Excel, PDF, PNG and clipboard formats directly from the application.

---

# Screenshots

A recommended gallery order for this portfolio repository:

### Application Home

> 🖼️ **[1 — PORTADA / MODULE SELECTOR]**

### Hydraulic Monitoring

> 🖼️ **[2 — FLOW DASHBOARD]**

> 🖼️ **[3 — MOBILE FIELD DATA ENTRY]**

> 🖼️ **[4 — REPORT EXPORT]**

### 2D Convergence

> 🖼️ **[5 — CONVERGENCE DASHBOARD]**

> 🖼️ **[6 — STATION DETAIL]**

> 🖼️ **[7 — FIELD INGESTION WIZARD]**

### 3D Convergence / TLS

> 🖼️ **[8 — 3D DASHBOARD]**

> 🖼️ **[9 — 3D STATION DETAIL]**

### Offline Workflow

> 🖼️ **[10 — OFFLINE MODE / PENDING SYNC]**

---

# Public Repository Structure

Since this repository is intended as a portfolio showcase rather than the production source repository, a simple structure is recommended:

```text
mining-telemetry-platform-showcase/
│
├── README.md
│
├── assets/
│   ├── cover.png
│   ├── module-selector.png
│   ├── flow-dashboard.png
│   ├── flow-mobile-entry.png
│   ├── offline-mode.png
│   ├── convergence-2d-dashboard.png
│   ├── convergence-2d-station.png
│   ├── convergence-2d-ingestion.png
│   ├── convergence-3d-dashboard.png
│   ├── convergence-3d-station.png
│   ├── report-export.png
│   ├── report-example.png
│   └── architecture.png
│
└── docs/
    └── architecture-overview.md
```

---

# Source Code Availability

The production source code is maintained in a private repository because the project contains proprietary business logic, internal integrations and operational information.

This public repository focuses on:

- the engineering problem,
- the solution architecture,
- technical decisions,
- implemented capabilities,
- screenshots and visual demonstrations,
- and the overall project impact.

No production credentials, confidential datasets or internal configuration files are included.

---

# Project Status

**Production-oriented / actively evolved**

The platform has progressed from a hydraulic monitoring dashboard into a broader modular mining telemetry system incorporating field data capture, offline synchronization, 2D geotechnical convergence monitoring, 3D/TLS monitoring and automated reporting.

---

## Author

**Tito Ruiz**  
Geospatial Engineer · Mining Technology · GeoAI · Software Development

[GitHub](https://github.com/YOUR_USERNAME) · [LinkedIn](https://www.linkedin.com/in/YOUR_PROFILE)

---

> **Note:** Replace the placeholder images, GitHub username and LinkedIn profile before publishing. Add company or client branding only when you have explicit authorization to make it public.
