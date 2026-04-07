# 🎵 YouTube Smart Crossfade

> A Chrome extension that automatically jumps to song peaks and creates seamless crossfades between tracks — no more silence between songs.

![Version](https://img.shields.io/badge/version-12.0-blue)
![Platform](https://img.shields.io/badge/platform-Chrome%20%7C%20Edge%20%7C%20Brave-green)
![License](https://img.shields.io/badge/license-MIT-orange)

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Demo & Screenshots](#-demo--screenshots)
- [Requirements Analysis](#-requirements-analysis)
- [Feasibility Analysis](#-feasibility-analysis)
- [System Design](#-system-design)
- [Implementation](#-implementation)
- [AI Collaboration Process](#-ai-collaboration-process)
- [Testing](#-testing)
- [Installation](#-installation)
- [Configuration Guide](#-configuration-guide)
- [Lessons Learned](#-lessons-learned)
- [References](#-references)

---

## 📌 Overview

**Problem:** YouTube has a 2-5 second silence between songs, long intros before the beat drops, and no smooth transition between tracks.

**Solution:** A browser extension that:

- Reads YouTube's heatmap data to find the most replayed section
- Jumps directly to that peak position
- Crossfades between songs with zero audio gap
- Opens next song in a new tab for seamless transition

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔥 **Heatmap Peak Detection** | Parses YouTube's SVG heatmap to find the first major peak within first 15% of video |
| 🎚️ **Smooth Crossfade** | Configurable fade in/out (500ms - 16000ms) |
| 📑 **Dual-Tab Mode** | Opens next song in new tab before current ends — zero gap |
| 🛡️ **Volume Guard** | Prevents YouTube from overriding fade-in volume |
| ⚙️ **Full UI Controls** | 12 adjustable parameters with persistent storage |
| 🔍 **Smart Next Detection** | Multiple fallback methods to find next song |

---

## 🖼️ Demo & Screenshots

### UI Panel (Y Button)
<img width="348" height="104" alt="image" src="https://github.com/user-attachments/assets/d3d6579a-2082-48ef-bd2c-45241b1cc39b" />


*Caption: The "Y" button appears next to the settings gear. Click to open control panel.*

---

### Settings Panel
<img width="420" height="729" alt="image" src="https://github.com/user-attachments/assets/9fdf946a-2f0e-4cf8-8bfc-61ec96512a47" />

*Caption: All 12 settings organized into Core, Mode, Jump, and Fade sections.*

---

### Heatmap Parsing Example
<img width="437" height="142" alt="image" src="https://github.com/user-attachments/assets/4be04586-5970-4b4a-89ae-a1ef0264e8f6" />

*Caption: The extension finds the first significant peak (Y < 75) within the search window.*

---





<img width="634" height="292" alt="image" src="https://github.com/user-attachments/assets/635f2724-107d-49ba-b95d-920eb9a6eccc" />


*Caption: Debug output shows peak detection, volume changes, and crossfade events.*

---

### Before / After Comparison

| Before | After |
|--------|-------|
| {INSERT: YouTube default player screenshot} | {INSERT: Extension working screenshot} |
| 2-5 second silence between songs | Zero gap, smooth transition |
| Long intros (15-30 seconds) | Jumps directly to chorus/peak |
| Abrupt volume changes | Professional crossfade |

---

## 📋 Requirements Analysis

### Problem Statement

YouTube's default playback has four major issues for continuous music listening:

| Problem | Impact |
|---------|--------|
| **Gap between songs** | 2-5 seconds of silence breaks the flow |
| **Long intros** | 15-30 seconds before main beat |
| **Manual skipping** | Users must constantly interact |
| **No crossfade** | Abrupt volume changes are jarring |

### Functional Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-01 | Detect when a video is playing on YouTube | Must |
| FR-02 | Parse YouTube's `.ytp-modern-heat-map` SVG data | Must |
| FR-03 | Find first significant peak within first 15-20% of video | Must |
| FR-04 | Automatically jump to detected peak position | Must |
| FR-05 | Implement volume fade-out (configurable duration) | Must |
| FR-06 | Implement volume fade-in (configurable duration) | Must |
| FR-07 | Automatically detect and play next song | Must |
| FR-08 | Dual-tab mode for zero-gap transition | Must |
| FR-09 | User-adjustable settings via UI panel | Should |
| FR-10 | Persist settings across browser sessions | Should |

### Non-Functional Requirements

| ID | Requirement | Metric |
|----|-------------|--------|
| NFR-01 | Peak detection speed | < 500ms |
| NFR-02 | Performance impact | No noticeable YouTube lag |
| NFR-03 | Browser compatibility | Chrome, Edge, Brave |
| NFR-04 | Next song detection reliability | > 95% |
| NFR-05 | Code maintainability | Clear structure with comments |

---

## 🔧 Feasibility Analysis

### Technical Assessment

| Aspect | Assessment |
|--------|------------|
| Chrome Extension API | ✅ Mature, well-documented Manifest V3 |
| YouTube DOM Access | ✅ Content scripts can access/modify |
| Volume Control | ✅ HTML5 Video API supports `.volume` |
| Heatmap Parsing | ✅ SVG path data parseable with regex |
| Cross-tab Communication | ✅ Chrome messaging API available |

**Conclusion:** All required technologies are available and feasible.

### Tools Used

| Tool | Purpose |
|------|---------|
| Chrome Extension Manifest V3 | Extension framework |
| JavaScript ES6+ | Core logic |
| CSS3 | UI styling |
| Chrome Storage API | Settings persistence |
| Chrome Tabs / Scripting API | Multi-tab management |
| DeepSeek + Gemini | AI-assisted development |
| VS Code | Local development |

### Risk Mitigation

| Risk | Mitigation |
|------|------------|
| YouTube DOM changes | Multiple fallback selectors |
| Autoplay blocked | `playing` event listener fallback |
| YouTube volume restore | Volume guard (force volume every 50ms) |
| Next song detection fails | 4 different URL extraction methods |

---

## 🏗️ System Design

### Architecture Overview

