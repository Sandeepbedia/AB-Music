<div align="center">

# 🎬 AB VPlayer

### A High-Performance, Privacy-First Offline Video Player for Android

[![Android](https://img.shields.io/badge/Platform-Android-green.svg?logo=android)](https://android.com)
[![Kotlin](https://img.shields.io/badge/Language-Kotlin-blueviolet.svg?logo=kotlin)](https://kotlinlang.org)
[![API](https://img.shields.io/badge/Min%20API-21-orange.svg)](https://developer.android.com/about/versions/lollipop)
[![Media3](https://img.shields.io/badge/Engine-Media3%20ExoPlayer-blue.svg)](https://developer.android.com/media/media3)
[![License](https://img.shields.io/badge/License-MIT-lightgrey.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-1.0.0-brightgreen.svg)]()

> Play any video format. Protect your private media. Zero internet required.

</div>
---

## 📋 Table of Contents

- [About](#-about)
- [Screenshots](#-screenshots)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Architecture](#-architecture)
- [Key Modules](#-key-modules)
- [Supported Formats](#-supported-formats)
- [Performance Targets](#-performance-targets)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 About

**AB VPlayer** (`com.io.ab.vplayer`) is a production-grade, offline video player built natively for Android using **Kotlin** and **Jetpack Media3 (ExoPlayer)**. It is designed for three core promises:

| Promise | Detail |
|---|---|
| ⚡ **Zero Latency** | Hardware-accelerated 4K/10K playback with instant startup |
| 🌐 **Universal Formats** | MP4, MKV, AVI, MOV, WMV, WebM, FLV, TS and more |
| 🔒 **Privacy-First** | No internet permission. No analytics. Encrypted Private Vault |

AB VPlayer never connects to the internet during normal operation. All data — video metadata, watch history, playlists, and vault contents — is stored exclusively in the app's sandboxed Room database on your device.

---

## 📸 Screenshots

```
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│  Library (Grid) │  │  Player Screen  │  │  Private Vault  │
│                 │  │                 │  │                 │
│  [Thumbnail]    │  │  ╔═══════════╗  │  │  🔒 Enter PIN  │
│  Movie.mkv      │  │  ║  VIDEO    ║  │  │                 │
│  2h 15m  1080p  │  │  ║  PLAYING  ║  │  │  ┌──────────┐  │
│                 │  │  ╚═══════════╝  │  │  │  ••••    │  │
│  [Thumbnail]    │  │  ━━━━●━━━━━━━   │  │  └──────────┘  │
│  Episode.mp4    │  │  ◀ 1:23 / 2:15 ▶│  │  [Unlock PIN]  │
│  45m  4K        │  │  Speed: 1.0x    │  │  [Biometric]   │
└─────────────────┘  └─────────────────┘  └─────────────────┘

┌─────────────────┐  ┌─────────────────┐
│  Folder View    │  │   Playlists     │
│                 │  │                 │
│  📁 Movies (12) │  │  ▶ My Favorites │
│  📁 Series (38) │  │  ▶ Watch Later  │
│  📁 Downloads(5)│  │  ▶ Top Picks    │
│                 │  │          [+ New]│
└─────────────────┘  └─────────────────┘
```

---

## ✨ Features

### 📂 Media Discovery
- **Auto-Scan** — Indexes all videos from internal & SD card storage on first launch
- **Folder Hierarchy View** — Browse videos organized by their actual folder structure
- **Background Refresh** — Detects newly added or deleted files and updates the UI instantly
- **Smart Exclusions** — Ignores clips under 5 seconds and folders with a `.nomedia` file

### ▶️ Core Playback Engine
- **Multi-Format Playback** — MP4, MKV, AVI, MOV, WMV, WebM, FLV, TS
- **HW / HW+ / SW Decoder** — Automatic hardware fallback to software for maximum compatibility
- **Resume Playback** — Remembers exact timestamp per video; prompts to resume on reopen
- **Variable Speed Control** — 0.25x → 4.0x without pitch distortion
- **Background Audio Playback** — Continues playing audio when screen locks or app minimizes
- **Picture-in-Picture (PiP)** — Floating mini-player while using other apps

### 🎮 Gesture Controls
| Gesture | Action |
|---|---|
| Left side swipe ↕ | Brightness control |
| Right side swipe ↕ | Volume control (up to 100%) |
| Horizontal swipe ↔ | Seek / scrub through timeline |
| Double tap ◀ | Skip back 10 seconds |
| Double tap ▶ | Skip forward 10 seconds |
| Single tap | Show / hide controls |
| Lock button 🔒 | Lock all touch interactions |

### 🔊 Audio & Subtitles
- **Multi-Track Audio** — Switch between embedded language tracks in MKV/MP4
- **Internal Subtitles** — Auto-load embedded SRT, ASS, SSA, VTT tracks
- **External Subtitles** — Pick any `.srt` / `.vtt` / `.ass` file from storage
- **Sidecar Detection** — Auto-detects `video.srt` next to `video.mp4`
- **Audio Sync Shift** — Fine-tune audio delay in milliseconds
- **Subtitle Sync Shift** — Fine-tune subtitle timing offset

### 📚 Library & Organization
- **Playlists** — Create unlimited named playlists, add/remove videos freely
- **Favorites** — One-tap star any video for quick access
- **Search** — Real-time search across all video titles
- **Watch History** — "Watched" badge and progress bar overlay on thumbnails

### 🔐 Private Vault
- PIN-protected hidden directory (min 4 digits)
- Biometric unlock (fingerprint / face) via Android BiometricPrompt API
- Vault videos are hidden from the system MediaStore — invisible to other gallery apps
- AES-256-GCM encryption support via Android Keystore

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| **Language** | Kotlin 2.1 |
| **UI** | Android Views + ViewBinding |
| **Media Engine** | Jetpack Media3 (ExoPlayer) 1.5.1 |
| **Background Playback** | Media3 MediaSessionService |
| **Database** | Room DB 2.7 + KSP |
| **Architecture** | MVVM + Repository Pattern |
| **Async** | Kotlin Coroutines + LiveData |
| **Image Loading** | Glide 4.16 |
| **Security** | Android Keystore + BiometricPrompt |
| **Min SDK** | API 21 (Android 5.0 Lollipop) |
| **Target SDK** | API 34 (Android 14) |

---

## 📁 Project Structure

```
AB_VPlayer/
├── app/
│   ├── src/main/
│   │   ├── kotlin/com/io/ab/vplayer/
│   │   │   ├── data/
│   │   │   │   ├── db/
│   │   │   │   │   ├── AppDatabase.kt          # Room database singleton
│   │   │   │   │   ├── VideoFileDao.kt         # Video CRUD + queries
│   │   │   │   │   └── PlaylistDao.kt          # Playlist CRUD
│   │   │   │   ├── model/
│   │   │   │   │   ├── VideoFile.kt            # @Entity: video metadata
│   │   │   │   │   └── Playlist.kt             # @Entity: playlist + items
│   │   │   │   └── repository/
│   │   │   │       ├── MediaScanner.kt         # MediaStore scan logic
│   │   │   │       └── VideoRepository.kt      # Single source of truth
│   │   │   ├── service/
│   │   │   │   └── PlaybackService.kt          # Background audio service
│   │   │   ├── ui/
│   │   │   │   ├── MainActivity.kt             # Host + bottom nav
│   │   │   │   ├── VideoListFragment.kt        # All/Favorites/Search list
│   │   │   │   ├── VideoAdapter.kt             # Grid RecyclerView adapter
│   │   │   │   ├── FolderListFragment.kt       # Folder browser
│   │   │   │   ├── FolderAdapter.kt            # Folder list adapter
│   │   │   │   ├── PlaylistFragment.kt         # Playlist manager
│   │   │   │   ├── PlaylistAdapter.kt          # Playlist list adapter
│   │   │   │   ├── PlaylistDetailFragment.kt   # Playlist contents
│   │   │   │   ├── VideoOptionsBottomSheet.kt  # Long-press context menu
│   │   │   │   ├── PlayerActivity.kt           # Full-screen player
│   │   │   │   └── VaultActivity.kt            # PIN/biometric vault
│   │   │   ├── util/
│   │   │   │   ├── PermissionHelper.kt         # Scoped storage permissions
│   │   │   │   ├── SubtitleUtils.kt            # External SRT loader
│   │   │   │   └── VaultManager.kt             # PIN hash + AES encryption
│   │   │   └── viewmodel/
│   │   │       ├── LibraryViewModel.kt         # Library + search state
│   │   │       └── PlayerViewModel.kt          # Player state + speed/delay
│   │   ├── res/
│   │   │   ├── layout/                         # All XML layouts
│   │   │   ├── menu/                           # Bottom nav + toolbar menus
│   │   │   ├── drawable/                       # Vector icons
│   │   │   └── values/                         # Colors, strings, themes
│   │   └── AndroidManifest.xml
│   ├── build.gradle
│   └── proguard-rules.pro
├── gradle/
│   └── libs.versions.toml                      # Version catalog
├── build.gradle
├── settings.gradle
└── gradle.properties
```

---

## 🚀 Getting Started

### Prerequisites

- Android Studio **Hedgehog (2023.1.1)** or newer
- JDK 17
- Android SDK with API 34 installed
- Gradle 8.x (included via wrapper)

### Clone & Build

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/AB_VPlayer.git
cd AB_VPlayer

# 2. Open in Android Studio
#    File → Open → select the AB_VPlayer folder

# 3. Sync Gradle
#    Android Studio will auto-sync on open

# 4. Build & Run
./gradlew assembleDebug

# Or install directly to connected device
./gradlew installDebug
```

### Permissions Required

| Permission | When | Purpose |
|---|---|---|
| `READ_MEDIA_VIDEO` | API 33+ | Access video files |
| `READ_EXTERNAL_STORAGE` | API ≤ 32 | Access video files (legacy) |
| `FOREGROUND_SERVICE` | Always | Background audio playback |
| `WAKE_LOCK` | During playback | Keep screen on |
| `USE_BIOMETRIC` | Vault unlock | Fingerprint/face authentication |

> **Note:** `INTERNET` permission is intentionally **not declared**. AB VPlayer is fully offline.

---

## 🏗 Architecture

AB VPlayer follows **MVVM + Repository** pattern:

```
┌─────────────────────────────────────────────┐
│                    UI Layer                  │
│  Activity / Fragment → ViewBinding           │
│  Observes LiveData, dispatches user events   │
└────────────────────┬────────────────────────┘
                     │ observes / calls
┌────────────────────▼────────────────────────┐
│                ViewModel Layer               │
│  LibraryViewModel / PlayerViewModel          │
│  Holds UI state, survives config changes     │
└────────────────────┬────────────────────────┘
                     │ calls suspend funs
┌────────────────────▼────────────────────────┐
│              Repository Layer                │
│  VideoRepository                             │
│  Single source of truth; merges DB + Scan   │
└──────────┬──────────────────────┬───────────┘
           │                      │
┌──────────▼──────┐    ┌──────────▼──────────┐
│   Room Database  │    │   MediaStore API    │
│  (local SQLite)  │    │  (device storage)   │
│  VideoFileDao    │    │  MediaScanner.kt     │
│  PlaylistDao     │    │                     │
└──────────────────┘    └─────────────────────┘
```

### Data Flow — Library Sync

```
App Launch
    │
    ▼
PermissionHelper.hasStoragePermissions()
    │ YES                   │ NO
    ▼                       ▼
MediaScanner.scanAllVideos()  Request permissions
    │
    ▼
Merge with existing Room DB (preserve lastPosition, isFavorite, isInVault)
    │
    ▼
VideoFileDao.insertAll() + removeStale()
    │
    ▼
LiveData emits → RecyclerView updates
```

### Data Flow — Video Playback

```
VideoAdapter.onPlay(video)
    │
    ▼
PlayerActivity.onCreate()
    │
    ▼
PlayerViewModel.loadVideo(id) → Room DB → VideoFile
    │
    ▼
ExoPlayer.setMediaItem(video.uri)
    │
    ├── SubtitleUtils.detectSidecarSubtitle(path) → auto-load .srt if found
    ├── seekTo(video.lastPosition)                 → FR-2.2 Resume
    └── player.prepare() + play()
    │
    ▼
onStop() → PlayerViewModel.savePosition(id, currentPosition)
```

---

## 🔑 Key Modules

### `MediaScanner.kt`
Queries Android MediaStore API to enumerate all video files on device storage. Respects Scoped Storage (Android 10+), automatically excludes:
- Clips shorter than **5 seconds**
- Folders containing a **`.nomedia`** file

### `VideoRepository.kt`
Acts as the single source of truth. On each sync, it:
1. Runs a fresh MediaStore scan
2. Merges discovered files with existing Room records (preserving user state like favorites, vault membership, and last playback position)
3. Prunes stale database entries for deleted files

### `PlayerActivity.kt`
The full-screen player. Key responsibilities:
- Builds `ExoPlayer` with `DefaultTrackSelector` for multi-track support
- Custom `GestureDetector` handling brightness, volume, seek, and double-tap skip
- Picture-in-Picture via `PictureInPictureParams` (Android 8.0+)
- Subtitle loading from embedded tracks or external `.srt`/`.vtt`/`.ass` files
- Saves resume position on `onStop()`

### `VaultManager.kt`
- Hashes PIN using **SHA-256** before storing in `SharedPreferences`
- Generates an **AES-256-GCM** key in the Android Keystore for file-level encryption
- PIN verification is constant-time safe (uses hash comparison)

### `PlaybackService.kt`
A `MediaSessionService` (Media3) that:
- Hosts a persistent `ExoPlayer` instance
- Exposes a `MediaSession` for lock-screen notification controls
- Handles audio focus and "becoming noisy" (headphone unplug)

---

## 🎞 Supported Formats

### Video Containers
| Format | Extension | Hardware Decode |
|---|---|---|
| MPEG-4 | `.mp4`, `.m4v` | ✅ All devices |
| Matroska | `.mkv` | ✅ API 21+ |
| AVI | `.avi` | ✅ SW fallback |
| QuickTime | `.mov` | ✅ |
| Windows Media | `.wmv` | ✅ SW fallback |
| WebM | `.webm` | ✅ |
| Flash Video | `.flv` | ✅ SW fallback |
| MPEG-TS | `.ts` | ✅ |
| 3GPP | `.3gp` | ✅ |

### Audio Codecs
`AAC` · `MP3` · `AC3 (Dolby)` · `DTS` · `TrueHD` · `FLAC` · `Opus` · `Vorbis`

### Subtitle Formats
| Format | Type |
|---|---|
| SubRip | `.srt` — External & embedded |
| WebVTT | `.vtt` — External & embedded |
| SSA / ASS | `.ass`, `.ssa` — External & embedded |

---

## ⚡ Performance Targets

| Metric | Target |
|---|---|
| Cold startup to library | < 1.5 seconds |
| Idle RAM usage | < 60 MB |
| Peak RAM (4K playback) | < 250 MB |
| Battery drain @ 1080p/hr | < 8% (mid-range device) |
| Library scan (1000 files) | < 3 seconds |

---

## 🗺 Roadmap

### ✅ v1.0 — Current Release
- [x] Full video library with folder view
- [x] ExoPlayer playback with HW/SW decoder
- [x] Gesture controls (brightness / volume / seek)
- [x] Resume playback
- [x] Variable speed (0.25x – 4.0x)
- [x] Multi-track audio & subtitle support
- [x] External SRT loading
- [x] Playlists & Favorites
- [x] Private Vault (PIN + Biometric)
- [x] Picture-in-Picture
- [x] Background audio playback
- [x] Media3 notification controls

### 🔜 v2.0 — Planned
- [ ] **Local Network Streaming** — SMB, FTP, UPnP/DLNA
- [ ] **Chromecast / Android TV** casting
- [ ] **Smart Subtitle Downloader** — OpenSubtitles API (opt-in)
- [ ] **Equalizer** — 10-band audio equalizer
- [ ] **Subtitle Customization** — Font, size, color, background opacity
- [ ] **Volume Boost** — Software amplification up to 200%
- [ ] **Chapters** — MKV chapter navigation
- [ ] **Widget** — Home screen playback controls

---

## 🤝 Contributing

Contributions are welcome! Here's how:

```bash
# 1. Fork the repository
# 2. Create a feature branch
git checkout -b feature/your-feature-name

# 3. Commit your changes
git commit -m "feat: add your feature description"

# 4. Push and open a Pull Request
git push origin feature/your-feature-name
```

### Coding Standards
- Follow [Kotlin Coding Conventions](https://kotlinlang.org/docs/coding-conventions.html)
- Use `ViewBinding` — no `findViewById`
- All DB operations must run on `Dispatchers.IO`
- New features should include a ViewModel + Repository separation
- Test on API 21 (min) and API 34 (target)

### Commit Message Format
```
feat: add subtitle sync shift control
fix: resolve PiP crash on Android 8
perf: reduce memory during 4K playback
refactor: extract GestureHandler to separate class
```

---

## 🛡 Privacy Policy

AB VPlayer collects **zero data**:
- ❌ No analytics or telemetry
- ❌ No crash reporting to external servers
- ❌ No internet permission declared in manifest
- ❌ No filenames, watch history, or metadata ever leaves your device
- ✅ All data stored in app's private SQLite database only

---

## 📄 License

```
MIT License

Copyright (c) 2025 AB VPlayer

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

<div align="center">

**Built with ❤️ using Kotlin · Media3 · Room · Android Jetpack**

⭐ Star this repo if you find it useful!

</div>
