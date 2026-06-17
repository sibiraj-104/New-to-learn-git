# Software Requirements Specification (SRS)
## Project: Spotify Clone Web Application
**Version:** 1.0.0  
**Date:** June 2026  
**Author:** Development Team  
**Status:** Approved  

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Project Scope](#2-project-scope)
3. [Users & Stakeholders](#3-users--stakeholders)
4. [Functional Requirements](#4-functional-requirements)
5. [Non-Functional Requirements](#5-non-functional-requirements)
6. [System Architecture](#6-system-architecture)
7. [Tech Stack & Dependencies](#7-tech-stack--dependencies)
8. [UI/UX Design Requirements](#8-uiux-design-requirements)
9. [Responsive Design Specifications](#9-responsive-design-specifications)
10. [Pages & Features Breakdown](#10-pages--features-breakdown)
11. [Data Model](#11-data-model)
12. [Audio Player Specifications](#12-audio-player-specifications)
13. [State Management](#13-state-management)
14. [Folder Structure](#14-folder-structure)
15. [Constraints & Assumptions](#15-constraints--assumptions)
16. [Milestones & Phases](#16-milestones--phases)
17. [Glossary](#17-glossary)

---

## 1. Introduction

### 1.1 Purpose
This document defines the complete Software Requirements Specification (SRS) for the **Spotify Clone Web Application**. It describes all functional and non-functional requirements, system design, UI/UX specifications, and project scope. This serves as the single source of truth for development, testing, and review.

### 1.2 Project Description
The Spotify Clone is a **fully responsive, feature-rich music streaming web application** that replicates the look, feel, and core functionality of the Spotify Web Player. It is built using **React.js 18 + Vite 5** with vanilla CSS and mock data (optionally upgradeable to the real Spotify API).

### 1.3 Goals
- Deliver a visually identical copy of Spotify's Web Player UI
- Ensure full responsiveness across all devices (Mobile → Desktop)
- Provide real HTML5 audio playback
- Use stable, pinned package versions for long-term maintainability
- Write clean, modular, reusable component architecture

### 1.4 Out of Scope
- User authentication / login system (cosmetic only)
- Real-time streaming via Spotify's CDN
- Payment / subscription management
- Social features (following users, shared playlists)
- Podcast support (cosmetic placeholder only)
- Push notifications

---

## 2. Project Scope

### 2.1 In Scope

| Feature | Included |
|---|---|
| Sidebar navigation | ✅ |
| Top navigation bar | ✅ |
| Home page feed | ✅ |
| Search page with genre grid | ✅ |
| Your Library page | ✅ |
| Playlist detail page | ✅ |
| Artist profile page | ✅ |
| Music player bar (bottom) | ✅ |
| Mobile bottom tab navigation | ✅ |
| Audio playback (HTML5) | ✅ |
| Responsive layout (5 breakpoints) | ✅ |
| Zustand state management | ✅ |
| Keyboard shortcuts | ✅ |
| Skeleton loaders | ✅ |
| Toast notifications | ✅ |
| Right-click context menus | ✅ |
| Mock data (playlists, songs, artists) | ✅ |

### 2.2 Optional (Future Scope)
- Real Spotify API integration via OAuth2 PKCE
- Dark/Light theme toggle
- Lyrics page
- Equalizer visualization

---

## 3. Users & Stakeholders

### 3.1 Primary User

**General Music Listener**
- Age: 16–45
- Tech comfort: Moderate to high
- Devices: Desktop (Chrome/Firefox/Edge), Mobile (iOS/Android browsers)
- Goal: Listen to music, browse playlists, discover new songs

### 3.2 User Personas

#### 🎧 Persona 1 — "Aarav" (Desktop Power User)
| Attribute | Detail |
|---|---|
| Age | 24 |
| Device | MacBook / Windows Laptop |
| Browser | Chrome |
| Behavior | Uses keyboard shortcuts, creates playlists, listens for hours |
| Needs | Full sidebar, rich home feed, responsive player |

#### 📱 Persona 2 — "Priya" (Mobile Casual Listener)
| Attribute | Detail |
|---|---|
| Age | 19 |
| Device | iPhone 13 / Android mid-range |
| Browser | Safari / Chrome Mobile |
| Behavior | Searches for songs on-the-go, uses quick controls |
| Needs | Compact player, bottom nav, minimal taps to play music |

#### 💻 Persona 3 — "Ravi" (Developer / Reviewer)
| Attribute | Detail |
|---|---|
| Age | 30 |
| Device | Desktop |
| Goal | Evaluate code quality, responsiveness, and architecture |
| Needs | Clean codebase, stable versions, no console errors |

---

## 4. Functional Requirements

### 4.1 Sidebar Navigation (FR-01)
- **FR-01.1** The sidebar shall display: Spotify logo, Home, Search, Your Library links
- **FR-01.2** The sidebar shall show a scrollable playlist list below the nav links
- **FR-01.3** Clicking any sidebar link shall navigate to the correct page without full reload
- **FR-01.4** The active link shall be highlighted with white text (non-active: gray)
- **FR-01.5** On screens `< 768px`, the sidebar shall be hidden completely
- **FR-01.6** On screens `768–1024px`, the sidebar shall collapse to icon-only mode

### 4.2 Top Navigation Bar (FR-02)
- **FR-02.1** The top bar shall show Back (←) and Forward (→) navigation arrows
- **FR-02.2** The top bar shall show a user avatar circle on the right
- **FR-02.3** The top bar background shall become opaque on scroll (glassmorphism effect)
- **FR-02.4** On the Search page, the top bar shall contain a search input field

### 4.3 Home Page (FR-03)
- **FR-03.1** The home page shall display a time-based greeting: "Good morning", "Good afternoon", "Good evening"
- **FR-03.2** The home page shall render a "Recently Played" horizontal scrollable row
- **FR-03.3** The home page shall render "Made For You", "Featured Charts", and "New Releases" rows
- **FR-03.4** Each row shall contain horizontally scrollable song/playlist cards
- **FR-03.5** Clicking a card shall navigate to the Playlist detail page
- **FR-03.6** Hovering a card shall reveal a green circular play button

### 4.4 Search Page (FR-04)
- **FR-04.1** The search page shall display a text input field at the top
- **FR-04.2** Below the input, a "Browse All" genre grid shall be displayed
- **FR-04.3** Each genre card shall have a unique background color and a category image
- **FR-04.4** Typing in the input shall filter and show matching songs/artists/playlists
- **FR-04.5** Search results shall display in a list format with album art, title, and artist

### 4.5 Your Library Page (FR-05)
- **FR-05.1** The library shall have three tabs: Playlists, Albums, Artists
- **FR-05.2** Each tab shall display its respective items in a card or list view
- **FR-05.3** A toggle button shall switch between grid and list view
- **FR-05.4** A sort dropdown shall allow sorting by: Name, Recently Added, Creator

### 4.6 Playlist Detail Page (FR-06)
- **FR-06.1** The page header shall show: playlist cover art, name, description, owner, total tracks, total duration
- **FR-06.2** The header background shall use a dynamic gradient derived from the album art color
- **FR-06.3** A track list table shall show: #, Title, Artist, Album, Date Added, Duration
- **FR-06.4** Clicking a track row shall begin playback of that song
- **FR-06.5** A Play and Shuffle button shall be shown above the track list
- **FR-06.6** A heart (❤) icon shall toggle "Liked" status on the playlist

### 4.7 Artist Profile Page (FR-07)
- **FR-07.1** The artist page shall show: artist cover image, name, monthly listener count
- **FR-07.2** Popular Tracks section shall show the top 5 songs
- **FR-07.3** Discography section shall show albums in a horizontal card row
- **FR-07.4** A Follow button shall toggle follow state

### 4.8 Music Player Bar (FR-08)
- **FR-08.1** The player shall be fixed at the bottom of the screen at all times
- **FR-08.2** Left section: album art thumbnail (48×48px), track title, artist name, heart icon
- **FR-08.3** Center section: Shuffle, Previous, Play/Pause, Next, Repeat buttons
- **FR-08.4** The Play/Pause button shall toggle between playing and paused state
- **FR-08.5** Center section shall show a seekable progress bar with current time / total duration
- **FR-08.6** Right section: Queue icon, volume icon, volume slider
- **FR-08.7** On mobile (`< 768px`), only album art + title + play/pause shall be shown

### 4.9 Audio Playback (FR-09)
- **FR-09.1** The app shall use the HTML5 `<audio>` element for playback
- **FR-09.2** Clicking Play on any song shall load and play that song's audio file
- **FR-09.3** The progress bar shall update in real time as the song plays
- **FR-09.4** Clicking the progress bar shall seek to that position in the track
- **FR-09.5** The volume slider shall control audio output volume (0–100%)
- **FR-09.6** When a track ends, the next track in the queue shall play automatically
- **FR-09.7** Shuffle mode shall randomize the play queue
- **FR-09.8** Repeat modes: Off → Repeat All → Repeat One

### 4.10 Bottom Navigation — Mobile (FR-10)
- **FR-10.1** On screens `< 768px`, a bottom tab bar shall be fixed above the player
- **FR-10.2** Tabs: Home, Search, Your Library
- **FR-10.3** Active tab shall be highlighted with white icon + label
- **FR-10.4** Tapping a tab shall navigate to the corresponding page

### 4.11 Keyboard Shortcuts (FR-11)
| Key | Action |
|---|---|
| `Space` | Play / Pause |
| `←` | Rewind 10 seconds |
| `→` | Forward 10 seconds |
| `Shift + ←` | Previous track |
| `Shift + →` | Next track |
| `M` | Mute / Unmute |
| `L` | Toggle Like on current song |

### 4.12 Context Menu (FR-12)
- **FR-12.1** Right-clicking a song/card shall open a context menu
- **FR-12.2** Context menu options: Add to Queue, Add to Playlist, Like Song, Share, Go to Artist, Go to Album
- **FR-12.3** Clicking outside the menu shall close it

### 4.13 Toast Notifications (FR-13)
- **FR-13.1** A toast shall appear when: song is liked, added to playlist, or removed from library
- **FR-13.2** Toasts shall auto-dismiss after 3 seconds
- **FR-13.3** Toasts shall appear at the bottom-left of the screen

### 4.14 Skeleton Loaders (FR-14)
- **FR-14.1** While content is loading (simulated), skeleton placeholder cards shall render
- **FR-14.2** Skeletons shall animate with a shimmer effect

---

## 5. Non-Functional Requirements

### 5.1 Performance (NFR-01)
- **NFR-01.1** First Contentful Paint (FCP) ≤ 1.5 seconds
- **NFR-01.2** Time to Interactive (TTI) ≤ 3 seconds
- **NFR-01.3** No jank or layout shift during scroll (CLS score < 0.1)
- **NFR-01.4** CSS animations shall use `transform` and `opacity` only (GPU-accelerated)

### 5.2 Stability (NFR-02)
- **NFR-02.1** All npm packages shall use exact pinned versions (no `^` or `~`)
- **NFR-02.2** `npm run dev` shall start without errors or warnings
- **NFR-02.3** `npm run build` shall produce a production bundle without errors
- **NFR-02.4** No `console.error` or unhandled promise rejections in the browser

### 5.3 Compatibility (NFR-03)
| Browser | Minimum Version |
|---|---|
| Chrome | 110+ |
| Firefox | 110+ |
| Edge | 110+ |
| Safari | 15+ |
| Chrome Mobile | 110+ |

### 5.4 Accessibility (NFR-04)
- **NFR-04.1** All interactive elements shall have ARIA labels
- **NFR-04.2** Focus indicators shall be visible on keyboard navigation
- **NFR-04.3** Color contrast ratio shall meet WCAG AA (4.5:1 for text)
- **NFR-04.4** `prefers-reduced-motion` media query shall disable animations

### 5.5 Responsive (NFR-05)
- **NFR-05.1** No horizontal scroll at any supported viewport width
- **NFR-05.2** Text shall never overflow its container
- **NFR-05.3** All touch targets shall be ≥ 44×44px on mobile
- **NFR-05.4** App shall be fully usable with one thumb on a 375px screen

### 5.6 Code Quality (NFR-06)
- **NFR-06.1** Components shall be ≤ 200 lines each
- **NFR-06.2** No inline styles — all styles in `.css` files
- **NFR-06.3** Zustand store shall be the single source of truth for player state
- **NFR-06.4** Custom hooks shall be used for reusable logic

---

## 6. System Architecture

```
┌─────────────────────────────────────────────────┐
│                  Browser (Client)                │
│                                                 │
│  ┌──────────┐  ┌──────────────┐  ┌──────────┐  │
│  │ Sidebar  │  │  Main Area   │  │  Player  │  │
│  │          │  │  (Pages)     │  │  (Bar)   │  │
│  │ - Home   │  │  - Home.jsx  │  │          │  │
│  │ - Search │  │  - Search    │  │ Zustand  │  │
│  │ - Library│  │  - Library   │  │  Store   │  │
│  └──────────┘  │  - Playlist  │  │          │  │
│                │  - Artist    │  │ HTML5    │  │
│                └──────────────┘  │ Audio    │  │
│                                  └──────────┘  │
│                                                 │
│  ┌─────────────────────────────────────────┐   │
│  │         React Router DOM v6              │   │
│  │  /home  /search  /library  /playlist/:id│   │
│  └─────────────────────────────────────────┘   │
│                                                 │
│  ┌─────────────────────────────────────────┐   │
│  │            Mock Data Layer               │   │
│  │  mockData.js → songs[], playlists[],    │   │
│  │  artists[], genres[]                    │   │
│  └─────────────────────────────────────────┘   │
└─────────────────────────────────────────────────┘
```

---

## 7. Tech Stack & Dependencies

### 7.1 Core
| Package | Version | Purpose |
|---|---|---|
| `react` | `18.2.0` | UI framework |
| `react-dom` | `18.2.0` | DOM rendering |
| `vite` | `5.2.0` | Build tool + dev server |
| `@vitejs/plugin-react` | `4.2.1` | Vite React plugin |

### 7.2 Application
| Package | Version | Purpose |
|---|---|---|
| `react-router-dom` | `6.23.1` | Client-side routing |
| `zustand` | `4.5.2` | Global state management |
| `react-icons` | `5.2.1` | Icon library (Spotify-like icons) |

### 7.3 Styling
- Vanilla CSS with CSS Custom Properties (variables)
- Google Fonts: `Inter` (400, 500, 600, 700)
- No CSS frameworks (no Bootstrap, no Tailwind)

### 7.4 Audio
- Native HTML5 `<audio>` element
- Web Audio API (optional for visualizer)
- Royalty-free MP3 tracks (local `/public/tracks/`)

---

## 8. UI/UX Design Requirements

### 8.1 Color Palette (Spotify Exact)
```
Background Base:       #121212
Background Highlight:  #1A1A1A
Background Elevated:   #242424
Spotify Green:         #1DB954
Spotify Green Hover:   #1ED760
Text Primary:          #FFFFFF
Text Secondary:        #A7A7A7
Text Subdued:          #6A6A6A
Border:                #282828
Error:                 #E91429
```

### 8.2 Typography
```
Font Family:  'Inter', sans-serif
H1:           700 weight, 2rem
H2:           700 weight, 1.5rem
H3:           600 weight, 1.125rem
Body:         400 weight, 0.875rem
Caption:      400 weight, 0.75rem
Label:        600 weight, 0.6875rem, UPPERCASE, letter-spacing: 0.1em
```

### 8.3 Spacing System
```
--space-xs:   4px
--space-sm:   8px
--space-md:   16px
--space-lg:   24px
--space-xl:   32px
--space-2xl:  48px
```

### 8.4 Border Radius
```
--radius-sm:  4px
--radius-md:  8px
--radius-lg:  12px
--radius-full: 50%   (circle avatars, play buttons)
```

### 8.5 Transitions
```
--transition-fast:   150ms ease
--transition-normal: 250ms ease
--transition-slow:   400ms ease
```

---

## 9. Responsive Design Specifications

### 9.1 Breakpoints
```css
/* Mobile Small */   @media (max-width: 480px)
/* Mobile Large */   @media (min-width: 481px) and (max-width: 768px)
/* Tablet */         @media (min-width: 769px) and (max-width: 1024px)
/* Desktop */        @media (min-width: 1025px) and (max-width: 1280px)
/* Wide Desktop */   @media (min-width: 1281px)
```

### 9.2 Layout Behavior Per Breakpoint
| Component | < 480px | 480–768px | 768–1024px | 1024–1280px | > 1280px |
|---|---|---|---|---|---|
| Sidebar | Hidden | Hidden | Icon only | Full | Full |
| Bottom Nav | Visible | Visible | Hidden | Hidden | Hidden |
| Player | Minimal | Compact | Full | Full | Full |
| Card Grid | 2 cols | 3 cols | 4 cols | 5 cols | 6 cols |
| Track Table | 2 cols | 3 cols | 5 cols | 6 cols | 6 cols |
| Search Grid | 2 cols | 2 cols | 3 cols | 4 cols | 5 cols |

### 9.3 Layout Dimensions
```
Sidebar Width (full):      240px
Sidebar Width (collapsed):  72px
Player Bar Height:          90px (desktop) / 72px (mobile)
Top Bar Height:             64px
Bottom Nav Height:          56px (mobile only)
```

---

## 10. Pages & Features Breakdown

### 10.1 Page Routing
| Route | Component | Description |
|---|---|---|
| `/` or `/home` | `Home.jsx` | Main landing feed |
| `/search` | `Search.jsx` | Browse and search |
| `/library` | `Library.jsx` | User's library |
| `/playlist/:id` | `Playlist.jsx` | Playlist/Album detail |
| `/artist/:id` | `Artist.jsx` | Artist profile |

### 10.2 Component Inventory
| Component | Location | Responsibility |
|---|---|---|
| `Sidebar` | `components/Sidebar/` | Left navigation |
| `Navbar` | `components/Navbar/` | Top bar |
| `Player` | `components/Player/` | Bottom music player |
| `BottomNav` | `components/BottomNav/` | Mobile tab bar |
| `SongCard` | `components/Cards/` | Music card (home rows) |
| `TrackRow` | `components/TrackList/` | Single track table row |
| `Toast` | `components/UI/` | Notification popup |
| `Skeleton` | `components/UI/` | Loading placeholder |
| `ContextMenu` | `components/UI/` | Right-click menu |
| `Slider` | `components/UI/` | Volume / seek slider |

---

## 11. Data Model

### 11.1 Song Object
```js
{
  id: "song_001",
  title: "Blinding Lights",
  artist: "The Weeknd",
  artistId: "artist_001",
  album: "After Hours",
  albumId: "album_001",
  albumArt: "/assets/albums/after-hours.jpg",
  duration: 200,          // seconds
  audioSrc: "/tracks/sample1.mp3",
  liked: false,
  dateAdded: "2024-01-15"
}
```

### 11.2 Playlist Object
```js
{
  id: "playlist_001",
  name: "Top 50 Global",
  description: "Your weekly music roundup",
  owner: "Spotify",
  coverArt: "/assets/playlists/top50.jpg",
  songs: ["song_001", "song_002", ...],
  totalDuration: 3600,    // seconds
  followers: 28000000,
  isLiked: false
}
```

### 11.3 Artist Object
```js
{
  id: "artist_001",
  name: "The Weeknd",
  coverImage: "/assets/artists/weeknd.jpg",
  monthlyListeners: 85000000,
  isFollowed: false,
  popularTracks: ["song_001", "song_002"],
  albums: ["album_001", "album_002"]
}
```

### 11.4 Zustand Player Store
```js
{
  currentSong: Song | null,
  queue: Song[],
  isPlaying: boolean,
  currentTime: number,
  duration: number,
  volume: number,         // 0–1
  isMuted: boolean,
  shuffle: boolean,
  repeat: "off" | "all" | "one",

  // Actions
  play: (song) => void,
  pause: () => void,
  next: () => void,
  prev: () => void,
  seek: (time) => void,
  setVolume: (vol) => void,
  toggleShuffle: () => void,
  cycleRepeat: () => void,
  toggleLike: (songId) => void,
  addToQueue: (song) => void
}
```

---

## 12. Audio Player Specifications

### 12.1 Playback Engine
- Engine: HTML5 `<audio>` element
- Audio formats supported: `.mp3`, `.ogg`, `.wav`
- Preload strategy: `metadata` (load metadata only until play)

### 12.2 Controls
| Control | Type | Range |
|---|---|---|
| Play/Pause | Toggle button | — |
| Previous | Button | — |
| Next | Button | — |
| Seek | Range input | 0 to `duration` (seconds) |
| Volume | Range input | 0 to 1 |
| Shuffle | Toggle | on/off |
| Repeat | Cycle button | off → all → one |

### 12.3 Progress Bar
- Updates every `250ms` via `setInterval` or `timeupdate` event
- Click-to-seek: calculates `(clickX / barWidth) × duration`
- Shows: `currentTime` formatted as `m:ss` and `duration` as `m:ss`

---

## 13. State Management

### 13.1 Zustand Store Design
- Single store: `playerStore.js`
- No Redux — Zustand is simpler and stable
- `persist` middleware NOT used (state resets on refresh — by design)

### 13.2 State Flow
```
User clicks Play on a Card
       ↓
playerStore.play(song) called
       ↓
currentSong updated in store
       ↓
Player component re-renders
       ↓
<audio> src updated → audio.play()
       ↓
isPlaying = true → UI updates
```

---

## 14. Folder Structure

```
spotify-clone/
├── public/
│   └── tracks/
│       ├── sample1.mp3
│       ├── sample2.mp3
│       └── sample3.mp3
├── src/
│   ├── assets/
│   │   ├── albums/
│   │   ├── artists/
│   │   ├── playlists/
│   │   └── logo.svg
│   ├── components/
│   │   ├── Sidebar/
│   │   │   ├── Sidebar.jsx
│   │   │   └── Sidebar.css
│   │   ├── Navbar/
│   │   │   ├── Navbar.jsx
│   │   │   └── Navbar.css
│   │   ├── Player/
│   │   │   ├── Player.jsx
│   │   │   └── Player.css
│   │   ├── BottomNav/
│   │   │   ├── BottomNav.jsx
│   │   │   └── BottomNav.css
│   │   ├── Cards/
│   │   │   ├── SongCard.jsx
│   │   │   └── Cards.css
│   │   ├── TrackList/
│   │   │   ├── TrackList.jsx
│   │   │   ├── TrackRow.jsx
│   │   │   └── TrackList.css
│   │   └── UI/
│   │       ├── Toast.jsx
│   │       ├── Skeleton.jsx
│   │       ├── ContextMenu.jsx
│   │       ├── Slider.jsx
│   │       └── UI.css
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── Search.jsx
│   │   ├── Library.jsx
│   │   ├── Playlist.jsx
│   │   └── Artist.jsx
│   ├── store/
│   │   └── playerStore.js
│   ├── data/
│   │   └── mockData.js
│   ├── hooks/
│   │   ├── useAudioPlayer.js
│   │   ├── useMediaQuery.js
│   │   └── useToast.js
│   ├── App.jsx
│   ├── App.css
│   ├── main.jsx
│   └── index.css
├── index.html
├── vite.config.js
├── package.json
├── .gitignore
└── SRS.md                   ← This file
```

---

## 15. Constraints & Assumptions

### 15.1 Constraints
- No real Spotify API in v1.0 — mock data only
- Audio files are stored locally in `/public/tracks/`
- No backend server — pure frontend SPA
- No user authentication in v1.0

### 15.2 Assumptions
- User has Node.js ≥ 18 installed
- User has npm ≥ 9 installed
- Modern browser with ES2020+ support
- Internet connection for Google Fonts

---

## 16. Milestones & Phases

| Phase | Description | Deliverable |
|---|---|---|
| **Phase 1** | Project setup, design system, layout shell | Dev server running, CSS variables |
| **Phase 2** | Sidebar + Navbar + Bottom Nav (mobile) | Navigation working across all routes |
| **Phase 3** | Music Player Bar with audio playback | Songs play, progress bar works |
| **Phase 4** | Home page (greeting + card rows) | Full home feed with mock data |
| **Phase 5** | Search page (genre grid + search input) | Search filters results live |
| **Phase 6** | Library page (tabs + view toggle) | Library renders all items |
| **Phase 7** | Playlist + Artist detail pages | Dynamic routes render correctly |
| **Phase 8** | Zustand store + keyboard shortcuts | Full state wiring complete |
| **Phase 9** | Toast, Skeleton, Context Menu | Polish UI components working |
| **Phase 10** | Responsive QA at all breakpoints | No layout issues at 375–1440px |

---

## 17. Glossary

| Term | Definition |
|---|---|
| **SRS** | Software Requirements Specification |
| **SPA** | Single Page Application |
| **Vite** | Next-generation frontend build tool |
| **Zustand** | Lightweight React state management library |
| **Mock Data** | Hardcoded JavaScript objects simulating a real API |
| **Breakpoint** | A CSS viewport width threshold where layout changes |
| **FCP** | First Contentful Paint — time until first content renders |
| **CLS** | Cumulative Layout Shift — measure of visual stability |
| **ARIA** | Accessible Rich Internet Applications attributes |
| **WCAG** | Web Content Accessibility Guidelines |
| **TTI** | Time to Interactive — time until page is fully interactive |

---

*End of SRS Document — Version 1.0.0*  
*Last Updated: June 2026*
