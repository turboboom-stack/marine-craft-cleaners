# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

# Frontend Website Rules

## Always Do First
- **Invoke the `frontend-design` skill** before writing any frontend code, every session, no exceptions.

## Reference Images
- If a reference image is provided: match layout, spacing, typography, and color exactly. Swap in placeholder content (images via `https://placehold.co/`, generic copy). Do not improve or add to the design.
- If no reference image: design from scratch with high craft (see guardrails below).
- Screenshot your output, compare against reference, fix mismatches, re-screenshot. Do at least 2 comparison rounds. Stop only when no visible differences remain or user says so.

## Local Server
- **Always serve on localhost** — never screenshot a `file:///` URL.
- Start the dev server: `node serve.mjs` (serves the project root at `http://localhost:3000`)
- `serve.mjs` lives in the project root. Start it in the background before taking any screenshots.
- If the server is already running, do not start a second instance.

## Screenshot Workflow
- Chrome cache is at `/Users/jordan/.cache/puppeteer/`.
- **Always screenshot from localhost:** `node screenshot.mjs http://localhost:3000`
- Screenshots are saved automatically to `./temporary screenshots/screenshot-N.png` (auto-incremented, never overwritten).
- Optional label suffix: `node screenshot.mjs http://localhost:3000 label` → saves as `screenshot-N-label.png`
- `screenshot.mjs` lives in the project root. Use it as-is.
- After screenshotting, read the PNG from `temporary screenshots/` with the Read tool — Claude can see and analyze the image directly.
- When comparing, be specific: "heading is 32px but reference shows ~24px", "card gap is 16px but should be 24px"
- Check: spacing/padding, font size/weight/line-height, colors (exact hex), alignment, border-radius, shadows, image sizing

## Output Defaults
- Single `index.html` file, all styles inline, unless user says otherwise
- Tailwind CSS via CDN: `<script src="https://cdn.tailwindcss.com"></script>`
- Placeholder images: `https://placehold.co/WIDTHxHEIGHT`
- Mobile-first responsive

## Brand Assets
- Always check the `assets/` folder before designing. It may contain logos, color guides, style guides, or images.
- If assets exist there, use them. Do not use placeholders where real assets are available.
- If a logo is present, use it. If a color palette is defined, use those exact values — do not invent brand colors.

## Anti-Generic Guardrails
- **Colors:** Never use default Tailwind palette (indigo-500, blue-600, etc.). Pick a custom brand color and derive from it.
- **Shadows:** Never use flat `shadow-md`. Use layered, color-tinted shadows with low opacity.
- **Typography:** Never use the same font for headings and body. Pair a display/serif with a clean sans. Apply tight tracking (`-0.03em`) on large headings, generous line-height (`1.7`) on body.
- **Gradients:** Layer multiple radial gradients. Add grain/texture via SVG noise filter for depth.
- **Animations:** Only animate `transform` and `opacity`. Never `transition-all`. Use spring-style easing.
- **Interactive states:** Every clickable element needs hover, focus-visible, and active states. No exceptions.
- **Images:** Add a gradient overlay (`bg-gradient-to-t from-black/60`) and a color treatment layer with `mix-blend-multiply`.
- **Spacing:** Use intentional, consistent spacing tokens — not random Tailwind steps.
- **Depth:** Surfaces should have a layering system (base → elevated → floating), not all sit at the same z-plane.

## Hard Rules
- Do not add sections, features, or content not in the reference
- Do not "improve" a reference design — match it
- Do not stop after one screenshot pass
- Do not use `transition-all`
- Do not use default Tailwind blue/indigo as primary color
- **Never use em dashes (—) anywhere in content, copy, or UI text.** Use periods, commas, or colons instead.

---

## Project Overview

Marine Craft Cleaners is a solo mobile boat cleaning/detailing service based in Vero Beach, Florida (Treasure Coast). This repository contains business planning, assets, and automation tooling for building and operating the business.

## Business Context

- **Owner**: Jordan
- **Service area**: Treasure Coast (Vero Beach, Fort Pierce, Stuart, Port St. Lucie, Jupiter)
- **Competitor**: Topside Boat Cleaning (Phil Flower, 772-321-2324) — minimal online presence, no booking, no pricing

## Planned Stack

- **Website**: WordPress (not Webflow)
- **Booking**: Online booking with instant confirmation
- **CRM**: Customer history and automated follow-ups
- **Review system**: Automated post-service review requests

## Assets

- `/assets/MCC Logo.jpeg` — primary brand logo

---

## Owner Voice & Brand Personality

**Who Jordan is:**

- Grew up in Michigan on boats constantly — family boats, friends' boats, always on the water
- Worked at **Grand Bay Marine**: cleaned boats, did winterization, repairs, and sales — full shop experience
- Now running MCC solo in Vero Beach, bringing that lifetime of experience to every job

**Core belief:** Cleanliness is next to godliness. A clean space means ease, happiness, and prosperity. This isn't just a job — it's a calling.

**The MCC difference:** Jordan goes the extra mile because cleaning a boat is more than a chore. It's making sure you feel and look amazing on the water.

**Tone for all copy — DO:**

- Lead with the feeling or transformation, not the task list
- Say "your boat," not "the vessel" or "your watercraft"
- Short, punchy sentences. Real talk. Like a person who loves what they do.
- Reference the owner's personal story and passion when it fits
- Emphasize how a clean boat = confidence, pride, better time on the water

**Tone for all copy — AVOID:**

- "Industry-leading," "premium solutions," "comprehensive services"
- Corporate/generic language
- Long lists of features without connecting to the feeling
- Anything that sounds like it was written by a marketing department

---

## Services & Packages

**Products available (SKWOL Flagship Collection kit):**

- pH Neutral Foaming Boat Soap
- Formula 4 pH Neutral All-Purpose Cleaner
- One Step Oxidation Remover (removes oxidation, water spots, scratches — polishes to high gloss, no fillers)
- Ceramic Top Coat Sealant (6–8 month protection, hydrophobic water-beading)
- Vinyl Protectant Plus (UV + mold resistant)
- Microfiber correction and protection towels + 6" polishing pad

**NOT offered yet:** Teak cleaning/restoration — no products or skills for teak yet. Do not include teak in any service descriptions.

---

### Package 1 — The Essential Wash

- Full exterior rinse and wash (hull, topside, deck, cockpit)
- Window and windshield clean + dry
- Interior surface wipe-down (dash, console, cupholders)

### Package 2 — The Full Detail

- Everything in The Essential Wash, plus:
- Upholstery and vinyl clean + conditioning (UV/mold protection)
- Floor and carpet vacuum and scrub
- Compartments and hatches cleaned out
- Mildew treatment on seats and cushions

### Package 3 — The Restoration Detail

- Everything in The Full Detail, plus:
- Oxidation removal (light to average severity) — restores gelcoat to high-gloss finish
- Ceramic sealant protection applied to all gelcoat (6–8 month durability)
- Heavy oxidation = additional charge, quoted separately after inspection

---

## Pricing

Priced per linear foot of boat length. Modeled after established Florida competitors; slightly below market as MCC builds its reputation.

| Package | Per Foot | Minimum |
| --- | --- | --- |
| The Essential Wash | $4/ft | $100 |
| The Full Detail | $12/ft | $280 |
| The Restoration Detail | $22/ft | $500 |
| Heavy Oxidation (add-on) | Custom quote | — |

**Reference benchmarks (Florida Boat Detailing, Central FL):**

- Basic wash: $3.50/ft | Detail: $14/ft | Premium + compound + sealant: $52/ft
- MCC prices sit competitively below given solo/mobile operation and startup stage

**Example quotes:**

- 22ft boat — Essential: $100 (min) | Full Detail: $264 | Restoration: $484
- 25ft boat — Essential: $100 | Full Detail: $300 | Restoration: $550
