## Personal Academic Website — Design Brief

### Overview

A single-page static website for a Brazilian Computer Science professor, hosted on GitHub Pages. The site must balance academic credibility with modern, refined design. The reference aesthetic is the portfolio of Moritz Oesterlau (moritzoesterlau.de): minimalist, editorial, clean typography, circular photo on the left, text on the right, subtle use of emoji.

---

### Content Sections (in order)

**1. Home (Hero)**
Circular profile photo on the left; text on the right. Content: full name, title, institutional affiliation, a 2–3 sentence bio, a tagline summarizing research areas (Edge–Cloud Continuum, Agentic AI, CS Education), and icon-links to Google Scholar, ORCID, LinkedIn, and GitHub.

**2. Research**
Two columns of project cards. Each card has a status badge (Ongoing / Completed), a project title, and a 2-sentence description. Below the grid, a "Collaboration interests" text block.

**3. Publications**
Grouped by year (descending). Each entry has a type badge (J = Journal, C = Conference), paper title, venue, author list, and inline links (PDF, DOI, Scholar). A note at the bottom explains that Google Scholar direct embedding is not supported in fully static sites; the list is manually maintained. The note links to the author's Google Scholar profile.

**4. Teaching**
Two-column grid of course cards. Each card shows level (Undergraduate / Graduate), course name, and department code.

**5. Students**
Two groups: Current Students and Alumni. Each entry shows a colored dot (green = active, gray = alumni), student name, degree level (BSc / MSc / PhD), and research topic. Alumni entries also show graduation year.

**6. Resources**
Vertical list of clickable cards linking to GitHub repositories and tools. Each card has an icon, tool name, and a one-sentence description.

**7. Contact**
A contained card with email (institutional), office room, building, campus, and full university address.

**Footer**
Copyright line and "Built with HTML/CSS · Hosted on GitHub Pages."

---

### Functional Requirements

| Feature         | Specification                                                                                      |
| --------------- | -------------------------------------------------------------------------------------------------- |
| Architecture    | Single-page; all sections on one HTML file                                                         |
| Navigation      | Fixed top navbar; smooth scroll to sections; active section highlighted                            |
| Bilingual       | EN-US (primary) and PT-BR toggle; all visible text must switch                                     |
| Responsive      | Desktop, tablet, and mobile (navbar collapses on mobile)                                           |
| Light/Dark mode | Toggle button; full theme switch with no visual bugs (no white text on white background, no flash) |
| Hosting         | GitHub Pages; no build step; pure HTML + CSS + vanilla JS                                          |

---

### Typography

**Problem with previous version:** Generic serif (Georgia) felt dated and low-effort.

**Direction:** A modern, elegant, slightly editorial type pairing. Suggestions:

- Display / headings: **Fraunces** (Google Fonts) — optical-size variable font, warm, sophisticated; or **Cormorant Garamond** for a more classical feel.
- Body: **DM Sans** or **Plus Jakarta Sans** — geometric, clean, highly legible at small sizes.
- Monospace (code snippets, badges): **JetBrains Mono** or **IBM Plex Mono**.

All fonts via Google Fonts CDN. No system fonts (Arial, Georgia, Times New Roman) anywhere on the page.

---

### Color Palette

**Light mode**

| Role                       | Value                      |
| -------------------------- | -------------------------- |
| Page background            | `#F7F6F3` (warm off-white) |
| Surface / cards            | `#FFFFFF`                  |
| Subtle surface             | `#EFEFEB`                  |
| Primary text               | `#181715`                  |
| Secondary text             | `#5C5A55`                  |
| Tertiary / muted           | `#9A9890`                  |
| Borders                    | `rgba(0,0,0,0.08)`         |
| Accent (links, active nav) | `#181715`                  |
| Status — ongoing           | `#2E7D32` on `#E8F5E9`     |
| Status — completed         | `#5C5A55` on `#EFEFEB`     |

**Dark mode**

| Role               | Value                    |
| ------------------ | ------------------------ |
| Page background    | `#111110`                |
| Surface / cards    | `#1C1B19`                |
| Subtle surface     | `#242320`                |
| Primary text       | `#EDEBE6`                |
| Secondary text     | `#A8A49E`                |
| Tertiary / muted   | `#6B6762`                |
| Borders            | `rgba(255,255,255,0.08)` |
| Accent             | `#EDEBE6`                |
| Status — ongoing   | `#81C784` on `#1B3A1C`   |
| Status — completed | `#A8A49E` on `#242320`   |

**Critical dark mode rule:** Every color must be defined as a CSS custom property (`--color-*`). Zero hardcoded hex values in component CSS. The theme switch must be instant and bug-free — achieved by toggling a `data-theme` attribute on `<html>` and defining all variables under `[data-theme="dark"]`.

---

### Spacing & Layout

- Max content width: `860px`, centered.
- Section vertical padding: `6rem 0` (desktop), `3.5rem 0` (mobile).
- Navbar height: `64px`. Content below hero must clear the sticky navbar.
- Hero: photo `160px` diameter; gap between photo and text `3rem`; bottom margin before first section `2rem`.
- **Hero–navbar gap problem (from previous version):** The hero section felt cramped under the navbar. Fix: add `padding-top: 5rem` to the hero section to create explicit breathing room between the navbar and the profile content.
- Card internal padding: `1.25rem 1.5rem`.
- Grid gap: `1rem` (cards), `0.75rem` (course items).
- Border radius: `8px` (cards, buttons), `50%` (photo), `4px` (badges/tags).
- All borders: `0.5px solid` using the border color variables above.

---

### Buttons & Interactive Elements

**Problem with previous version:** Buttons were plain and visually uninteresting — simple bordered rectangles with no personality.

**Direction:** Buttons should feel tactile and refined. Specific treatments:

- **Language toggle (EN / PT):** Pill-shaped toggle switch, not two separate buttons. Active language has a filled background; inactive is ghost. Smooth transition on switch.
- **Theme toggle (Light / Dark):** Icon-only button (sun ☀ / moon ☾ SVG icons, not emoji). No label text. Circular button, `36px` diameter, subtle border.
- **Social links (Scholar, ORCID, LinkedIn, GitHub):** Horizontal row of pill buttons. Each has a small SVG icon on the left and a text label. On hover: background fills to `--color-subtle`, border darkens, slight upward translate (`translateY(-1px)`). No underline.
- **Publication links (PDF, DOI, Scholar):** Small inline pill tags. Font size `11px`. On hover: background and border transition smoothly. Should not look like hyperlinks — they should look like tags/chips.
- **All hover states:** Use `transition: all 0.18s ease` consistently. No abrupt changes.

---

### Animations

**Problem with previous version:** Animations were either absent or simplistic — scroll-triggered highlighting only.

**Direction:** Subtle, purposeful motion that feels fluid and premium, not decorative. All animations must respect `prefers-reduced-motion`.

Specific animations to implement:

1. **Page load — staggered reveal:** Each section fades in and slides up `16px` on page load. Stagger delay increases by `80ms` per section. Use CSS `@keyframes` with `animation-delay`. Duration: `500ms`, easing: `cubic-bezier(0.16, 1, 0.3, 1)` (expo-out).

2. **Navbar — scroll appearance:** On page load, navbar is fully transparent with no border. After scrolling `40px`, it transitions to the frosted-glass state (`backdrop-filter: blur(10px)` + background opacity). Duration: `300ms ease`.

3. **Card hover:** Cards lift slightly (`translateY(-2px)`) and border darkens on hover. Duration: `180ms ease-out`. No box-shadow (conflicts with flat design direction).

4. **Section scroll reveal:** Use `IntersectionObserver`. Elements (cards, list items, pub entries) animate in with `opacity: 0 → 1` and `translateY(12px → 0)` as they enter the viewport. Stagger children by `60ms`. This replaces the simplistic "everything loads at once" behavior.

5. **Theme toggle:** Color transitions use `transition: background-color 0.25s ease, color 0.25s ease, border-color 0.25s ease` on all elements. No flash. The transition must feel like a smooth temperature shift, not a hard switch.

6. **Language switch:** Text content swaps with a brief `opacity: 0 → 1` crossfade (`150ms ease`). Prevents jarring content jump.

7. **Active nav indicator:** The underline indicator slides horizontally between nav items on hover/scroll using a `::after` pseudo-element with `transition: left/width 0.2s ease`.

---

### Navigation

- Fixed top, full width.
- Left: author name (display font, `15px`).
- Center: nav links (sans-serif, `13px`, uppercase, letter-spacing `0.06em`). Active link: full-opacity + animated underline. Inactive: `60%` opacity.
- Right: language toggle (pill) + theme toggle (icon button).
- On mobile (`< 700px`): center and right collapse into a hamburger menu. Nav links appear as a full-width dropdown with `backdrop-filter`.

---

### Known Issues to Fix (from previous prototype)

1. **White text on white background in dark mode** — caused by hardcoded colors not covered by the theme variables. Fix: audit every CSS rule; zero hardcoded colors.
2. **Status badges in dark mode** — green-on-light-green became unreadable. Fix: define separate dark-mode values for badge background and text.
3. **Publication type badges (J/C)** — same issue. Define explicit dark-mode colors.
4. **Navbar active state** — the `border-bottom` highlight disappeared in dark mode. Fix: use `border-bottom-color: var(--color-text-primary)`.
5. **Hero section cramped under navbar** — see spacing section above.

---

### File Structure (for GitHub Pages)

```
/
├── index.html       ← single file with all HTML, CSS (in <style>), and JS (in <script>)
├── photo.jpg        ← profile photo (replace the placeholder avatar)
└── README.md
```

No build tools, no frameworks, no npm. Pure HTML/CSS/JS. All fonts loaded from Google Fonts CDN. The entire site must work by opening `index.html` directly in a browser.

---

### Tone & Reference

The site should feel like the personal page of a serious researcher who also cares about craft. Not a corporate page. Not a university template. Clean, modern, a little warm. Similar in spirit to: Moritz Oesterlau's portfolio, Fabian Schultz's site, and the academic pages of researchers at top systems groups (MIT CSAIL, CMU PDL, EPFL LABOS).
