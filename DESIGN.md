# Mission 2K38 Design System: Tactical Cockpit Noir

> **Single Source of Truth for Mission 2K38 Frontend Architecture, Google Stitch Screen Generation, and Elite Sports Vision UI.**

---

## 1. Visual Theme & Atmosphere

Mission 2K38 fuses **tactical football operations** with **aerospace-grade telemetry**. The aesthetic embodies an elite European club tactical video suite (think Manchester City analytics bunker or UEFA Champions League VAR hub) combined with state-of-the-art sports science laboratory precision.

### Aesthetic Spectrum
* **Atmospheric Mood:** Clinical, disciplined, high-agency, dark-mode intelligence.
* **Density Index:** `7.5 / 10` (Cockpit Dense) — compact data readouts, monospaced velocity readouts, spatial pitch coordinates, and live vector streams balanced by generous outer margins.
* **Variance Index:** `6.0 / 10` (Offset Asymmetric) — 7-column primary tactical playback paired with a 5-column spatial homography intelligence unit.
* **Motion Intensity:** `6.0 / 10` (Tactile Spring Motion) — continuous pulse pings on active pipeline states, smooth tab switching, and hardware-accelerated transforms.

---

## 2. Color Palette & Functional Roles

```
┌───────────────────────────┬──────────────┬─────────────────────────────────────────────────┐
│ Token Name                │ Hex / OKLCH  │ Functional Role                                 │
├───────────────────────────┼──────────────┼─────────────────────────────────────────────────┤
│ Void Obsidian             │ #050507      │ Deep viewport canvas & background backdrop      │
│ Cockpit Charcoal          │ #121214      │ Primary container cards, modal bodies           │
│ Inset Console Noir        │ #0A0A0C      │ Embedded terminal drawers, pitch radar canvases │
│ Pitch Turf Dark           │ #0A120C      │ 2D tactical pitch radar field background        │
│ Whisper Border            │ rgba(255,255,255,0.06) │ Structural card boundaries & grid borders│
│ Inset Highlight           │ rgba(255,255,255,0.05) │ Top-edge rim lighting for cards (depth) │
├───────────────────────────┼──────────────┼─────────────────────────────────────────────────┤
│ Trophy Gold (Primary)     │ #FACC15      │ Primary active state, key velocity callouts     │
│ Gold Accent Dark          │ #E5B842      │ Focus rings, slider buttons, active tabs        │
│ Pitch Emerald             │ #10B981      │ Calibrated states, homography locked, success   │
│ MediaPipe Cyber Cyan      │ #00F0FF      │ 33-point skeletal bones, kinematic angle arcs   │
│ Neon Joint Green          │ #00FF66      │ Skeletal joint vertices, low-latency nodes      │
│ Team 1 Royal Blue         │ #3B82F6      │ Team 1 roster nodes, possession bar left half   │
│ Team 2 Crimson Amber      │ #EF4444      │ Team 2 roster nodes, possession bar right half  │
├───────────────────────────┼──────────────┼─────────────────────────────────────────────────┤
│ Pure Luminescence         │ #FFFFFF      │ Primary headers, high-contrast numeric data     │
│ Muted Slate               │ #71717A      │ Secondary descriptions, inactive tabs, captions │
│ Code Terminal Green       │ #34D399      │ Live stdout logs, frame ingestion counters      │
└───────────────────────────┴──────────────┴─────────────────────────────────────────────────┘
```

### Color Constraints
* **No Pure Black:** `#000000` is banned for UI container surfaces; use Void Obsidian (`#050507`) or Cockpit Charcoal (`#121214`).
* **No AI Violet/Purple Neon Glows:** Banned. Accents must reflect authentic football and sports science palettes (Gold, Pitch Emerald, Cyber Cyan).
* **Controlled Saturation:** Background tints remain strictly under 15% opacity to avoid visual fatigue during prolonged match review sessions.

---

## 3. Typography Architecture

### Font Families
* **Primary Sans (UI & Editorial):** `Geist Sans`, `Outfit`, or `Satoshi` — modern geometric sans-serif with tight letter-spacing for headlines.
* **Monospace (Telemetry & Numbers):** `Geist Mono` or `JetBrains Mono` — mandatory for all speed numbers (km/h), distance meters (m), coordinates (x, y), timestamps, angles, and pipeline stage IDs.
* **Display / Brand Accent:** `Zentry` (or geometric display bold) for branded uplift headers.

### Scale & Hierarchy
* **Screen Display Title:** `clamp(1.75rem, 3vw, 2.5rem)` | Font-weight: `900` | Tracking: `-0.03em`
* **Section Header:** `1.125rem (18px)` | Font-weight: `700` | Tracking: `-0.02em`
* **Card Sub-title:** `0.6875rem (11px)` | Font-weight: `500` | Uppercase | Tracking: `0.08em` | Color: `#71717A`
* **Telemetry Data Points:** `2.25rem (36px)` | Monospace | Font-weight: `800` | Tracking: `-0.02em`
* **Data Units (km/h, m, deg):** `0.6875rem (11px)` | Monospace | Font-weight: `700` | Uppercase | Color: `rgba(255,255,255,0.4)`
* **Body Text:** `0.875rem (14px)` | Leading: `1.6` | Max line length: `65ch`

---

## 4. Layout Architecture & Spatial Hierarchy

### 12-Column Asymmetric Cockpit Grid
* **Left Column (7 Columns):** Primary **Match Tactical Playback Card**
  * Hardware-accelerated live video stream (`/api/v1/stream-annotated-feed`)
  * Floating HUD overlays: Optical Flow Camera Vector (`ΔX, ΔY`), Ball Control HUD (`Team 1 vs Team 2 %`), and Active Feed status.
  * Direct fullscreen trigger (`Maximize2` / `Minimize2`) with full-screen container projection.
  * Tactical CV Pipeline Console with 9-stage synchronized badges and real-time Python stdout terminal drawer.
* **Right Column (5 Columns):** **Tactical Spatial Intelligence Unit**
  * Live Team Possession Balance Dual-Bar (animated gradient bar with numerical splits).
  * 3-Way Sub-Navigation Controller:
    1. **Radar View:** 2D metric pitch homography (105m × 68m top-down coordinate canvas with color-coded 10v10 nodes).
    2. **The 9 Pipes View:** Modular architecture cards detailing all 9 computer vision modules with live data throughput specs.
    3. **MediaPipe View:** Interactive 33-point human skeletal wireframe rig with live joint kinematics.

### Responsive Breakpoint Rules
* **Desktop (≥ 1024px):** 12-column asymmetric side-by-side cockpit layout.
* **Tablet (768px – 1023px):** Stacked 2-row layout with maintained aspect ratios.
* **Mobile (< 768px):** Strict single-column vertical cascade. Video aspect ratio maintained at 16:9; pipeline cards collapse to single-column tap cards; all interactive buttons adhere to a minimum tap target of `44px × 44px`.

---

## 5. Component Design Standards

### 1. Match Video Player Card
* **Frame:** Aspect ratio `16:9` (`aspect-video`), border radius `rounded-2xl`, background `#050507`.
* **Controls Toolbar:** Micro-action buttons with active border highlights:
  * `Media Pipes: ON / OFF` (Emerald badge `#10B981`)
  * `B-Boxes: ON / OFF` (Gold badge `#FACC15`)
  * `Heat Map: ON / OFF` (Blue badge `#3B82F6`)
  * `The 9 Pipes: VIEW` (Purple badge `#A855F7`)
  * `Fullscreen` (Yellow accent `#FACC15`)
* **Streaming Protocol:** Live zero-latency MJPEG stream over `/api/v1/stream-annotated-feed` for 100% universal browser compatibility without codec freezes.

### 2. Tactical Pitch Radar (2D Homography)
* **Canvas:** Dark pitch grass texture (`#0A120C`) framed by a subtle 1px emerald border (`rgba(16,185,129,0.2)`).
* **Markings:** SVG vector regulation lines (halfway line, penalty boxes, center circle, corner arcs) stroke `rgba(16,185,129,0.25)`.
* **Player Nodes:**
  * Diameter: `20px` circular discs with high-contrast white tracking ID numerals.
  * Team 1: Royal Blue fill with glowing drop shadow (`rgba(59,130,246,0.8)`).
  * Team 2: Crimson Red fill with glowing drop shadow (`rgba(239,68,68,0.8)`).
  * Hover state: Scales by 1.5x with floating glassmorphic tooltip showing speed and distance.

### 3. MediaPipe 33-Point Skeletal Rig
* **Wireframe:** Interactive vector SVG stick figure:
  * Bones: 2.5px neon cyan stroke (`#00F0FF`) with subtle drop-shadow glow.
  * Joints: 3px neon green circular vertices (`#00FF66`) with crisp white centers.
* **Kinematic Gauge Cards:** High-density 2x2 grid displaying:
  * Knee Flexion Angle (e.g., `142.0°` — sprint shock absorption).
  * Torso Lean / Acceleration Angle (e.g., `14.5°` — forward propulsion tilt).
  * Stride Efficiency Cadence (e.g., `88.0%` — locomotion turnover score).
  * Peak Velocity (e.g., `35.2 km/h` — top measured speed).

### 4. The 9 CV Pipes Architecture Cards
* **Cards:** Dark surface `#060608` with border `rgba(255,255,255,0.05)`.
* **Header:** Monospace badge (e.g., `PIPE 01`, `PIPE 02`) with title and algorithm tags.
* **Status Pills:** Glowing green `SYNCHRONIZED` tag with pulsing status indicator.

### 5. Tactical Sliding Buttons
* **Interaction:** Horizontal slide-to-activate mechanism (inspired by elite hardware lock switches).
* **Feedback:** Smooth spring transition with thumb indicator translating along track.

---

## 6. Motion Philosophy & Micro-Interactions

* **Spring Physics:** Defaults to `stiffness: 120, damping: 20` for a weighty, tactile feel. Linear easing is strictly prohibited.
* **Perpetual Micro-Interactions:**
  * Active pipeline indicators feature infinite subtle pulse rings (`animate-pulse` or `animate-ping`).
  * Terminal log auto-scrolls smoothly on new SSE message arrivals.
  * Hover states on buttons employ subtle scale increases (`hover:scale-105`) and background luminescence shifts.
* **Performance Guarantee:** All animated properties are restricted to `transform` and `opacity` to maintain 60 FPS hardware acceleration on integrated GPUs and mobile devices.

---

## 7. Anti-Patterns (Banned AI Clichés)

To maintain a bespoke, agency-grade design standard, the following patterns are **strictly prohibited**:

1. **NO Generic Emojis as UI Icons:** Use only precision SVGs from `lucide-react` (`Compass`, `Radar`, `Cpu`, `GitBranch`, `Activity`, `Terminal`).
2. **NO `Inter` Font:** Use `Geist`, `Outfit`, or `Satoshi` for sans-serifs, and `Geist Mono` or `JetBrains Mono` for monospace telemetry.
3. **NO Pure Black (`#000000`):** Always use deep charcoal `#050507` or `#121214`.
4. **NO Neon Outer Glows:** Avoid exaggerated box-shadow blurs that obscure text contrast.
5. **NO 3-Equal Cards Feature Rows:** Use asymmetric split layouts, zig-zag arrangements, or 2+1 configurations.
6. **NO Artificial Mock Timers:** Never simulate client-side timeouts; all metrics must stream from actual backend computer vision pipelines.
7. **NO Unbalanced Team Distributions:** Roster clustering must maintain strict 50/50 balance (e.g., 10 vs 10 or 11 vs 11).
8. **NO AI Copywriting Tropes:** Words like *"Next-gen"*, *"Seamless"*, *"Unleash"*, and *"Revolutionize"* are replaced with concrete technical descriptors (*"Millimeter Homography"*, *"Sub-pixel Optical Flow"*, *"Kinematic Joint Flexion"*).
