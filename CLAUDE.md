# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic website for a Brazilian CS professor. Single-page static site hosted on GitHub Pages. Reference aesthetic: minimalist, editorial, warm (inspired by moritzoesterlau.de).

## Architecture

- **No build tools, no frameworks, no npm.** Pure HTML + CSS + vanilla JS.
- Everything lives in a single `index.html` file: HTML structure, `<style>` block, `<script>` block.
- The site must work by opening `index.html` directly in a browser.
- Fonts: Google Fonts CDN only (Fraunces or Cormorant Garamond for display, DM Sans or Plus Jakarta Sans for body, JetBrains Mono or IBM Plex Mono for code). No system fonts.

## Key Design Constraints

- **Bilingual:** EN-US (primary) and PT-BR. All visible text must switch via a language toggle.
- **Light/Dark mode:** All colors as CSS custom properties (`--color-*`). Zero hardcoded hex values. Theme switches via `data-theme` attribute on `<html>`. Must be instant and bug-free.
- **Responsive:** Desktop, tablet, mobile. Navbar collapses to hamburger on `< 700px`.
- **Animations:** All respect `prefers-reduced-motion`. Staggered reveal on load, IntersectionObserver scroll reveals, smooth theme/language transitions.

## Color System

Light mode base: `#F7F6F3` background, `#181715` text. Dark mode base: `#111110` background, `#EDEBE6` text. Every color role (surface, card, border, status badges, etc.) must have both light and dark variants defined as CSS custom properties under `:root` and `[data-theme="dark"]`.

## Layout Constants

- Max content width: `860px` centered
- Navbar: `64px` height, fixed, frosted-glass on scroll
- Hero: `160px` circular photo, `padding-top: 5rem` (breathing room from navbar)
- Section padding: `6rem 0` desktop, `3.5rem 0` mobile
- Card padding: `1.25rem 1.5rem`, border-radius `8px`, borders `0.5px solid`

## Sections (in order)

Home (hero with photo + bio + social links) → Research (project cards grid) → Publications (grouped by year, manually maintained) → Teaching (course cards grid) → Students (current + alumni) → Resources (linked cards) → Contact (info card) → Footer.

## File Structure

```
/
├── index.html    ← all HTML, CSS, and JS
├── photo.jpg     ← profile photo
├── README.md     ← design brief
└── CLAUDE.md
```
