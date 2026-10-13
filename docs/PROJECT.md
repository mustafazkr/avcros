Project State

Last updated: 2026-10-13

What this is

Avcros is a football analytics platform for analysts. It provides:

1. Match reports — detailed match data including shot maps, xG flow, radar comparisons, lineups, substitutions, formations, and annotations.
2. Club profiles — history, finance, staff, records, players, and head-to-head.
3. Blueprint (planned) — the analyst workspace where users build custom research layouts, arrange visualizations, document observations, compare matches, and eventually share their findings.

Target audience: analysts, scouts, journalists, and data-driven sports researchers who need detailed match information rather than only a summary.

Current state

Area	Status
Static site (en/main/)	Working
Club pages (en/sports/football/profiles/clubs/)	Working
Match pages (match.html)	Working, feature-rich
User account creation / authentication	Implemented with Supabase
Supabase backend integration	Connected for authentication
Player pages	Not started
Blueprint workspace	Not started
Blueprint cloud persistence	Not implemented / needs verification
Multilingual	Folder structure exists (en/), only English populated

Backend note: Supabase is already used for account creation/authentication. Do not describe the entire project as having no backend. Database features for Blueprint, workspace persistence, and collaboration have not been confirmed as implemented.

File inventory

en/main/

File	Purpose
index.html	Homepage — hero, search, football clubs grid, footer
settings.html	User settings — theme, calendar, research mode, keybinds, timezone

en/sports/football/profiles/clubs/

File	Purpose
match.html	Match report shell — loads data via query params
real-madrid.html, ac-milan.html, etc.	Club profile pages
_shared/match.js	Match page engine
_shared/match.css	Match page styles
_shared/club.js	Club profile engine
_shared/club.css	Club profile styles
_shared/data/matches/ucl/2024-25.js	Match data files
_shared/data/clubs/*.js	Club data files

Key features already built

Match page

* Overview tab: possession, radar chart, top performers, detailed stats
* Shots tab: shot map (SVG), xG flow chart, filters (team/goals), fullscreen mode
* Lineup tab: pitch view, formation changes, substitution impact, lineup tables
* Additional tab: referee, venue, managers, attendance
* Hover tooltips on player names (Shift-gated)
* Pin tooltips by clicking
* Crosshair mode on charts (C toggle)
* X-ray mode — reveals inline ratings and values (X hold)
* Mini scorecard in corner (S toggle)
* Notes system — shot notes and element notes
* Shift+N to pick any element and annotate
* Alt+hover to highlight a name across the page
* Research Mode Panel (Q)
* Keyboard: 1/2/3/4 (tabs), H/A/B (team filter), G (goals), F (fullscreen), Esc (reset)
* Session memory — remembers active tab and card state
* Cookies popup

Club page

* Overview, Finance, Stadium, Staff, Records, Players, Info tabs
* H2H with fixture navigation
* Multi-calendar support (Gregorian, Hijri, Persian, Chinese)
* Light/dark theme

Authentication

* User account creation and authentication through Supabase

Blueprint — planned analyst workspace

Blueprint is the planned analyst workspace within Avcros. Its purpose is to let users build, organize, and present football research using Avcros data.

Planned capabilities

1. Research canvas
    * Add, move, resize, group, and arrange blocks on a flexible canvas.
    * Support separate sections for different research questions.
2. Charts and data blocks
    * Reuse Avcros match visualizations and statistics.
    * Planned chart types may include shot maps, xG charts, passing networks, heatmaps, player radar comparisons, tables, and trend charts.
    * Only show metrics when suitable underlying data is available.
3. Notes and evidence
    * Add text blocks, images, annotations, and links to matches, players, and clubs.
    * Attach observations to relevant charts or match events.
    * Keep conclusions connected to supporting evidence.
4. Match and player comparison
    * Compare selected matches, teams, players, seasons, or periods of a match.
    * Support filters and consistent metric definitions where the data permits.
5. Tactical boards
    * Provide a pitch canvas for manually illustrating formations, movement, passing lanes, and tactical ideas.
    * Clearly distinguish manually drawn diagrams from verified event or tracking data.
6. Save and organize research
    * Create, rename, duplicate, reopen, and delete workspaces.
    * Browser-local saving may be suitable for an early prototype.
    * Supabase database persistence and cross-device synchronization require implementation and appropriate access controls.
7. Export and sharing
    * Planned exports may include charts, data tables, and printable reports.
    * Shared or collaborative workspaces require permissions and backend support.

Suggested initial scope for Blueprint

Prioritize these capabilities for the first version:

* Flexible canvas with movable and resizable blocks
* Reusable Avcros charts and data blocks
* Text notes and annotations
* References to existing match, club, and player records
* Save and reopen workspaces
* Basic export or print support

Defer real-time collaboration, advanced tactical tools, and complex scouting workflows until the core canvas and data model are reliable.

Global settings (localStorage)

Key	Purpose
olkvaj_theme	light / dark
olkvaj_calendar	gregorian / islamic / persian / chinese
olkvaj_research_mode	on / off — unlocks most keybinds
olkvaj_keybinds	on / off — master kill switch
olkvaj_animations	on / off
olkvaj_cookies	accept / essential
olkvaj_annotations:<matchId>	Per-match notes (localStorage)
olkvaj_match_session:<matchId>	Per-match session state (sessionStorage)

Compatibility note: Existing storage keys use the olkvaj_ prefix even though the project is now called Avcros. Decide whether to retain these keys for backward compatibility or implement a migration before changing them.

Known issues / TODOs

* Match page currently hardcodes layout; extract chart renderers into a shared charts.js module so they can be reused in Blueprint.
* Player pages not started.
* Supabase authentication is implemented; verify the current integration details and document the relevant files/configuration.
* Blueprint workspace app not started.
* Blueprint database schema, persistence, and access policies are not implemented or have not yet been verified.
* Ensure private workspace data is protected by Supabase Row Level Security (RLS) before adding cloud-saved workspaces or sharing.
* Multilingual structure exists, but only English is populated.

Dependencies and architecture

* Frontend: plain HTML, CSS, and JavaScript.
* No npm, build tools, or frontend framework currently documented.
* External CDN: Google Fonts (Inter).
* Supabase: used for user account creation/authentication.
* Supabase database, storage, or Edge Functions should only be documented as implemented once their use in the application has been verified.

Suggested development order

1. Extract reusable chart renderers and define consistent data structures.
2. Verify and document the existing Supabase authentication integration.
3. Build Blueprint’s canvas, chart blocks, notes, and local save/reopen flow.
4. Design and implement Supabase tables and Row Level Security for cloud workspaces.
5. Add exports, cross-match research, and more advanced analytical tools.
6. Add sharing and collaboration after ownership and permissions are secure.