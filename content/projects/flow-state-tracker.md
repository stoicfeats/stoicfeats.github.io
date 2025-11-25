---
title: "flow state tracker"
date: 2025-11-25T09:00:00+05:30
level: "beginner"
draft: false
---

## technical notes

### core architecture
- **frontend**: react + typescript + vite.
- **styling**: tailwind css with dark/light mode support.
- **backend**: supabase (auth + database).
- **state**: local react state + custom hooks.

### features & implementation

#### 1. focus timer
- **logic**: custom `usetimer` hook using `requestanimationframe` for drift-free timing.
- **persistence**: saves state to `localstorage` to handle page reloads.
- **modes**: standard timer and "flow" mode (stopwatch style).

#### 2. audio system
- **tech**: native web audio api (no external libraries).
- **sound**: synthetic "soft bell" (sine wave @ 523hz with exponential decay).
- **trigger**: fires on timer completion via `useeffect`.

#### 3. authentication
- **provider**: supabase auth.
- **method**: passwordless email (magic link), google auth will be enabled soon.
- **security**: row level security (rls) enabled on database tables.

#### 4. data layer
- **storage**: supabase postgresql.
- **tables**:
    - `sessions`: tracks duration and timestamp of work blocks.
    - `notes`: stores user thoughts/todos.
    - `feedback`: captures user suggestions ("kaizen").
- **sync**: real-time state updates upon successful db writes.

#### 5. user interface
- **framework**: mobile-first responsive design.
- **animation**: framer motion for smooth transitions (modals, theme toggle).
- **components**: modular architecture (`timer`, `stats`, `history`, `feedbackmodal`).

#### 6. feedback system ("kaizen")
- **ui**: modal with validation (min 10 chars).
- **flow**: user submits -> writes to db -> auto-closes with success animation.
