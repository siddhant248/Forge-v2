# FORGE — Project Planning & Execution Copilot

**AI Engineering Track · Team FORGE: Aditya Raj, Jai Prakash, Sidhant**

> **AI reads. Rules decide. Physics validates. Every number has verifiable proof.**

---

## ⚡ Executive Summary

Building physical robotics and embedded systems is notoriously fragmented and error-prone. Engineering teams and makers face scattered component datasheets, inconsistent vendor nomenclature (e.g. an "Arduino Nano" search returning ₹229 clones and ₹2,755 original boards on the same storefront), hidden costs (deceptive EMI monthly installments, shipping fees, out-of-stock items), and catastrophic electrical mismatches (voltage spikes, logic-level incompatibilities, insufficient motor driver current).

**FORGE** is an autonomous, end-to-end **Project Planning & Execution Copilot** that bridges the gap between high-level project ideation and verified hardware reality. It guides builders from initial skill discovery and resume analysis all the way to deterministic BOM generation, real-time market sourcing, electrical compatibility checking, physics-based component swapping, wiring diagrams, starter firmware generation, and automated live cart verification.

---

## 🌟 Key Capabilities

### 1. 🎯 Intelligent Discovery & Needs Matching
- **Interactive 9-Question Survey**: Evaluates career trajectory, experience level, programming languages, time commitment, budget (INR), available tools, existing hardware, project goals, and interest domains.
- **Resume / CV Evidence Extractor**: Ingests PDF, DOCX, or plain text resumes. Powered by Google Gemini with **mandatory exact quote verification**—every extracted skill, tool, or past project must link to verbatim text in the resume and requires explicit user confirmation.
- **Career Market Research**: Connects with TinyFish Search + Fetch to discover real-time industry and dream-job requirements (e.g., autonomous systems, ROS2, embedded perception).
- **12-Factor Deterministic Matcher**: Filters by hard constraints (budget, schedule, tooling) and scores compatibility across 12 deterministic criteria. Includes an interactive **Radial Fit Profile** chart.

### 2. 🏆 Competition Strategy & Shortlisting ("Build to Compete")
- Catalog of **18 competition-tailored builds** across **14 major robotics events** (RoboCup, Robocon, Line Maze, Combat Robotics, Formula Student, Autonomous Drone Racing, etc.).
- Outlines event constraints, safety considerations, estimated build hours, and parts availability index for the Indian market.
- **Direct 1-Click Planning & BOM Hand-off**:
  - Every competition project card features a direct **`⚡ Plan & Build BOM`** action button.
  - Instantly transitions from competition discovery to **Stage 4 (Planning & Execution)**, pre-loading the bot's complete architecture (10–15 parts), target budget, live vendor sourcing, What-If hardware optimizer, and pinout wiring diagram.
  - Seamlessly bridges competition requirements with immediate physical BOM execution—no manual searching or re-entry required.

### 3. ✦ Curated Star Projects
- **20 team-curated builds** spanning autonomous robotics, advanced control, FPGA, embedded Linux, power electronics, and more, stored separately in `core/project_data/star_projects.csv`.
- Search each project by name, domain, skills, or prerequisites; expand project cards to review tools, safety notes, effort, and estimated cost.
- Star-project cards are a curated discovery catalog and do not imply that every project has a ready-to-generate BOM.
- Star-catalog costs are rough estimates, not quotes. Prices for the QDD arm, CubeSat flatsat, and imitation-learning arm are withheld pending vendor-price verification.

### 4. 🧠 Hybrid Architecture Planning & BOM Generation
- **Pre-Verified Catalog (168 Projects)**: Comprehensive component lists across 16 robotics disciplines, drafted with engineering notes, quantities, and vendor search queries.
- **Deterministic Rule-Checked Builds**: 3 core robotic baselines (Line Follower, Obstacle Avoider, Bluetooth Mobile Robot) tested against thousands of combinatorial combinations across Microcontroller, Motor Driver, Motors, Battery, and Sensors.
- **Autonomous Ideation Copilot (Gemini + TinyFish)**: Free-text project ideation ("a solar-powered field rover with 4 mecanum wheels") resolves through a priority hierarchy:
  1. Previously learned & saved builds (free, instant)
  2. Exact catalog project match
  3. Deterministic keyword routing
  4. Similar catalog project suggestions
  5. Single structured Gemini call (cached permanently in `learned_projects.json` for zero-cost repeat access).

### 5. 🛒 Real-Time Market Sourcing & Evidence Ledger
- **Live Vendor Scraping**: Direct search and page extraction across major Indian component distributors (Robu.in, Robocraze, Sunrobotics, ElectronicsComp, Robokits, etc.).
- **Rules First, LLM Last**: Heuristic regex engine (`core/pagerules.py`) extracts prices, titles, and availability without consuming LLM tokens. Gemini serves as a strictly capped fallback and requires that the exact price digits exist inside the cited quote.
- **Anti-Fraud & Deception Filters**:
  - Automatically identifies and excludes EMI / installment pricing (e.g., "starts at ₹86/mo").
  - Rejects price ranges, accessory bundles, and shipping threshold text.
  - Clone vs. Original detection flags genuine boards priced differently than generic alternatives.
  - Flags suspiciously low prices with warnings (`UNUSUALLY LOW · CHECK`).
- **Cryptographic Evidence Ledger**: Auditable table with CSV export logging verification status, shop URL, UTC timestamp, extraction technique, and verbatim quote proof.

### 6. 🔬 Project Optimizer (What-If Hardware Swap Engine)
- **Multi-Metric Physics & Electrical Impact Simulation**: Swap any component (MCU, driver, motor, battery, sensor) and immediately see real-world impacts on:
  - **Speed & Torque**: RPM, stall torque, linear speed (m/s), wheel pushing force.
  - **Power & Runtime**: Standby vs peak current, battery discharge rates, operating minutes.
  - **Electrical Safety**: Logic level differences (e.g., 3.3V vs 5V level shifting), VIN tolerances, motor driver current limits.
  - **Compute & I/O**: Clock speed, RAM, Flash, ADC/PWM channels, and spare GPIO pins.
- **Atomic Swap State Management (`core/kept.py`)**: "Keep this replacement" commits the swap directly into the active bill, totals, and PDF export without cross-contaminating other catalog builds.

### 7. 📊 Part Specs & Side-by-Side Comparison
- **Part specs · typical datasheet values, best value in green when comparing**:
  - Curated, typed engineering specifications for all 231 parts in the library (`core/part_specs.py`), detailing supply voltages, logic levels, peak/stall currents, clock/memory, torque, range, and accuracy.
  - **Compare with other microcontrollers / motor drivers / sensors**: Put any component side-by-side against similar alternatives from the library. The best value in each spec row is highlighted in **green** (only where "better" is clearly defined, e.g. lower voltage dropout, higher clock speed, longer range, or lower price).

### 8. 🔌 Wiring & Firmware Studio
- **Dynamic Wiring Guide**: Visual pin-to-pin schematic, Mermaid-rendered device and signal map, and a pinout table generated from the active BOM.
- **Logic Level Warnings**: Proactively highlights missing level shifters, pull-up resistors, and power decoupling.
- **Starter Firmware Synthesis**: Generates ready-to-flash C++/Arduino or MicroPython code configured with the exact pinouts and sensors in the active BOM.
- **Wokwi starter bundle**: Download `diagram.json`, `sketch.ino`, and `wiring.mmd` for the active build. Import the files into a Wokwi project and start the simulation there; FORGE cannot create a project in your Wokwi account or start its remote simulator from the browser.

### 9. 🔬 Research What This Project Needs
- **Research what this project needs · Search + Fetch (free)**:
  - Discovers real-world build guides, open-source hardware projects, and tutorials using TinyFish **Search + Fetch** (free API, no quota used).
  - Extracts the exact components used in published guides accompanied by verbatim supporting quotes, allowing users to validate community-tested parts against the generated BOM.

### 10. 🚚 Delivery Optimizer & Cart Check
- **Vendor Consolidation**: Analyzes supplier distribution to minimize split shipments and reduce delivery costs.
- **Cart check · TinyFish Browser for robu.in and robocraze.com, Web Agent for other shops**:
  - **TinyFish Browser for robu.in and robocraze.com**: Automated cloud browser driven by Playwright with a fixed, deterministic script (opt-in, consumes zero agent step credits). Targets only the main product's own Add-to-Cart button with strict stock inspection, preventing false clicks on out-of-stock related items, and reads the real shop cart total.
  - **Web Agent for other shops**: Autonomous web agent that navigates arbitrary third-party storefronts or handles browser fallbacks with strict safety instructions (capped at 12 steps and 180 seconds, read-only, never log in, never enter payment details).

### 11. 📄 Audit & Export
- Interactive on-screen invoice with manual override controls and unverified price adjustments.
- Clean PDF bill of materials export with native Indian Rupee (`₹`) symbol formatting.

### 🌐 TinyFish API & Cost Breakdown
| Feature | TinyFish API | Cost / Quota |
|---|---|---|
| **Sourcing**: Find real vendor pages for each BOM component | **Search** | Free |
| **Price & Spec Reading**: Extract live page text and proof quotes | **Fetch** | Free |
| **Research what this project needs**: Discover build guides & listed parts with quotes | **Search + Fetch** | Free |
| **Cart check (robu.in & robocraze.com)**: Open listing, add to cart, compare cart total | **Browser** (Playwright Cloud Browser) | Free (no agent steps) |
| **Cart check (other shops & browser fallback)**: Autonomous store navigation | **Web Agent** | Step credits, capped & opt-in |
| **Career & Market Research**: Research role & industry requirements | **Search + Fetch** | Free |


---

## 🏛️ System Architecture

```
forge/
├── app.py                      # Local development launcher for the web application
├── server/                     # FastAPI backend and API routes
├── web/                        # Vanilla HTML, CSS, and JavaScript frontend
│
├── core/                       # Core engine & deterministic logic
│   ├── auto_fix.py             # 1-Click auto-fix engine for budget & compatibility violations
│   ├── bill.py                 # Invoice calculation, tax rules, and PDF generator
│   ├── browser_cart.py         # Dual-engine cart verification (Playwright Cloud Browser + Agent)
│   ├── cart_check.py           # Verified cart comparison utilities
│   ├── combination_store.py    # Evaluated hardware combinations cache
│   ├── compatibility_engine.py # Hardware rule validation (PASS / FAIL / UNKNOWN)
│   ├── component_catalog.py    # Curated component database
│   ├── custom_bom.py           # Gemini architecture decomposition for new ideas
│   ├── data.py                 # Baseline catalog, extras, and baseline robot builds
│   ├── delivery_optimizer.py   # Supplier consolidation & shipping optimizer
│   ├── engineering_calculations.py # Physical formulas (torque, velocity, runtime, power)
│   ├── firmware.py             # Automated starter firmware synthesizer (C++ / Arduino)
│   ├── hybrid_bom.py           # Hybrid resolution pipeline (Catalog -> Rules -> Gemini)
│   ├── impact.py               # First-order physics impact formulas for component swaps
│   ├── kept.py                 # Atomic session manager for kept optimizer replacements
│   ├── ledger.py               # Verifiable evidence ledger with formula injection protection
│   ├── optimizer.py            # Component swap recommendation & ranking engine
│   ├── pagerules.py            # High-precision regex page parser (price, title, EMI filter)
│   ├── part_specs.py           # Typed engineering specifications for 231 parts
│   ├── picker.py               # 12-factor deterministic survey matcher & normalizer
│   ├── pipeline.py             # Core pipeline connecting rules, TinyFish, and Gemini
│   ├── profile_fill.py         # Fallback part profile generator & validator
│   ├── profiles.py             # Part profile data loader and atomic store
│   ├── project_store.py        # Project catalog indexing and learned plan store
│   ├── recommendation_catalog.py # Recommendation dataset parser
│   ├── research.py             # Web guide research engine using TinyFish
│   ├── resume.py               # Resume text extraction (PDF/DOCX/TXT) & quote verification
│   ├── rules.py                # Deterministic electrical rules engine
│   ├── specification_validator.py # Empirical spec validator
│   ├── specs.py                # Datasheet vs. live vendor spec comparison
│   ├── swap_dataset.py         # Part swap impact database
│   ├── tf.py                   # TinyFish SDK wrapper (Search, Fetch, Cache)
│   ├── wiring.py               # Pinout mapping & logic-level checking engine
│   └── project_data/           # Catalogs (168 projects, 14 competition events)
│
├── scripts/                    # Offline dataset builders & validation tools
├── tests/                      # 300+ offline pytest test suite
└── requirements.txt            # Pinned dependencies
```

---

## 🛠️ Installation & Setup

### Prerequisites
- Python 3.11 or 3.12 (Python 3.12 recommended)
- Git

### Quickstart

1. **Clone the repository**:
   ```bash
   git clone https://github.com/jhony1122f/BuilderBot.git
   cd BuilderBot
   ```

2. **Create and activate a virtual environment**:
   ```bash
   python -m venv .venv
   # Linux/macOS:
   source .venv/bin/activate
   # Windows PowerShell:
   .\.venv\Scripts\Activate.ps1
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**:
   ```bash
   cp .env.example .env
   ```
   Edit `.env` to include your API keys:
   ```env
   # Live market sourcing & cloud browser (https://agent.tinyfish.ai)
   TINYFISH_API_KEY=your_tinyfish_key_here

   # Architecture planning fallback & resume analysis (https://aistudio.google.com/apikey)
   GEMINI_API_KEY=your_gemini_key_here
   ```
   > **Note**: FORGE operates gracefully in offline/mock mode even without API keys by using seeded catalogs and stored benchmarks.

5. **Run the automated test suite**:
   ```bash
   PYTHONPATH=. pytest
   ```

6. **Launch the application**:
   ```bash
   python app.py
   ```
   FORGE serves its vanilla HTML/CSS/JavaScript interface and FastAPI endpoints at
   `http://127.0.0.1:8000`. For development, run `uvicorn server.main:app --reload`.

---

## 🛡️ Engineering Guardrails & Verifiability

| Guardrail | Implementation |
|---|---|
| **AI Reads, Rules Decide** | LLMs are restricted to parsing and naming. Deterministic formulas validate electrical voltage, current draw, and pricing math. |
| **Strict Quote Checking** | A price from any web page is accepted **only if the exact figure appears in the extracted quote**. |
| **Anti-EMI / Anti-Deception** | Regex filters discard EMI per month (e.g., "₹86/mo"), multi-pack totals, and delivery threshold numbers. |
| **Clone vs Original Audit** | Distinguishes between generic clones and genuine OEM boards, preventing skewed budget comparisons. |
| **Formula Injection Defense** | All values written to the Evidence Ledger and CSV exports are sanitized against spreadsheet formula injection (`=`, `+`, `-`, `@`). |
| **Isolated Optimizer State** | Component swaps remain isolated to the target build (`core/kept.py`), preventing unwanted state leaks into other builds. |
| **Sandboxed Cart Verification** | The Playwright cloud browser runs a fixed script targeting only the primary product's Add-to-Cart button. The Web Agent is strictly instructed never to check out or enter user credentials. |

---

## 👥 Team

**Team FORGE — Azinhack 2026**
- **Aditya Raj**
- **Jai Prakash**
- **Sidhant**
- **Aaryan giri**

---

## 📜 License & Acknowledgements

- Built for the **Azinhack 2026 AI Engineering Track**.
- Uses **TinyFish API** for web search, page extraction, cloud browser automation, and agentic validation.
- Powered by Google **Gemini 3.8 Flash** for structured evidence extraction and project synthesis.
- Includes **DejaVu Sans Font** (Bitstream Vera License) for PDF generation with rupee symbol support.
