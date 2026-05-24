# UMD Testudo Course Seat Tracker

A Windows system-tray app that watches UMD course seat availability and fires a toast notification the moment a seat opens.

---

## Features

| Feature | Detail |
|---|---|
| 🟢 Tray icon | Green = seats open · Red = all full · Yellow = checking / error |
| 🔔 Notifications | Windows toast when a section flips closed → open |
| ⚙ Configurable | Poll interval, notify-on-close toggle, live course list |
| 🖱 Right-click menu | Per-course status, pause/resume, check now, settings, quit |
| 📦 Single .exe | PyInstaller bundles everything — no Python needed on target machine |

---

## Quick Start

### 1 — Install dependencies

```bat
setup.bat
```

### 2 — Edit `courses.json`

Open `courses.json` and replace the example entries with the courses you want to track.

```json
[
  {
    "courseId": "CMSC351",
    "termId": "202608",
    "sectionId": "",
    "label": "Algorithms"
  },
  {
    "courseId": "CMSC131",
    "termId": "202608",
    "sectionId": "0101",
    "label": "OOP I §0101"
  }
]
```

| Field | Meaning |
|---|---|
| `courseId` | Course code exactly as on Testudo (e.g. `CMSC351`) |
| `termId` | Term code: `202501` = Spring 2025, `202508` = Summer 2025, `202601` = Spring 2026, `202608` = Summer 2026, etc. |
| `sectionId` | Leave `""` to track **all** sections, or enter a specific section like `"0101"` |
| `label` | Optional friendly name shown in the tray menu |

### 3 — Run

```bat
python tracker.py
```

An icon appears in the system tray (bottom-right corner). Right-click for the full menu.

---

## Build a standalone .exe

```bat
build.bat
```

Output: `dist\CourseTracker.exe`

Copy it anywhere. On first launch it will create `courses.json` next to the `.exe` and open Notepad so you can fill it in.

---

## Settings (right-click → ⚙ Settings)

| Setting | Default | Notes |
|---|---|---|
| Poll interval | 60 s | Minimum 30 s (Testudo rate-limit protection) |
| Notify on close | Off | Also notify when a seat disappears |
| Edit courses.json | — | Opens in Notepad; use *Reload* after saving |
| Reload courses.json | — | Re-reads the file and restarts polling without restarting the app |

Settings are stored in `settings.json` next to the script / exe.

---

## How it works

1. **Polling** — every N seconds the app hits Testudo's lightweight sections endpoint:
   ```
   https://app.testudo.umd.edu/soc/{termId}/sections?courseIds={courseId}
   ```
2. **Parsing** — BeautifulSoup looks for `div.section` elements, reads `.open-seats-count`, and checks whether the div carries the `open` CSS class.
3. **State diff** — previous open/closed state is remembered; a closed→open transition fires a toast.
4. **Browser link** — clicking a course in the menu (or clicking the notification) opens the full Testudo search URL with all filters set to "show everything".

---

## Finding your `termId`

Visit `https://app.testudo.umd.edu/soc/` and look at the term selector. The value in the URL after you pick a term is your `termId`.

Common codes:
- `202501` — Spring 2025
- `202505` — Winter 2025 (if offered)
- `202508` — Summer 2025
- `202601` — Spring 2026
- `202608` — Summer 2026

---

## Files

```
Course Tracker/
├── tracker.py        ← main application
├── courses.json      ← your course list (edit this!)
├── settings.json     ← auto-created on first settings change
├── icon.ico          ← auto-generated on first run / build
├── tracker.log       ← rolling log
├── requirements.txt  ← pip dependencies
├── setup.bat         ← installs dependencies
└── build.bat         ← creates dist\CourseTracker.exe
```

---

## Dependencies

```
requests        HTTP client
beautifulsoup4  HTML parsing
pystray         Windows system tray
Pillow          Icon image generation
plyer           Cross-platform toast notifications
pyinstaller     .exe packaging
```
