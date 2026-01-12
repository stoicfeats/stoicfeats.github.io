---
title: "harvester"
date: 2026-01-12T23:24:00+05:30
level: "intermediate"
draft: false
project_url: "https://x-marks.space"
---

## technical notes

### core architecture
- **frontend**: react 18 + typescript + vite.
- **styling**: tailwind css with dark/light mode support.
- **backend**: firebase (auth + firestore + hosting).
- **state**: local react state + custom hooks.

### features & implementation

#### 1. data ingestion
- **logic**: specialized interface for browsing archived tweet json payloads.
- **methods**: drag-and-drop or manual entry of data streams.
- **normalization**: layer to handle various archive formats.

#### 2. visual processing
- **masonry layout**: high-density grid with adjustable columns (1-5x).
- **filtering**: real-time segmentation (media, threads, favorites).
- **dynamic display**: adaptive cards with media previews and interaction stats.

#### 3. utility tools
- **scraper utility**: integrated generator for client-side scraping scripts.
- **local storage**: automatic persistence for guest users.

#### 4. authentication & sync
- **provider**: firebase auth (google login).
- **storage**: firestore for user preferences and "starred" tweets.
- **sync**: real-time updates across devices.

#### 5. user interface
- **aesthetic**: brutalist/neumorphic design prioritizing data density.
- **animation**: framer motion for smooth transitions and layout changes.
- **responsive**: mobile-friendly design with optimized grid views.

#### 6. bookmark management
- **starring**: allow users to bookmark specific tweets for quick access.
- **filtering**: dedicated filter for viewing all starred or high-engagement content.
