[README.md](https://github.com/user-attachments/files/34851183/README.md)
# Momentum

A single-file personal dashboard — goals, habits, calorie/fitness tracking, a calendar with your roadmap, focus sessions with a website blocker, quick capture, and daily motivation — built as one self-contained HTML file with real cross-device sync via Supabase.

No build process, no framework, no backend server to maintain. Just one file.

---

## What's new (since September 2026)

- **New look** — a dark "operations console" design: graphite surfaces, hairline edges, Geist / Geist Mono type, one cyan accent for anything live or actionable
- **Works at every screen size** — full desktop, half-screen (icon rail), and a phone layout with a bottom tab bar and slide-out menu
- **Chrome forced-dark safe** — the page declares itself dark and redraws key lines as SVG, so Chrome's "Auto Dark Mode" flag can't wash it out
- **🎯 Focus** — a Pomodoro timer, confetti + notification when a block ends, and an optional browser extension that blocks distracting sites only during focus
- **📅 Calendar** (was *Deadlines*) — a TimeTree-style month view with continuous bars for sprints, goal windows and multi-day events; add your own one-off events
- **🛣 Roadmap editing** — add, edit, delete and auto-renumber sprints; new accounts get a generic, date-relative starter roadmap
- **🔥 Easier food logging** — one-tap "usuals", Enter reuses your own numbers, a "rough day" estimate instead of skipping, and honest *Untracked* days
- **🏋️ Exercise library** — your own exercises, groups and burn rates live in your data, with one-arm detection and automatic correction of past logs
- **Backups that are safer** — patches, "Undo last change", and Reset to default

---

## What's inside

### ◎ Today
Your home screen: greeting, an optional countdown, a **daily quote** from your own library, the Deep Focus goals scheduled for today, habit check-offs, and the nearest deadlines. On full-width screens it splits into two columns.

### 🌀 Flywheel
The daily driver. A 5-stage loop — **Capture → Clarify → Commit → Complete → Celebrate** — built around picking a small number of "Deep Focus" goals rather than holding your entire goal list in your head every day.

- Cap of 5 Deep Focus goals at a time
- Assign each one specific days of the week to work on it — shown as real calendar dates, not just weekday names
- Link a goal to an existing Habit (e.g. "Get a V-shape Body" → your Gym habit) so its status is pulled live from real tracked data instead of a second, disconnected checkbox
- A weekly review flow ("Turn the wheel") to reset your focus without losing anything — old notes get dumped into Capture, not deleted

### ✅ Goals
Every goal, organized by category, each with:
- A collapsible checklist of sub-steps
- **Finite / Infinite / Fixed / Long Term / Short Term** tagging — because a goal that never finishes (like "practice Leetcode") shouldn't be graded the same way as a goal with an actual end date (like "apply for NUS")
- Optional deadline **windows** (opens-on + closes-by), not just a single due date
- Drag-and-drop reordering and inline checklist editing
- **✎ Goal editor** — one dialog to change name, category, term, start date and deadline, with validation (start after end, missing dates)

### 🛣 Roadmap (sprints)
Sprints are goals in the **Roadmap** category with a start date, end date, checklist and a "daily time budget" note.
- **✎ Edit sprint** — name, dates (with a live "Window: 46 days" readout) and the daily time budget, one line per row
- **+ Add sprint** — pre-filled with the next number, starting the day after the last sprint ends
- **✕ Delete sprint** — asks first; later sprints **renumber themselves** so there are never gaps
- Each sprint is shown as **one self-contained card** — status strip, date range, length, countdown and progress bar all inside the same box, so dates can't be mistaken for the next sprint
- **New accounts** get a generic 4-sprint starter (6 weeks each), dated from the day of first login — nothing is hard-coded to a calendar date

### 🔥 Fuel
Calorie and fitness tracking, entirely offline (no external API needed).

**Meals**
- **Local food database** (including Singapore hawker staples) that estimates kcal / protein / carbs / fat — matched by keyword, with quantity and portion-size recognition
- **Your usuals** — your most-eaten foods as one-tap buttons, using the numbers from the last time you logged each one (recent habits weigh more; a food needs to be eaten at least twice to appear)
- **Enter uses your history** — typing a food you've logged before and pressing Enter reuses *your* corrected numbers; only new foods go through the estimator
- **Macros to one decimal place** (e.g. 12.5 g), with totals summed accurately
- **Rough day** — didn't log everything? Add the rest as a **Light / Normal / Heavy** estimate sized from your own typical meal. A rough day still counts toward your deficit
- Every logged number is editable inline; values typed in consecutive boxes are never lost

**Day types**

| Day | How it happens |
|---|---|
| Tracked | You logged meals |
| Rough | Part of the day is an estimate |
| Off day | You mark a **planned break** (holiday, celebration) — the app asks first |
| Untracked | Automatic: any past day with nothing logged |

The 14-day history shows an honest count (e.g. *"4 tracked · 1 rough · 1 off · 7 untracked"*), with a one-click option to convert old empty off days into untracked.

**Exercise**
- **Deterministic MET-based formula** — same inputs always give the same result: `MET × body weight × time` plus lifting work (`load × g × 0.5 m × reps ÷ 22% efficiency`)
- **＋ Exercises library** — add your own exercises, pick a type (heavy lower, compound upper, isolation, core, cardio light/moderate/hard, sport, mobility), group them (e.g. *Gym · Chest*, *Home*), search by name or group
- **Plurals understood** — "Curls" = "curl", "Rows" = "row", "Crunches" = "crunch"
- **One side at a time** — exercises named "One Arm …" / "Single-leg …" count both sides automatically; log reps for one side. Can be toggled per exercise
- Changing an exercise's type or side mode **corrects its past logs**, keeping the body weight you had when each was logged; hand-typed numbers are left alone
- Your **weekly training split** lives in your data, so today's exercises show first in the suggestions
- **BMI and body fat %** (US Navy method), a **calorie deficit calculator** (Mifflin–St Jeor), day navigation for back-filling past days

### 🔁 Habits
Daily check-off habits with streaks and an 18-week GitHub-style consistency heatmap. Includes one auto-tracked habit ("Calorie Deficit") that syncs itself from your real Fuel data — no manual checking required.

### 📅 Calendar (formerly Deadlines)
Three views, and the app remembers which one you last used:

- **List** — every dated goal with a real countdown, plus your sprint cards
- **Timeline** — a Gantt-style strip of goal deadlines, goal windows and sprints. Your own calendar events are **hidden by default**; a tick box brings them back
- **Calendar** — a Sunday-first month view, TimeTree-style:
  - **Continuous bars** for sprints, goal windows (opens-on → deadline, with a ⚑ on the due day) and multi-day events — bars wrap across weeks
  - Goal bars turn **amber** within 14 days and **red** when overdue
  - **Your own events** — tap a day to add one: name, type (**Event / Time off / Reminder / Personal**), optional time, optional end date for multi-day, and a note. Edit or delete from the day panel
  - Show/hide **My events · Deadlines · Sprints**; busy weeks collapse into "+N"
  - Planned off days are shaded with stripes

### 🎯 Focus
- **Pomodoro timer** — Focus → Short break → … → Long break every N blocks (defaults 25 / 5 / 15 / 4, all adjustable). Ring countdown, Start / Pause (Space), Reset, Skip
- **"Focusing on"** label per block, suggested from starred goals and current sprint items
- Survives reloads and tab switches — the time shows in the **tab title**, an emoji **favicon** (🧠 / 🎯 / ☕) and a pill in the sidebar
- When a block ends: **confetti**, a banner, a desktop **notification** and a chime (each can be turned off)
- **Stats** — blocks today, time focused, day streak, a 7-day chart and a log of today's blocks

**Website blocker (optional extension)**
A web page can't block other websites, so Momentum builds a small browser extension for you:
1. Focus → **⤓ Download blocker extension**, then unzip
2. Open `chrome://extensions`, turn on **Developer mode**, click **Load unpacked**, choose the `momentum-blocker` folder
3. Reload Momentum — the card should say **● Connected**

Once installed (Chrome, Edge, Brave, Arc):
- Sites on your list are blocked **only during focus blocks**; open tabs on those sites switch over when focus starts
- A polished **🎯 "Stay in the zone"** page shows the site name, a countdown ring, what you're focusing on, distractions blocked, and one of your own quotes; it switches to **🎉 break time** when the block ends
- It **unblocks itself** when you pause or the block ends, even if the Momentum tab is closed
- A toolbar icon with an **ON** badge and a status popup
- It's **locked to your copy of Momentum's address** — if you move hosting, re-download it

### 📥 Capture
A brain-dump space for anything on your mind. Park a worry, promote a thought into a real goal, or just clear your head.

### ❝ Quotes
A personal quote database you write into yourself — one shown per day, picked pseudo-randomly (stable for the whole day, changes automatically the next). Full editor with add/edit/delete. Long lists keep the background texture all the way down.

---

## Backup, patches & reset

Everything is under **Backup & sync** in the sidebar.

1. **Back up** — copy or download your whole state as JSON
2. **Restore** — paste or load a file:
   - a **full backup** (has a `goals` list) replaces everything
   - a **patch** (any other object) changes only the keys it names; a value sets that key, `null` removes it. Core data (goals, habits, meals, workouts, quotes…) can't be removed by a patch
3. **Reset to default** — *Reset roadmap only*, or *Reset everything…* (type `RESET` to confirm)

Before any restore, patch, reset or bulk correction, a copy is saved on that device and **↶ Undo last change** appears.

---

## Tech stack

- **Plain HTML/CSS/JavaScript** — no framework, no build step
- **[Supabase](https://supabase.com)** — free-tier Postgres database + auth, used for cross-device sync and realtime updates
- **[SortableJS](https://sortablejs.github.io/Sortable/)** (via CDN) — drag-and-drop reordering
- **[JSZip](https://stuk.github.io/jszip/)** (loaded on demand) — packaging the blocker extension
- **Google Fonts** — Geist and Geist Mono
- **localStorage** — local cache/fallback, plus device-only state (running timer, undo copy)
- **Chrome Manifest V3** (generated) — `declarativeNetRequest` rules for the blocker

---

## Hosting it yourself (free)

### 1. GitHub Pages
1. Create a public GitHub repo
2. Upload this file, renamed to `index.html`
3. Repo → **Settings → Pages** → Source: **Deploy from a branch**, branch `main`, folder `/ (root)`
4. Your site goes live at `https://yourusername.github.io/your-repo-name/`

After uploading a new version, hard-refresh (Ctrl/Cmd + Shift + R) on every device so none of them keeps running an old copy.

### 2. Supabase (for cross-device sync)
1. Create a free project at [supabase.com](https://supabase.com)
2. **Table Editor** → create a table `momentum_state` with columns:
   - `id` (default, auto)
   - `user_id` — type `uuid`
   - `data` — type `text`
   - `updated_at` — type `timestamptz`, default `now()`
3. Enable **Row Level Security** on the table, then in **SQL Editor** run:
   ```sql
   CREATE POLICY "Users manage their own data"
   ON momentum_state
   FOR ALL
   TO authenticated
   USING (auth.uid() = user_id)
   WITH CHECK (auth.uid() = user_id);

   ALTER TABLE momentum_state ADD CONSTRAINT unique_user_id UNIQUE (user_id);
   ```
4. **Project Settings → API** → copy your **Project URL** and **anon public key**
5. In the HTML file, find `SUPABASE_URL` and `SUPABASE_ANON_KEY` near the top of the `<script>` block and paste yours in
6. Re-upload to GitHub

The anon key is safe to ship in the page **only because** Row Level Security is on — double-check it in the Supabase dashboard.

### 3. First login
Open your live URL, **Sign Up** once with any email/password, then **Log In** with the same credentials on any other device to see the same data.

### 4. (Optional) Focus blocker
Open **Focus** on your live URL and download the extension from there, so it's locked to that address.

---

## How data flows

```
Any change (check a habit, log a meal, edit a goal)
        │
        ▼
   S (in-memory state object)
        │
   debounced 300ms
        │
        ▼
 ┌──────────────┬──────────────────┐
 │ localStorage │ Supabase (upsert)│  ← writes to YOUR row only, never a new one
 └──────────────┴──────────────────┘
        │
        ▼
 Realtime channel pushes the change
 to every other open device instantly
        │
        ▼
  Other device's screen updates live
  (no refresh needed)
```

If Supabase is unreachable, the app falls back to the local cache — you don't lose data, you just don't get the cross-device update until the connection's back.

**Synced vs device-only**

| Synced to your account (`S`) | This device only (localStorage) |
|---|---|
| Goals, sprints, habits, meals, workouts, body stats | The running Pomodoro timer |
| Calendar events (`S.reminders`), layer & view choices | The "Undo last change" copy |
| Training plan & exercise library (`S.training`) | |
| Focus settings, blocklist, focus history (`S.focus`) | |
| Quotes, captures, off days | |

The focus extension talks to the page through `window.postMessage`; it never reads your Momentum data beyond the blocklist, the current label, the end time and a few quotes for the blocked page.

---

## Project structure

It's one file. Everything — HTML, CSS, and JavaScript — lives in `index.html`. This is intentional: no build tooling, no dependencies to install, easy to host anywhere that serves static files, and easy to hand-edit directly in GitHub's web editor.

Rough internal layout, top to bottom:
1. `<head>` — styles (base → theme → polish → responsive → forced-dark safety net → feature styles), Supabase SDK
2. `<body>` — auth gate, then the app markup (sidebar nav, phone top/tab bars, one `<section class="panel">` per tab, modals)
3. `<script>` — persistence layer → state/seed data → render functions (one per tab) → event handlers → migrations → boot sequence

Theme colours and fonts are CSS variables in `:root` (`--deep`, `--text`, `--pencil` for the accent, `--display` / `--body` / `--mono`), so restyling is mostly a matter of changing those.

The whole app re-renders through a single central `render()` function every time state changes. Inline-editable fields check whether they currently have focus and skip rebuilding until you move on, and edits re-render on the next tick, so values typed into consecutive boxes are never dropped. The Pomodoro timer and calendar resize handling update their own DOM instead of triggering full renders.

---

## Migrations

The app uses a versioned-flag pattern for evolving saved data without breaking existing users — each one-time fix is gated behind `if(!S.someFlagV1){ ...; S.someFlagV1=true; }` in the boot sequence, so it runs exactly once per user. Brand-new accounts start with every flag already set.

Personal, one-off data (your own sprints, training split, etc.) is **not** hard-coded into the app — it lives in your data and is changed through the in-app editors or a patch file.

---

## Known limitations

- **Free-tier Supabase** has no built-in rate limiting beyond the platform defaults — fine for personal use, not built for many users
- **No password reset flow** is wired in yet — Supabase supports it, but the UI hasn't been built
- **Calorie estimates** (meals, exercise, rough days) are approximations — treat them as consistent ballparks, not exact figures
- **No offline-first conflict resolution** — if two devices both change data while out of sync, the last one to save wins; keep every device on the latest version
- **Background-tab timing** — browsers throttle background tabs, so a Pomodoro end notification can arrive up to about a minute late if Momentum isn't the active tab
- **Blocker** works in Chromium-based browsers only (not Safari or Firefox) and is installed manually in Developer mode
- **"Undo last change"** keeps only the most recent copy, on one device — use **Download file** for long-term backups
