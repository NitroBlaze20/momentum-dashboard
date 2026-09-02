[Uploading README.md…]()
# Momentum

A single-file personal dashboard — goals, habits, calorie/fitness tracking, deadlines, quick capture, and daily motivation — built as one self-contained HTML file with real cross-device sync via Supabase.

No build process, no framework, no backend server to maintain. Just one file.

---

## What's inside

### 🌀 Flywheel (home)
The daily driver. A 5-stage loop — **Capture → Clarify → Commit → Complete → Celebrate** — built around the idea of picking a small number of "Deep Focus" goals rather than trying to hold your entire goal list in your head every day.

- Cap of 5 Deep Focus goals at a time
- Assign each one specific days of the week to work on it — shown as real calendar dates, not just weekday names
- Link a goal to an existing Habit (e.g. "Get a V-shape Body" → your Gym habit) so its status is pulled live from real tracked data instead of a second, disconnected checkbox
- A weekly review flow ("Turn the wheel") to reset your focus without losing anything — old notes get dumped into Capture, not deleted

### ✅ Goals
Every goal, organized by category, each with:
- A collapsible checklist of sub-steps
- **Finite / Infinite / Fixed / Long Term / Short Term** tagging — because a goal that never finishes (like "practice Leetcode") shouldn't be graded the same way as a goal with an actual end date (like "apply for NUS")
- Optional deadline **windows** (opens-on + closes-by), not just a single due date — for things like applications that can only be submitted within a specific period
- Drag-and-drop reordering, inline title/checklist editing

### 🔥 Fuel
Calorie and fitness tracking, entirely offline (no external API needed):
- **Meal logging** with a local food database (including Singapore hawker staples) that estimates kcal/protein/carbs/fat automatically — matched by keyword, with quantity and portion-size ("large", "half") recognition
- **Meal autocomplete** — surfaces meals you've logged before, ranked by frequency and recency, reusing your last-corrected macros
- **Exercise tracking** with a deterministic MET-based calorie formula (same inputs always produce the same result — no AI guessing) covering weighted lifts, timed cardio, and a dedicated sport-logging widget; exercise autocomplete also surfaces today's split from your own hardcoded weekly workout plan, so you can tap an exercise instead of typing it
- **BMI and body fat %** (US Navy method) calculated live from your profile stats
- A **calorie deficit calculator** (Mifflin–St Jeor) with a 14-day history strip, paginated to view older weeks, color-coded (green = deficit, red = surplus, yellow = marked "off day")
- Every logged number (calories, protein/carbs/fat, exercise kcal) is manually editable inline — tap the field, tap the value, type over it
- Day navigation — log for today, or go back and fill in a past day

### 🔁 Habits
Daily check-off habits with streaks and an 18-week GitHub-style consistency heatmap. Includes one auto-tracked habit ("Calorie Deficit") that syncs itself from your real Fuel data — no manual checking required.

### ⏰ Deadlines
Every dated goal in one place, with a real countdown — including support for goals that aren't due yet but also can't be started before a certain date — plus standalone reminders you add yourself (a single day, or a window if it spans a range) for anything that isn't tied to a goal.

### 📥 Capture
A brain-dump space for anything on your mind. Park a worry, promote a thought into a real goal, or just clear your head.

### ❝ Quotes
A personal quote database you write into yourself — one shown per day, picked pseudo-randomly (stable for the whole day, changes automatically the next). Full editor with add/edit/delete.

---

## Tech stack

- **Plain HTML/CSS/JavaScript** — no framework, no build step
- **[Supabase](https://supabase.com)** — free-tier Postgres database + auth, used for cross-device sync and realtime updates
- **[SortableJS](https://sortablejs.github.io/Sortable/)** (via CDN) — drag-and-drop reordering
- **localStorage** — local cache/fallback so the app still works offline or if the network hiccups

---

## Hosting it yourself (free)

### 1. GitHub Pages
1. Create a public GitHub repo
2. Upload this file, renamed to `index.html`
3. Repo → **Settings → Pages** → Source: **Deploy from a branch**, branch `main`, folder `/ (root)`
4. Your site goes live at `https://yourusername.github.io/your-repo-name/`

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

### 3. First login
Open your live URL, **Sign Up** once with any email/password, then **Log In** with the same credentials on any other device to see the same data.

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

If Supabase is unreachable, the app falls back to the local cache — you never lose data, you just don't get the cross-device update until the connection's back.

---

## Project structure

It's one file. Everything — HTML, CSS, and JavaScript — lives in `index.html`. This is intentional: no build tooling, no dependencies to install, easy to host anywhere that serves static files, and easy to hand-edit directly in GitHub's web editor if you don't want to set up a local dev environment.

Rough internal layout, top to bottom:
1. `<head>` — styles, Supabase SDK
2. `<body>` — auth gate, then the full app markup (sidebar nav + one `<section class="panel">` per tab)
3. `<script>` — persistence layer → state/seed data → render functions (one per tab) → event handlers → migrations → boot sequence

The whole app re-renders through a single central `render()` function every time state changes, rather than patching individual DOM nodes. `render()` preserves whatever input field currently has focus (and its cursor position/scroll offset) across the rebuild, so editing inline numbers — calories, macros, body-metric fields — doesn't kick you out of the field mid-keystroke.

---

## Migrations

The app uses a simple versioned-flag pattern for evolving saved data without breaking existing users — each one-time fix or data restructure is gated behind `if(!S.someFlagV1){ ...; S.someFlagV1=true; }` in the boot sequence, so it runs exactly once per user, ever, regardless of when they next open the app.

---

## Known limitations

- **Free-tier Supabase** has no built-in rate limiting protection beyond the platform defaults — fine for personal use, not built for many users
- **No password reset flow** is wired in yet — Supabase supports it, but the UI for it hasn't been built
- **Meal/exercise calorie estimates** are approximations (keyword-matched database / fixed MET formulas), not lab-measured — treat them as consistent ballparks, not exact figures
- **No offline-first conflict resolution** — if two devices go offline and both make changes, the last one to reconnect and save wins; there's no merge logic
