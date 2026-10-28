# Stratoks interface

## Overview

Stratoks is a world observer for watching autonomous creatures and inspecting their behavior. The recovered visual identity stays intact: an illustrated isometric clearing, yellow creatures, green controls and warm paper panels. The simulation occupies the screen. Header utilities and the bottom observation dock frame it; details use the existing side panel rather than a new dashboard or page.

The Phase 2A additions are `web/src/BrainBehavior.tsx`, `LearningLab.tsx` and their styles in `web/src/styles.css`. The world renderer, mascot/icon module and wallet component are byte-identical to the recovered source. No new art, font or icon library was introduced.

## Colors

Use the existing semantic CSS properties from `styles.css`, expressed in hex:

| Token | Value | Role |
|---|---|---|
| `--paper` | `#fafaf1` | Main panels, dialogs and selected segments |
| `--surface` | `#f3f4e8` | Inputs and subdued surfaces |
| `--soft` | `#e9eddf` | Segments, selected candidates, decision summary |
| `--ink` | `#263f31` | Primary text |
| `--muted` | `#5c6c58` | Secondary text and explanatory notes |
| `--line` | `#d9dece` | Structural separators and table rules |
| `--accent` | `#315d40` | Primary actions and experiment meters |
| `--accent-hover` | `#244b32` | Primary hover |
| `--danger` / `--danger-bg` | `#98462e` / `#f4e5da` | Error and harmful-action states |
| `--focus` | `#29592e` | Keyboard focus perimeter |

The terrain backdrop is `#b9cba1`; the renderer owns its illustrated palette. There is no dark theme. Learned values always carry signed numbers; decision source, selection and learning status have text, so color is not the only signal. Rendered contrast checks and any limitations are recorded in the validation report rather than inferred from these token values.

## Typography

The retained local Manrope Variable Latin WOFF2 is bundled through `@fontsource-variable/manrope`; fallbacks are Manrope, Arial and sans-serif. The source requests weights 400, 600 and 800. Normal body line-height is 1.5; prose uses 1.6. Headings use 1.25 and balanced wrapping; the welcome headline uses 1.15 and `-0.035em` tracking. Small text has natural spacing and casing. Numeric scores, facts and result rows use tabular digits.

| Token | Size | Typical use |
|---|---|---|
| `--text-xs` | 12px | Captions, compact candidate table, segment labels |
| `--text-sm` | 14px | Dense panel rows, disclosures and controls |
| `--text-md` | 16px | Body text, section headings and form inputs |
| `--text-lg` | 20px | Panel headings |
| `--text-xl` | 24px | Dialog headings and mobile welcome |
| `--text-display` | 32px | Desktop welcome headline |

Reuse this six-size scale. Inputs remain 16px on mobile. Long names, identifiers and table values wrap instead of being silently clipped. Prose stays inside the narrow panel; monospace is not used for narrative text.

## Layout

The app fills the viewport with the existing header, canvas, lower status and bottom dock. Desktop details are a 340px panel, 32px from the trailing edge, with a fixed header and independently scrolling body. It uses 20px horizontal content padding; new groups use 16–20px separation and 8–12px internal spacing. Candidate tables use fixed layout, a 44% action column and two numeric columns. They fit the panel without a horizontal scroll region.

Existing breakpoints at 1150, 800, 600 and 360px retain the layout's progressive compaction. At 600px and below, the panel spans the viewport with 12px margins, starts at 244px and ends above the 96px bottom navigation area. The panel body uses 18px inline padding. Existing short-height rules keep panels and navigation usable in landscape. The welcome surface remains above the fold at 390px, with the local world action, server settings and learning-scenario entry visible. The lab reuses the panel; it does not replace or resize the world.

The active mode and last selected action lead the Brain view. Sensed inputs, circuit details and protocol information use native disclosure controls. Candidate scores remain open by default. Longer reward and phase histories stay bounded and scroll with the panel. The UI exposes at most the server's 16 rewards and the lab's last 12 phases. The lab explains reset and download behavior next to its controls.

## Elevation & depth

The established panel shadow is `--shadow: 0 8px 32px #243e3020`; the welcome surface retains its larger `0 16px 56px #35482a24` shadow. Tonal backgrounds group content inside panels. Table rows and headers use separators for structure. No extra nested cards or decorative glow were added. Existing native modal dialogs sit above the world and make the background inert.

## Shapes

`--radius` is 16px for panels. The retained welcome surface uses 20px, mobile dialogs 18px, segments 9px and segment buttons 6px. New decision summaries use an 8px tonal inset. Native meters provide a small horizontal measure of autonomous choices, accompanied by numeric values and descriptive labels.

## Components

- `WorldCanvas` and `renderer.ts`: original scene, selection, pan/zoom, creature animation and template speech. The same engine supplies local and server observations.
- `SidePanel` in `Panels.tsx`: heading focus on entry, labeled aside, Escape and close control, persistent panel head and scrollable body.
- `Inspector`: existing Needs, Memories and Learning segments. `BrainBehavior` reads the optional version-1 server contract and shows unavailable/loading/stale states. **Learning history** groups retained **Linear-policy updates**, aggregate mean reward and recent decisions spanning policies. Current policy plasticity, decision source, historical action mode and separate wallet-memory policy have explicit text. Frozen/ablated outcomes say **No weight update**; retained earlier outcomes keep their recorded facts.
- `LearningLab`: labeled scenario and seed fields; reset, train, held-out evaluation, reversal and ablation controls; worker-busy disabled states; stable status region; retryable errors; measured result meters and a JSON download. Data lives only in its worker.
- `Modal`: native dialog, Escape/backdrop close, Tab handling and focus return. Settings and the unchanged wallet sheet reuse it.
- Existing `primary`, `secondary`, `text-button`, `icon-button`, `notice`, `facts`, `fineprint` and `error` styles remain the reuse points. The lab has one filled primary action; other operations use secondary buttons.

## Interaction & motion

Buttons use the existing 150ms transition language. The Phase 2A panels add no animation. Visible focus uses a 3px `--focus` outline offset by 3px; disclosures, native selects and buttons are keyboard operable. Form controls have persistent labels. State changes have text rather than color-only indications. Existing reduced-motion preferences stop cosmetic scene motion; world decisions continue. The private world has explicit pause/resume controls.

## Responsive behavior & verification

Production-export checks cover 320, 390, 800 and 1440px widths and 667×375 landscape for the new panels, with screenshots and actual interactions. The entry page is checked by taste@1 at 320, 390 and 1440. The current validation report distinguishes browser measurements, automated accessibility scans, native-device/screen-reader limitations and historical evidence. Do not infer complete accessibility conformance from a passing scan.

The correction preserves every color, type, spacing and component token above. It changes inspector meaning and disclosure copy, with no visual redesign, art or payment integration. Reuse `.brain-disclosure` for bounded technical detail; put the actual decision source before scores, keep historical counters labeled by policy, and never use a reflex as evidence of learned selection. Do not add a new type size or status color for another brain mode. Current coverage and applicable findings are in `docs/correction/VALIDATION.md`; earlier screenshots/reports remain historical.

Design methods: Better Interface by Jakub Krehel, pinned `267330e1adfc66a718fb65fa6918c1f06d0a689e` (MIT), and Impeccable documentation guidance by Paul Bakaus, pinned `9d715cc4f5564a990ca8345abfdd5df6dc9b41c8` (Apache-2.0). Original notices remain in `docs/licenses/design-guidance.txt`.
