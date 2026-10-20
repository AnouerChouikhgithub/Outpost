# UI specification (source of truth for all screens)

INSTRUCTIONS FOR THE CODING AGENT
- Implement the screens below as real, working code in `frontend/`. Wording such as "generate" or "visual reference" means: build them in the codebase.
- Work in the batches the developer asks for. Never skip, merge or summarize screens inside a requested batch.
- Every screen must support light AND dark mode through the central theme tokens. No hard-coded colors in components.
- Use typed mock data in `src/mocks/` for now. No backend calls until the developer says so.
- Reuse components. If a pattern appears twice, extract a component.
- Before the first batch, build the foundation: theme tokens, theme provider with Light / Dark / System, base components, navigation skeleton with a placeholder for every screen.
- Ask before adding a dependency that is not already listed in AGENTS.md. If a listed library is incompatible with the installed framework version, tell the developer and propose the closest alternative.

---

## Part 1: Shared design foundation

You are a senior product designer and front-end engineer. Design a professional, polished, production-grade UI. It must look like a funded startup's app, not a template.

THEMING (critical)
- Every screen must exist in BOTH light and dark mode. Default = follow system, plus a manual Light / Dark / System switch in Settings.
- Dark mode is NOT an inversion: use layered surfaces (background < surface < elevated), a slightly lighter and desaturated primary, subtle 1px borders instead of shadows, and softer white text (never pure #FFF on pure #000).
- All colors come from semantic tokens in ONE theme file (no hard-coded hex in components).
- Neutral tokens. Light: background #F8FAFC, surface #FFFFFF, border #E2E8F0, text #0F172A, text-secondary #475569. Dark: background #0B0F14, surface #121821, elevated #1A2230, border #263041, text #E6EAF0, text-secondary #9AA6B8.
- Status tokens. Light: success #16A34A, warning #D97706, danger #DC2626, info #2563EB. Dark: success #4ADE80, warning #FBBF24, danger #F87171, info #60A5FA.
- The project's primary color is given in the project prompt (light value and dark value). Use it sparingly: primary actions, active states, key highlights. Do not flood the UI with it.

DESIGN SYSTEM
- Font: Inter (system font fallback). Scale: display 28/34 semibold, title 20/28 semibold, body 16/24 regular, caption 13/18 medium. Tabular numbers for prices, times and metrics.
- 4pt spacing grid. Corner radius: 12 cards and inputs, 16 sheets and modals, full for chips and avatars.
- Minimum touch target 44pt (primary buttons 52pt tall). Respect safe areas.
- Icons: one consistent single-stroke set (Lucide), 1.75px stroke. No emoji as icons.
- Components to build once and reuse: buttons (primary, secondary, ghost, destructive, with loading state), text inputs (label above, helper text, error state, disabled), cards, list rows, chips and badges, avatars, segmented control, switch, bottom sheet or modal, toast, skeleton loaders.
- Every list and data screen needs designed states: loading (skeletons), empty (simple line icon + one-line explanation + primary CTA), error (message + Retry), and success feedback.
- Motion: 150-250ms ease-out transitions, subtle press feedback, haptics on key actions (mobile). Respect reduced-motion settings.
- Accessibility: WCAG AA contrast (4.5:1 text) in BOTH modes, visible focus states, labels for every control, dynamic text sizing must not break layouts.

CONTENT
- Use realistic sample data set in Tunisia: names like Amine Ben Salah, Ons Trabelsi, Yassine Jebali; cities Tunis, Sfax, Sousse, Bizerte, La Marsa; currency TND (e.g. 48,500 TND with 3 decimals where appropriate); French-style addresses. NO lorem ipsum, no gray placeholder boxes.
- Keep copy short, human, and action-oriented.

CODE RULES
- TypeScript, strict. Clean folder structure: theme/, components/, screens/, mocks/ (all sample data lives in mocks/). No backend calls yet: typed mock data only.
- Reusable components, no copy-pasted JSX. Keep the theme tokens centralized so the primary color can be changed in one place.

DO NOT: heavy gradients, drop shadows in dark mode, stock-photo clutter, more than one accent color, tiny text, crowded screens.

---

## Project spec

PROJECT: Outpost. An offline-first field app for technicians, inspectors and delivery staff. Users log jobs, capture photos and GPS, and everything syncs automatically when the connection returns. Tone: reliable, calm, professional, built for gloves-on, sunlight, bad-signal conditions.

PRIMARY COLOR: light #15803D (white text on it), dark #4ADE80 (near-black text on it). Logo idea: a map pin split vertically, left half outlined (offline), right half solid (synced), small sync arrow in the center. Show a simple version in the splash and login.

SIGNATURE FEATURE: a clear SYNC STATE on every record, shown as a chip: Pending (warning), Syncing (info, animated spinner), Synced (success, check), Conflict (danger, alert icon). A persistent but unobtrusive connection banner appears when offline ("You're offline. 4 changes will sync automatically.").

NAVIGATION: bottom tabs: Today, Map, Sync, Profile. A floating "+" button on Today creates a job.

SCREENS (build in this order; each in light AND dark):
1. Splash + Login (email/password, "Continue with company code", forgot password link, clean illustration-free layout).
2. Today (home): large title with date, sync summary card ("12 jobs, 3 pending sync, last synced 2 min ago"), filter chips (All, To do, In progress, Done), job list rows (title, client, address, time window, status badge, sync chip). Pull-to-refresh. Offline banner variant.
3. Job detail: header with status and client, address with "Open in maps", scheduled time, notes, checklist with checkable items, photo grid (with pending-upload overlay on photos not yet synced), activity timeline, sticky bottom bar with "Start job" / "Complete job".
4. New / edit job: form with client, address with "Use current location" (GPS accuracy badge), date and time, priority segmented control, notes, add-photo tile, save button that says "Save offline" when offline.
5. Camera review: captured photo preview, GPS and timestamp overlay chip, annotation tools (draw, text), retake / use photo.
6. Map: full-screen map with job pins colored by status, bottom sheet carousel of nearby jobs, "locate me" button. Provide light and dark map styles.
7. Sync center: big status header (Online / Offline), queue list grouped by Pending / Failed / Synced with per-item sync chip, "Sync now" button, last sync time, storage used.
8. Conflict resolution sheet: two-column "Your version vs Server version" comparison with changed fields highlighted, buttons "Keep mine", "Keep server", "Merge".
9. Profile and Settings: avatar, company, appearance (Light / Dark / System), sync preferences (Wi-Fi only, auto-sync), language, notifications, log out.

Make sure every screen shows at least one realistic offline or sync detail.

DELIVERY: Generate ALL 9 screens listed above, each in light and dark mode, as ONE connected, navigable app (working tab bar, working navigation between screens, working theme switch). Do not skip, merge or summarize any screen. These screens are the visual reference for the implementation, so be complete and consistent.
