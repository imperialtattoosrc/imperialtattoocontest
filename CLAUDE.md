# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **single-file static landing page** (`index.html`) for the Imperial Tattoo Contest 2026 — a tattoo competition and Miss Tattoo pageant held at Centro Cultural Vento Solar, São Cristóvão, Rio de Janeiro.

## No Build Process

There is no build system, package manager, or framework. To preview the site, open `index.html` directly in a browser. All dependencies are loaded via CDN.

## Dependencies (all via CDN)

- **Tailwind CSS** — loaded via `<script src="https://cdn.tailwindcss.com">` with inline `tailwind.config` for custom colors
- **Google Fonts** — Montserrat and Playfair Display
- **Font Awesome 6.4.0** — icons
- **Google Gemini API** — `gemini-2.5-flash-preview-09-2025` model, called client-side via `fetchGeminiAPI()`

## Custom Tailwind Color Palette

Defined inline in `tailwind.config`:
- `imperial-gold` → `#D4AF37`
- `imperial-goldlight` → `#F3E5AB`
- `imperial-red` → `#8B0000`
- `imperial-dark` → `#0a0a0a`
- `imperial-gray` → `#1a1a1a`

Also `.text-gradient-gold` is a custom CSS class (not a Tailwind utility) defined in `<style>`.

## AI Features

Two Gemini-powered features share the `fetchGeminiAPI(prompt, systemInstruction)` helper (with 5-retry exponential backoff):

1. **Bio Enhancer** (`#btnEnhanceBio`) — rewrites the Miss Tattoo candidate's bio draft into an empowered "rock n' roll" manifesto, replacing the textarea value in-place.
2. **Oráculo da Agulha** (`#btnGenerateIdea`) — generates a tattoo concept and recommends a competition category based on the user's personality description; renders HTML into `#aiResultText`.

The `apiKey` constant at the top of the script block is intentionally empty (`""`); it must be injected at deploy time or filled in locally.

## Page Sections (by anchor)

| Anchor | Section |
|---|---|
| `#sobre` | About the event |
| `#misstattoo` | Miss Tattoo highlight + registration link (Google Forms) |
| `#inscricao` | Pre-registration form with AI bio enhancer |
| `#categorias` | Tattoo competition categories |
| `#oraculo` | AI tattoo idea generator |
| `#organizador` | Organizer bio (Silvio RC) |

## Key Details

- Content is in Brazilian Portuguese.
- The Miss Tattoo registration button links to an external Google Forms URL.
- The pre-registration form (`#missForm`) does **not** submit to a backend — `onsubmit` just triggers the custom modal.
- The custom modal (`#customModal`) replaces `alert()` for all user notifications.
