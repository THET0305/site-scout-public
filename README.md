# SiteScout

**Turn cold outreach into data-backed, visual, persuasive sales conversations.**

SiteScout is an agentic AI-powered lead generation platform designed for web developers and agencies. It doesn't just find busines websites; it **audits** them, identifies technical and visual flaws, and generates professional redesign pitches automatically.

**RESPECTS `robots.txt`**

---

## Demo Video

video/SiteScoutDemo.mp4

---

## Core Capabilities

### Smart Lead Discovery
Scans businesses within a 1-50 mile radius of any ZIP code. 
- **Google Places**: High-fidelity live data.
- **OpenStreetMap**: Community-driven open data.
- **Mock Provider**: Instant testing without API keys.

### High-Fidelity Capture
Automatically visits every lead's website to capture:
- **Visual Snapshots**: Full-page Desktop and Mobile screenshots.
- **Technical DNA**: Raw HTML analysis for outdated coding patterns.

### Two-Layer Scoring System
SiteScout ranks leads from **Most Outdated** to **Most Modern**:
1.  **Heuristics**: Deterministic checks for HTTPS, mobile viewports, table layouts, and legacy JS libraries.
2.  **AI Vision**: Real visual analysis of screenshots to detect poor whitespace, "dated" aesthetics, and UX friction.

### Automated Pitch Generation
Generates professional, non-aggressive emails tailored to specific business pain points found during the audit.

---

## How the "Agentic AI" Works

SiteScout goes beyond simple prompts. It follows a bounded reasoning loop:
1.  **Gather Evidence**: Fetches HTML and takes screenshots.
2.  **Extract Signals**: Runs 10+ heuristic checks.
3.  **Evaluate**: An AI Auditor reviews the screenshots and heuristic data.
4.  **Decide**: It determines the severity of the redesign need and adjusts the score.
5.  **Act**: It writes a personalized pitch and presents the "Visual Evidence" to you.

---

## System Optimizations

SiteScout is engineered for speed and politeness:

-   **Concurrency Control**: Uses an `asyncio.Semaphore` to limit concurrent browser instances (default: 3), preventing CPU/Memory spikes.
-   **Async-First DNA**: Built on FastAPI and HTTPX for non-blocking I/O across the entire pipeline.
-   **Resilient Retries**: Integrated with exponential backoff and multi-server rotation (for OSM/Overpass) to handle transient network issues or API timeouts gracefully.
-   **Intelligent Loading**: Playwright is configured to wait for `domcontentloaded` rather than full heavy assets, speeding up the capture phase.
-   **Efficient AI**: Supports "Lite" model variants (e.g., Llama 3.2 1B) and lightweight vision models (Moondream) for faster local inference.
-   **Rate Limiting**: Built-in adherence to provider constraints and `robots.txt` compliance to ensure ethical scanning and avoid IP bans.

---

## User Interfaces

| UI | Best For | Technical Note |
| :--- | :--- | :--- |
| **Gradio Dashboard** | Prototyping & Quick Scans | `pdm run python app.py` |
| **React Dashboard** | Production-ready Experience | `npm run dev` in `/frontend` |

---

## Setup & Requirements

### Prerequisites
- **Python 3.11+**
- **Node.js 18+** (for React UI)
- **Ollama**: Required for AI. Install from [ollama.com](https://ollama.com).
    - *Note: SiteScout will automatically pull missing models (llama3.2, llava, etc.) when you start a scan.*

### Environment Variables (`local.env`)
- `GOOGLE_PLACES_API_KEY`: For Google provider.
- `SITE_SCOUT_PROVIDER`: Default provider (mock, google_places, overpass).
- `SITE_SCOUT_STORAGE_DIR`: Output directory (default: `./scout_output`).

---

## Tech Stack

- **Backend**: FastAPI, Playwright, BeautifulSoup4, Pydantic V2
- **AI Engine**: Ollama (Llama 3.2, LLaVA)
- **Frontend**: React 19, Vite, Tailwind CSS (Glassmorphism design)
- **Geo**: pgeocode (Offline ZIP conversion)

---

## Project Status

- [x] **v0.1.0 Core**: Multi-provider search, high-res capture, and AI audit.
- [x] **Interactivity**: Expanded Detail Modal with visual evidence.
- [x] **Auto-Setup**: Automated model pulling and path verification.
- [ ] **TBA**: Mock Redesign Generator (HTML concepts).
- [ ] **TBA**: PDF Proposal Automation.

---

## Legal & Usage

*SiteScout is a personal project intended for educational and portfolio use. Any reuse, modification, or deployment of this code is done at your own risk and responsibility.*
*Users are responsible for ensuring compliance with all applicable laws and with target websites’ `robots.txt` and Terms of Service. Misuse of this project, including aggressive scraping or abusive automation, is strongly discouraged.*

