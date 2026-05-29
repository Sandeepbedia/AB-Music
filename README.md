# AB Music

A modern offline music player for Android built with Jetpack Compose and Material 3 design language. Features a rich UI with neumorphism elements, AMOLED theme support, and an immersive playback experience.

## Features

### Playback
- **ExoPlayer/Media3** engine for high-quality audio playback
- Play, pause, skip, seek, shuffle & repeat modes (Off / One / All)
- **Crossfade** transitions between tracks
- **Sleep timer** with countdown display
- **Equalizer** with 5-band controls + presets (Flat, Bass, Vocal, Classical)
- Audio focus handling (pause when other apps play audio)
- Background playback via **foreground service** with notification controls
- "Close App" button in notification when paused

### Library Management
- **Automatic music scanning** from device storage via MediaStore
- Minimum 30-second track filter
- Optional subfolder inclusion
- **Recently added** and **most played** tracking
- **Favorites** system
- **Recently played** history
- **Playlist** creation, renaming, deletion, and song management

### Browse & Discover
- **Home** tab — recently added + most played
- **Explore** tab — all songs with sort options
- **Library** tab — albums, artists, playlists sub-tabs
- **Favorites** tab
- **Search** with 300ms debounce across all songs
- Sort by name, date added, duration, or file size

### User Interface
- **Material 3** design with dynamic color support (Android 12+)
- **6 theme modes**: System, Light, Dark, AMOLED Purple, AMOLED Cyan, AMOLED Pink, AMOLED Gold
- **Neumorphic** UI elements (cards, shadows, shapes)
- **Horizontal pager** for tab navigation with swipe support
- **Mini-player** with animated artwork, waveform bars, show/hide on scroll
- **Full player screen** with album art, progress, controls
- **Queue management** screen
- **Edge-to-edge** immersive display
- **Splash screen** API

## Screenshots

| Home | Player | Library | Settings |
|------|--------|---------|---------|
| Recently added & top tracks | Full player with album art | Albums/Artists/Playlists | Theme, EQ, sleep timer |

## Tech Stack

| Layer | Technology |
|---|---|
| **UI** | Jetpack Compose, Material 3, Compose Navigation |
| **Architecture** | MVVM + Repository Pattern |
| **DI** | Hilt (Dagger) |
| **Database** | Room (SQLite) with KSP |
| **Media Playback** | AndroidX Media3 / ExoPlayer |
| **Image Loading** | Coil (Compose) |
| **Preferences** | DataStore Preferences |
| **Background** | Foreground Service + MediaSessionService |
| **Async** | Kotlin Coroutines & Flow |
| **Build** | Gradle KTS, AGP 8.5.0, Kotlin 1.9.24 |

## Build Requirements

- **Android Studio** Hedgehog or later
- **JDK** 17+
- **Gradle** 8.x
- **Min SDK**: 26 (Android 8.0)
- **Target SDK**: 36 (Android 15)
- **Compile SDK**: 36

## Building

```bash
./gradlew assembleDebug    # Debug build
./gradlew assembleRelease  # Release build (requires keystore)
```

The debug APK will have `.debug` suffix in application ID and version name.

## Project Structure

```
ABMusic/
├── app/
│   ├── src/main/
│   │   ├── AndroidManifest.xml
│   │   └── kotlin/com/io/ab/music/
│   │       ├── ABMusicApp.kt              # @HiltAndroidApp
│   │       ├── MainActivity.kt           # Single activity, theme + permission gate
│   │       ├── di/
│   │       │   └── DatabaseModule.kt     # Hilt module for Room
│   │       ├── domain/model/             # Pure domain models
│   │       │   ├── Song.kt
│   │       │   ├── Album.kt
│   │       │   ├── Artist.kt
│   │       │   ├── Playlist.kt
│   │       │   └── PlayerState.kt
│   │       ├── data/
│   │       │   ├── db/                   # Room database, DAOs, entities
│   │       │   ├── preferences/          # DataStore preferences
│   │       │   ├── repository/           # MusicRepository
│   │       │   └── scanner/              # MediaStore scanner
│   │       ├── service/
│   │       │   ├── MusicService.kt       # Media3 foreground service
│   │       │   └── NotificationCloseReceiver.kt
│   │       ├── ui/
│   │       │   ├── components/           # SongItem, MiniPlayer, ArtworkModel
│   │       │   ├── navigation/           # Screen routes, NavGraph
│   │       │   ├── theme/                # Color, Theme, Typography, Neumorphism
│   │       │   ├── viewmodel/            # Player, Library, Settings ViewModels
│   │       │   └── screens/              # Home, Explore, Library, Favorites,
│   │       │                             # Search, Player, Queue, Settings
│   │       └── utils/
│   │           └── Extensions.kt
│   ├── build.gradle
│   └── proguard-rules.pro
├── gradle/
│   └── libs.versions.toml                # Version catalog
├── settings.gradle
├── gradle.properties
└── update.json                           # OTA update info
```

## Architecture

The app follows **MVVM** with a single `MusicRepository` orchestrating Room DAOs and the `MusicScanner`. ViewModels expose `StateFlow` to Compose screens. The `PlayerViewModel` connects to `MusicService` via Media3's `MediaController` for playback control.

### Data Flow

```
MediaStore → MusicScanner → Room Database → Repository → ViewModel → Compose UI
                                        ↘ PlayerViewModel → MediaController → MusicService → ExoPlayer
```

## Permissions

| Permission | Purpose |
|---|---|
| `READ_MEDIA_AUDIO` (13+) | Access audio files |
| `READ_EXTERNAL_STORAGE` (≤12) | Access audio files |
| `POST_NOTIFICATIONS` | Media playback notification |
| `FOREGROUND_SERVICE` + `MEDIA_PLAYBACK` | Background playback |
| `BLUETOOTH_CONNECT` | Bluetooth device controls |

## License

```
Copyright 2024 Sandeep Bedia

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
