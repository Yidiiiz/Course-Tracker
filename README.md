<div align="center">

# UMD Course Tracker

**Never miss an open seat.** A lightweight Windows tray app that watches Testudo and fires an instant notification the moment a seat opens up.

<br/>

[![Download](https://img.shields.io/github/v/release/Yidiiiz/UMD-Course-Tracker?label=Download%20Latest&style=for-the-badge&color=22c55e&logo=windows&logoColor=white)](https://github.com/Yidiiiz/UMD-Course-Tracker/releases/latest/download/UMDCourseTracker.exe)

</div>

---

## Getting Started

### 1 — Download & Run

Download **UMDCourseTracker.exe** above and double-click it. No installation, no Python needed.

### 2 — Pin it to your taskbar

> ⚠️ **Do this first** — by default Windows hides tray icons in the overflow menu (the `^` arrow). To keep the tracker always visible:
>
> **Windows 11:** Drag the 🟡 icon out of the overflow tray onto your taskbar notification area.  
> **Windows 10:** Right-click the taskbar → *Taskbar settings* → *Select which icons appear on the taskbar* → turn on **UMD Course Tracker**.

### 3 — Add your courses

Left-click the tray icon to open the panel. Enter a course ID (e.g. `CMSC351`), pick the semester, and click **+ Add Course**.

---

## Usage

| Action | How |
|---|---|
| Open panel | Left-click the tray icon |
| Add a course | Enter course ID + optional section, pick semester, click **+ Add Course** |
| Remove a course | Hover a card → click the **×** that appears |
| Open on Testudo | Click anywhere on a course card |
| Tray icon color | 🟢 Seats open · 🔴 Full · 🟡 Checking / error |

---

## Advanced Settings

Expand **Advanced** at the bottom of the panel:

| Setting | Default | Notes |
|---|---|---|
| Poll interval | 60 s | Minimum 30 s |
| Notify when a section closes | Off | — |
| Open on Windows startup | On | Adds registry entry |
| Theme | System | Follows Windows dark/light mode |

---

## Requirements

- Windows 10 or 11
- No UMD account needed — seat data is public

---

## Term Codes

The app picks the most likely upcoming semester automatically. To override:

| Code | Semester |
|---|---|
| `202501` | Spring 2025 |
| `202508` | Summer 2025 |
| `202512` | Winter 2026 |
| `202601` | Spring 2026 |
| `202608` | Fall 2026 |

---

## Build from Source

```bat
git clone https://github.com/Yidiiiz/UMD-Course-Tracker.git
cd "UMD-Course-Tracker"
setup.bat   # install dependencies
build.bat   # produces dist\UMDCourseTracker.exe
```

**Dependencies:** `requests` · `beautifulsoup4` · `pystray` · `Pillow` · `plyer` · `pyinstaller`
