<div align="center">

<img src="public/flowcrm-logo.svg" width="112" height="112" alt="FlowCRM Logo" />

# FlowCRM

**A fast, modern visual CRM and sales pipeline platform built for high-velocity teams.**

Track leads, move deals across customizable stages, manage accounts, collaborate on tasks, and export boardroom-ready PDF reports — powered by React 19, TypeScript, and Supabase.

<p align="center">
  <a href="https://github.com/Anirudh1017/FlowCRM/releases"><img src="https://img.shields.io/badge/version-1.0.0-blue.svg" alt="Version 1.0.0" /></a>
  <a href="./LICENSE"><img src="https://img.shields.io/badge/license-MIT-5e6ad2.svg" alt="License: MIT" /></a>
  <a href="https://react.dev/"><img src="https://img.shields.io/badge/React-19.2-61dafb.svg?logo=react&logoColor=black" alt="React 19" /></a>
  <a href="https://www.typescriptlang.org/"><img src="https://img.shields.io/badge/TypeScript-5.9-3178c6.svg?logo=typescript&logoColor=white" alt="TypeScript" /></a>
  <a href="https://vite.dev/"><img src="https://img.shields.io/badge/Vite-7.3-646cff.svg?logo=vite&logoColor=white" alt="Vite" /></a>
  <a href="https://supabase.com/"><img src="https://img.shields.io/badge/Supabase-PostgreSQL%20%26%20Auth-3ecf8e.svg?logo=supabase&logoColor=white" alt="Supabase" /></a>
  <a href="https://dndkit.com/"><img src="https://img.shields.io/badge/@dnd--kit-Drag%20%26%20Drop-E11D48.svg" alt="dnd-kit" /></a>
</p>

</div>

---

## Overview

**FlowCRM** is a full-featured customer relationship management and visual sales pipeline application designed to bring order, speed, and clarity to your sales cycle. Built as a modern Software Construction project, FlowCRM replaces cluttered spreadsheets and rigid legacy tools with a fluid, dark-themed SaaS workspace that teams actually enjoy using.

Everything from lead qualification to won contracts is managed through an interactive drag-and-drop Kanban board, supported by unified company and contact directories, activity timelines, task queues, instant global search, and client-side PDF reporting.

FlowCRM is backed by **Supabase** for secure authentication and real-time PostgreSQL persistence, with zero-latency optimistic state updates and comprehensive local CSV import capabilities.

> **New here?** Check out the [**Getting Started guide**](#getting-started) to set up your environment, connect your Supabase database, and import sample leads in under 3 minutes.

---

## Contents

- [Features](#features)
  - [Visual Kanban Pipeline](#visual-kanban-pipeline)
  - [Lead Intelligence & Bulk Actions](#lead-intelligence--bulk-actions)
  - [Companies & Accounts Directory](#companies--accounts-directory)
  - [Contacts Management](#contacts-management)
  - [Task Engine & Activity Timeline](#task-engine--activity-timeline)
  - [Executive Dashboard & PDF Reporting](#executive-dashboard--pdf-reporting)
  - [Global Search Palette](#global-search-palette)
  - [Customizable Pipeline Settings](#customizable-pipeline-settings)
- [How It Works](#how-it-works)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Configuration](#environment-configuration)
  - [Running the App](#running-the-app)
  - [Importing Sample Data](#importing-sample-data)
- [Available Scripts](#available-scripts)
- [Production Build & Deployment](#production-build--deployment)
- [Security & Authentication](#security--authentication)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## Features

### Visual Kanban Pipeline
- **Smooth Drag-and-Drop**: Built on `@dnd-kit/core` and `@dnd-kit/sortable` with hardware-accelerated pointer sensors, drop overlays, and collision detection.
- **Dynamic Stages**: Out-of-the-box stages (`New Lead` &rarr; `Contacted` &rarr; `Qualified` &rarr; `Proposal` &rarr; `Won` &rarr; `Lost`) with stage-specific color accents and deal counters.
- **Stage Metrics**: Instantly see total deal counts and aggregated financial pipeline values for each column.
- **Granular Filters**: Filter the active board by stage, custom tag, or deal value brackets (Under $5k, $5k–$25k, $25k+).
- **Direct Lead Creation**: Add deals straight into any column or open the rich editing modal.

### Lead Intelligence & Bulk Actions
- **Rich Lead Profiles**: Track lead name, email, phone, company affiliation, job title, expected deal value, stage, custom tags, and notes.
- **Bulk Operations**: Multi-select leads with batch selection toggles to bulk-delete or organize deals in seconds.
- **CSV Import**: Upload any `.csv` file (such as the included `sample-leads.csv`) to parse and populate dozens of leads automatically.
- **Instant Filtering**: Real-time debounce searching across lead names, contact emails, and company titles.
- **Avatar Badges**: Dynamically computed initials and color hashes for every lead.

### Companies & Accounts Directory
- **Organization Hierarchy**: Centralized database of accounts with domain names, industry verticals, company size, headquarters address, phone, and direct website links.
- **Linked Deals**: Automatically queries and surfaces all active leads associated with each company.
- **Full CRUD Support**: Add, update, and remove companies with confirmation modals.

### Contacts Management
- **Individual Directory**: Store and reference individual points of contact, their direct phone numbers, email addresses, and positions.
- **Linked Organization**: Map contacts directly to parent companies for cross-functional relationship mapping.

### Task Engine & Activity Timeline
- **Priority-Coded Tasks**: Manage follow-ups and deliverables with `Low`, `Medium`, and `High` priority tags.
- **Interactive Checklists**: One-click completion toggles, smart date sorting, and filter views for `All`, `Pending`, and `Completed`.
- **Activity Stream**: Log and review historical interactions across deals including calls, emails, notes, meetings, and completed milestones.

### Executive Dashboard & PDF Reporting
- **High-Level KPIs**: Real-time calculation of Total Leads, Cumulative Pipeline Value, Win / Conversion Rate (%), and Active Open Deals.
- **Recent Activity Feed**: Chronological log of recent lead movements and team interactions.
- **Client-Side PDF Generator**: Export professional executive summaries using `jspdf` (`flowcrm-report.pdf`) with breakdown metrics and timestamps ready for stakeholders.

### Global Search Palette
- **Unified Querying**: Universal search input in the header that filters leads, companies, and tags concurrently.
- **Contextual Results**: Instant dropdown previewing matching leads and organizations with keyboard-friendly dismissals.

### Customizable Pipeline Settings
- **Drag-and-Drop Stage Reordering**: Customize your team's sales stages by renaming labels, altering stage colors, or rearranging column order with `@dnd-kit`.
- **Persistent Preferences**: Sidebar collapse states and custom stage arrangements are synced directly to Supabase.

---

## How It Works

FlowCRM coordinates an asynchronous React 19 client with Supabase's PostgreSQL backend, using optimistic UI patterns so your workflow never stutters.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           Client Architecture                           │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   React 19 + TypeScript + Vite SPA                                      │
│   ├── UI Layer: Framer Motion (Transitions) + Lucide Icons + CSS Modules│
│   ├── State Layer: AuthContext ── CRMContext ── SearchContext           │
│   └── Interaction: @dnd-kit (Kanban DND) + jsPDF (PDF Reporting)       │
│                                                                         │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                             REST / Realtime API
                                     │
┌────────────────────────────────────▼────────────────────────────────────┐
│                         Supabase Cloud Backend                          │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   ├── Auth Service: Email / Password Auth & Session Tokens              │
│   └── PostgreSQL Database:                                              │
│       ├── leads          (Deals, stages, values, tags, notes)           │
│       ├── companies      (Organizations, industries, domains)           │
│       ├── contacts       (Individual points of contact)                 │
│       ├── tasks          (Priorities, due dates, completions)           │
│       ├── activities     (Calls, emails, meetings, timeline)            │
│       └── settings       (User preferences & pipeline stage configs)    │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Frontend Framework** | [React 19](https://react.dev/) | Component architecture, hooks, and responsive state rendering |
| **Language** | [TypeScript 5.9](https://www.typescriptlang.org/) | End-to-end type safety, strict interface models, and refactoring security |
| **Build Tool & Bundler** | [Vite 7](https://vite.dev/) | Sub-second Hot Module Replacement (HMR) and optimized Rollup builds |
| **Routing** | [React Router v7](https://reactrouter.com/) | Declarative routing, protected route guards, and URL parameters |
| **Backend & Database** | [Supabase](https://supabase.com/) | Managed PostgreSQL, Row Level Security, and user authentication |
| **Drag and Drop** | [@dnd-kit](https://dndkit.com/) | Accessible, high-performance drag-and-drop for Kanban and settings |
| **Animations** | [Framer Motion 12](https://www.framer.com/motion/) | Smooth layout animations, modal transitions, and micro-interactions |
| **Icons** | [Lucide React](https://lucide.dev/) | Clean, consistent SVG iconography |
| **PDF Generation** | [jsPDF 4.2](https://github.com/parallax/jsPDF) | Vector PDF document generation for executive pipeline reports |
| **ID Generation** | [UUID v13](https://github.com/uuidjs/uuid) | RFC4122 compliant unique identifiers for entities |
| **Styling** | Vanilla CSS Modules | Scoped component styling with dark-mode SaaS variables |

---

## Project Structure

```
FlowCRM/
├── index.html                     # HTML5 entrypoint with FlowCRM branding
├── package.json                   # Project dependencies and script runner
├── tsconfig.json                  # TypeScript compiler settings
├── vite.config.ts                 # Vite bundler configuration
├── sample-leads.csv               # Ready-to-import sample dataset
├── public/
│   ├── flowcrm-logo.svg           # High-resolution vector logo
│   └── landing/                   # Standalone product landing page
│       ├── index.html
│       ├── styles.css
│       └── script.js
└── src/
    ├── main.tsx                   # React root mount
    ├── App.tsx                    # Route definitions and auth wrapper
    ├── index.css                  # Global tokens, resets, and dark theme
    ├── types/
    │   └── index.ts               # Core domain models (Lead, Company, Task, etc.)
    ├── lib/
    │   └── supabase.ts            # Supabase client singleton
    ├── store/
    │   ├── AuthContext.tsx        # Session state, login, and sign-up handlers
    │   ├── CRMContext.tsx         # Central store for CRUD operations & Supabase sync
    │   └── SearchContext.tsx      # Global search and query filter provider
    ├── components/
    │   ├── Layout.tsx             # Application shell with responsive sidebar
    │   ├── Sidebar.tsx            # Navigation sidebar with collapsible state
    │   ├── KanbanBoard.tsx        # Drag-and-drop sales pipeline columns
    │   ├── LeadCard.tsx           # Draggable lead deal card
    │   ├── LeadModal.tsx          # Lead creation & editing form
    │   ├── GlobalSearch.tsx       # Search bar with instant typeahead dropdown
    │   ├── Modal.tsx              # Reusable animated modal container
    │   └── DeleteModal.tsx        # Danger confirmation dialog
    ├── pages/
    │   ├── Dashboard.tsx          # Executive overview & performance KPIs
    │   ├── Pipeline.tsx           # Kanban sales board with advanced filters
    │   ├── Leads.tsx              # Leads table, multi-select, and CSV import
    │   ├── Companies.tsx          # Accounts & organization directory
    │   ├── Contacts.tsx           # Contact directory & details
    │   ├── Tasks.tsx              # Task lists & priority management
    │   ├── Reports.tsx            # Analytics, conversion rates, and PDF export
    │   ├── Settings.tsx           # Stage customization & workspace preferences
    │   ├── Login.tsx              # Authentication portal (Sign in / Sign up)
    │   └── Landing.tsx            # Product showcase iframe bridge
    └── utils/
        └── index.ts               # Currency, date, initials, and CSV parsers
```

---

## Database Schema

FlowCRM relies on relational PostgreSQL tables configured with Supabase:

| Table | Primary Key | Key Attributes | Notes |
|---|---|---|---|
| `leads` | `id` (UUID) | `name`, `email`, `phone`, `company_id`, `position`, `value`, `stage`, `tags`, `notes` | Foreign key `company_id` links to `companies` |
| `companies` | `id` (UUID) | `name`, `domain`, `industry`, `size`, `address`, `phone`, `website` | Tracks organization attributes |
| `contacts` | `id` (UUID) | `name`, `email`, `phone`, `company_id`, `position`, `notes` | Mapped to parent organizations |
| `tasks` | `id` (UUID) | `title`, `description`, `lead_id`, `contact_id`, `due_date`, `completed`, `priority` | Linked to specific leads and contacts |
| `activities` | `id` (UUID) | `type`, `title`, `description`, `lead_id`, `contact_id`, `company_id` | Historical interaction logs |
| `settings` | `id` (UUID) | `user_id`, `sidebar_collapsed`, `pipeline_stages` (JSONB) | Saves user preferences & stage layout |

---

## Getting Started

### Prerequisites

Make sure you have the following installed on your machine:
- **Node.js** (v18.0.0 or higher recommended)
- **npm** (v9.0.0+) or **pnpm** / **yarn**
- A **Supabase** account (Free tier works perfectly)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Anirudh1017/FlowCRM.git
   cd FlowCRM
   ```

2. **Install project dependencies:**
   ```bash
   npm install
   ```

### Environment Configuration

Create a `.env` file in the root of the project using `.env.example` as a template:

```bash
cp .env.example .env
```

Open `.env` and fill in your Supabase credentials:

```ini
VITE_SUPABASE_URL=https://your-project-ref.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-public-key-here
```

> **Note:** Both variables are prefixed with `VITE_` so that Vite safely exposes them to the client bundle at build time.

### Running the App

Start the local Vite development server:

```bash
npm run dev
```

Navigate to `http://localhost:5173` in your browser.

- Sign up for a new account (or sign in if an account exists).
- You will be greeted by the executive dashboard with full access to all CRM tools.

### Importing Sample Data

To test the application immediately with realistic data:
1. Navigate to the **Leads** page (`/leads`) in the sidebar.
2. Click the **Import CSV** button in the header toolbar.
3. Select or upload the included `sample-leads.csv` file from the project root.
4. Your leads will immediately populate the table and sync across the **Pipeline**, **Dashboard**, and **Reports**.

---

## Available Scripts

| Command | Description |
|---|---|
| `npm run dev` | Launches the local Vite development server with Hot Module Replacement |
| `npm run build` | Runs TypeScript compilation (`tsc -b`) and bundles production assets into `dist/` |
| `npm run preview` | Spins up a local server to preview the built `dist/` production assets |
| `npm run lint` | Runs ESLint 9 across all TypeScript and React files |

---

## Production Build & Deployment

To produce an optimized production build:

```bash
npm run build
```

The compiled assets will be output to the `dist/` folder.

### Deploying to Vercel
1. Push your repository to GitHub.
2. Import the project into [Vercel](https://vercel.com).
3. Set the Framework Preset to **Vite**.
4. In **Environment Variables**, add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`.
5. Deploy!

### Deploying to Netlify
1. Connect your repository to [Netlify](https://netlify.com).
2. Set Build command to `npm run build` and Publish directory to `dist`.
3. Add a `_redirects` file with `/*  /index.html  200` to support client-side routing.
4. Add your environment variables under Site settings &rarr; Environment variables.

---

## Security & Authentication

- **Authentication Flow**: Managed via Supabase Auth with secure JWT tokens stored in browser local storage.
- **Row Level Security (RLS)**: PostgreSQL policies isolate user configurations (`settings`) to the authenticated `user_id`.
- **Environment Isolation**: Private service keys are never exposed in frontend code; only public anon keys are used with restricted database permissions.

---

## Troubleshooting

**The app gets stuck on the loading spinner after sign-in.**
Verify that your Supabase instance is active and that your `.env` contains the exact URL and anon key matching your project. Open Developer Tools (F12) &rarr; Console to check for network connection errors.

**CSV import does not parse my custom file.**
Ensure your CSV headers match the required structure:
`name,email,phone,company,position,value,stage,tags,notes`
If an optional field is missing, leave the column empty between commas.

**Dragging cards does not drop into a column.**
Make sure you are hovering over the droppable column container until the highlighted border appears before releasing the cursor.

**Report export fails to download.**
Check your browser's download permissions. jsPDF generates `flowcrm-report.pdf` directly in memory and triggers a native download prompt.

---

## License

[MIT](LICENSE) &copy; 2026 Sanirudh ([sanirudh17](https://github.com/sanirudh17)) & Anirudh ([Anirudh1017](https://github.com/Anirudh1017))

Built with [React](https://react.dev/), [Vite](https://vitejs.dev/), [Supabase](https://supabase.com/), [@dnd-kit](https://dndkit.com/), [Framer Motion](https://www.framer.com/motion/), [jsPDF](https://github.com/parallax/jsPDF), and [Lucide Icons](https://lucide.dev/).
