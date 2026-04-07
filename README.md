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
