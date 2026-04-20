# 🦁 Fasting Coach — AI Edge Gallery Skill

A motivational intermittent fasting coach that runs **100% on-device**. No cloud. No accounts. No tracking. Your health data stays on your phone.

## Features

- **Start/Stop/Track** fasts with natural language — "start fasting", "how long left?", "end fast"
- **5 Fasting Phases** explained in real-time: Digestion → Transition → Fat Burn → Deep Burn → Goal
- **Protocol Support**: 14/10, 16/8 (default), 18/6, OMAD
- **Interactive Dashboard**: Circular progress ring, color-coded phases, live timer
- **Streak Tracking**: Consecutive days of hitting your goal
- **Fasting History**: Last 7 fasts at a glance with goal/completion status
- **Motivational Coach**: Phase-appropriate encouragement from Gemma 4
- **Zero Cloud**: All data in localStorage. Zero network requests.

## Installation

### Option 1: Load from URL (Recommended)
1. Open **AI Edge Gallery** app
2. Select a model (Gemma 4 E4B recommended) → **Agent Skills**
3. Tap **Skills** chip → **(+)** → **Load skill from URL**
4. Enter: `https://<your-username>.github.io/fasting-coach`

### Option 2: Import from Local File (Android)
```bash
git clone https://github.com/<your-username>/fasting-coach.git
adb push fasting-coach/ /sdcard/Download/
```
Then in AI Edge Gallery: Skills → (+) → Import local skill → select the folder

### Option 3: Featured Skills
If listed in the community gallery: Skills → (+) → Add from featured list → Fasting Coach

## Usage

| Command | Action |
|---------|--------|
| "start fasting" | Begin a 16/8 fast from now |
| "start 18/6 fast" | Begin an 18/6 fast |
| "how long left?" | Show current phase, elapsed time, remaining time |
| "end fast" | Break the fast, log it, show summary |
| "dashboard" | Show interactive progress dashboard |
| "history" | Show past fasts and streak |
| "cancel fast" | Cancel without logging |

## How It Works

```
User → "start fasting"
  → Gemma 4 interprets intent
    → Calls run_js with {action: "start", protocol: "16/8"}
      → JS saves startTime to localStorage
      → Returns start time + phase info + dashboard webview
        → User sees interactive ring + phase explanation
```

All data is stored in `localStorage` on the device. No data ever leaves the phone.

## Skill Architecture

```
fasting-coach/
├── SKILL.md              ← Agent instructions (YAML frontmatter + Markdown)
├── scripts/
│   └── index.html        ← JS logic: actions, localStorage, calculations
├── assets/
│   └── webview.html      ← Interactive dashboard (SVG ring, phases, history)
└── README.md             ← This file
```

### SKILL.md
Defines the coaching persona, fasting phases, and action mappings. Gemma 4 reads this to know how to respond and which `run_js` calls to make.

### scripts/index.html
The logic engine. Handles 6 actions: `start`, `stop`, `cancel`, `status`, `history`, `dashboard`. All data in `localStorage`.

### assets/webview.html
Self-contained HTML/CSS/JS dashboard. Receives state via URL parameters and reads localStorage. Features:
- SVG circular progress ring (color-coded by phase)
- Phase progress bar
- Streak display
- 7-day history dots
- Summary and idle states

## Why On-Device?

Fasting data is **deeply personal**. When you eat, when you don't, your discipline patterns — this belongs on your device, not on a server. Fasting Coach never sends a single byte to the cloud.

## License

Apache License 2.0
