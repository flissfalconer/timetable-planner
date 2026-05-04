# timetable-planner
A planner to support every one who is done with their life being a chaotic jumble and just needs something to be taking care of them!

# Find Your Space

**A free weekly timetable planner from [Study Beyond English](https://www.studybeyondenglish.com); built around your life, not the other way around.**

A self-contained HTML page that turns four lifestyle presets and a small set of optional preferences into a calmer, more realistic weekly timetable, with calendar export and gentle in-page nudges. No app store, no signup wall on the file itself, no build step. One file, any browser.

> *Transforming moments of anxiety into unshakeable foundations of confidence.*

---

## Live demo

`https://YOUR-NETLIFY-URL-HERE.netlify.app/`

(Replace once deployed; see [Deployment](#deployment) below.)

---

## What it does

Find Your Space is built for adults navigating busy lives where the day already has a shape before they get to it. Working parents, shift workers, work-from-home professionals, hybrid jugglers; anyone for whom a flat to-do list keeps quietly failing. The planner does not pretend the day is empty until you fill it; it starts with what is already true about your week (work hours, sleep, dependents, shift pattern) and lays the calm bits in around them, on purpose, before anything else can claim the slot.

### Features

| Feature | Detail |
|---|---|
| Persona presets | 9 to 5 working parent, shift worker, work-from-home professional, hybrid juggler |
| Shift handling | Per-day Early, Day, Late, Night presets, plus custom hours |
| Care commitments | Generic, rename-able blocks for school runs, hobby drop-offs and weekend commitments |
| Focus blocks | Two protected 90-minute focus windows per workday, notifications-off |
| Lunch | A 45-minute screen-free lunch that never silently shrinks |
| Wellbeing nudges | Hourly water reminders, two-hourly stand and stretch, optional digital detox before bed |
| Meal prep | A weekly meal-prep slot on the day that suits the persona |
| Exercise | Three movement slots a week, placed where the persona has energy |
| Weekly refresh | A 20-minute Sunday slot to review and update the week ahead |
| Day-zoom view | Tap any day for the hour-by-hour with per-event quick links |
| Calendar export | One-click `.ics` download with VALARM reminders for Apple Calendar, Google Calendar, Outlook, Fastmail |
| Per-event Google quick-add | Each event in the day-zoom has an "Add to Google Calendar" link |
| In-page toasts | Live nudges while the page is open, mirroring the calendar reminders |

### What it intentionally is not

Not a habit-tracker, not a productivity scoreboard, not a mood diary. There is no streak to lose, no leaderboard, no notification asking how you "did." The planner runs once, sets the rhythm, and steps out of the way.

---

## Screenshot

Add a hero screenshot here once the page is live; ideally one showing the persona picker and one showing the generated week.

---

## Quick start

The whole project is a single HTML file with no dependencies; you can run it without any tooling.

```bash
# 1. Clone the repo
git clone https://github.com/YOUR-USERNAME/find-your-space.git
cd find-your-space

# 2. Open in a browser
# Windows
start index.html
# macOS
open index.html
# Linux
xdg-open index.html
```

Or, simpler: download `index.html` from the repo and double-click it. There is no build step, no `npm install`, nothing to compile.

---

## Deployment

Pick whichever route suits you. All four are free for a freebie of this size.

### Option 1, Netlify (fastest)

1. Open [netlify.com/drop](https://netlify.com/drop).
2. Drag `index.html` onto the drop zone.
3. Netlify gives you a public URL inside thirty seconds.
4. Click "Claim site" and create a free account if you want the URL to last beyond 24 hours.

### Option 2, GitHub Pages

1. Push this repo to GitHub.
2. In **Settings → Pages**, set the source to `main` branch, root.
3. GitHub publishes the site at `https://YOUR-USERNAME.github.io/find-your-space/`.
4. Custom domain optional; configure under the same Pages settings.

### Option 3, Cloudflare Pages

1. Connect this repo at [pages.cloudflare.com](https://pages.cloudflare.com).
2. Build command: leave empty.
3. Build output directory: `/`.
4. Cloudflare gives you a `*.pages.dev` URL with a free SSL certificate and Cloudflare's CDN out of the box.

### Option 4, Vercel

1. Import this repo at [vercel.com/new](https://vercel.com/new).
2. Framework preset: "Other".
3. Vercel gives you a `*.vercel.app` URL on the next push.

---

## File structure

```
find-your-space/
├── index.html         # The planner; one self-contained file with HTML, CSS, JS inline
├── README.md          # This file
└── LICENSE            # MIT license for the code (see Licensing notes below)
```

Internal SBE materials (landing-page copy, welcome email, automation specs, printable one-pager) live outside this repository.

---

## How it works

The page is vanilla HTML, CSS and JavaScript; no frameworks, no bundler, no third-party scripts at runtime.

| Layer | What it does |
|---|---|
| `PERSONAS` object | Holds the four preset baselines (work hours, wake / sleep, care defaults, exercise days, meal-prep day) |
| `SHIFT_PRESETS` object | Defines Early, Day, Late, Night presets the user can apply per day |
| `generateSchedule(cfg)` | Reads the form, walks each day, and lays in blocks for sleep, meals, work, focus, lunch, breaks, care, exercise, detox and refresh |
| `buildICS()` | Produces an RFC 5545-compliant `.ics` calendar file with `VALARM` reminders, line-folded to 75 characters |
| `googleCalendarLink(event, baseDate)` | Builds an `https://calendar.google.com/calendar/render?action=TEMPLATE&...` URL for per-event quick-add |
| `startInPageNudges()` | Sets `setInterval` timers for water, movement and the weekly refresh check |

There is no backend, no analytics, no cookies, no user accounts and no data leaves the user's browser.

---

## Customising

A few of the most common edits, with file locations.

### Change the persona defaults

In `index.html`, find the `PERSONAS` object near the top of the `<script>` block. Each persona has work hours, wake / sleep, care commitment defaults, exercise days and a meal-prep day. Edit any of these to seed a different baseline.

### Change the colour palette

The page uses CSS custom properties for the SBE calm sub-palette. They sit at the top of the `<style>` block as `:root` variables; change `--sbe-purple`, `--lilac`, `--blush`, etc., and every block inherits the new palette.

### Change the wellbeing rule defaults

Inside the deep-dive `<details>` panel for "Wellbeing rules," each toggle has a default `checked` attribute and an associated input for time or duration. Change the defaults in the HTML if you want a different out-of-the-box behaviour.

### Add a new persona

1. Add a new entry to the `PERSONAS` object with the same shape as the existing four.
2. Add a new `<button class="persona" data-persona="your-key">` block in the markup, with an icon, a heading and one paragraph of copy.

### Localise

All user-facing strings are inline. UK English is the default; replace strings in place if you need a different locale. The .ics generator uses floating local time (no `Z` suffix), so calendar apps render the events at the user's wall-clock time wherever they import.

---

## Browser support

Tested on current Chrome, Edge, Firefox, Safari (desktop and iOS). The page uses standard HTML5, CSS Grid, Flexbox and ES2017 JavaScript; no IE support, no transpilation, no polyfills.

---

## Roadmap

A few ideas worth picking up if anyone wants to extend the project.

- **Per-child hobby slots** as an opt-in deep-dive panel beyond the current generic care blocks.
- **Refresh diff view** that highlights what changed between the last generated week and the current one.
- **Print-friendly week view** with a one-page A4 layout.
- **Optional dark theme** for shift workers who use the planner late at night.
- **Localised templates** for non-UK users (different default working hours, weekend conventions).

These are nice-to-haves; the planner is fully usable as-is.

---

## Built by

Find Your Space is built and maintained by [Fliss Falconer](mailto:hello@studybeyondenglish.com), Founder and Creative Director of [Study Beyond English](https://www.studybeyondenglish.com). It sits alongside SBE's other free, student-facing and adult-facing resources; the work is funded by schools using the paid SBE tools, including [EchoGuide](https://www.echoguidetheatre.com), an accessibility-first rehearsal tool for speaking and listening tasks.

Strategic generosity is how SBE works; everything aimed at students and individuals stays free at the point of use.

---

## License

The code in this repository is released under the **MIT License**; see `LICENSE` for the full text. You are welcome to fork, modify and self-host for any purpose.

The **Study Beyond English** name, logo, brand colours, the SBE wordmark, the "Find Your Space" wordmark, and any associated illustration assets are not covered by the MIT License and remain the property of Study Beyond English. If you fork the project for your own use, please replace the SBE branding with your own, or email hello@studybeyondenglish.com if you want to discuss a different arrangement.

If you would prefer a different license for the code (for example Creative Commons Attribution-NonCommercial 4.0, or All Rights Reserved), update `LICENSE` to match before publishing the repo.

---

## Contact

Issues and pull requests are welcome; for anything else, write to [hello@studybeyondenglish.com](mailto:hello@studybeyondenglish.com).

🌸 📚 🐾 🖥️ ✒️ ☕ 🌸

