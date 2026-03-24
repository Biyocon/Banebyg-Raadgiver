# Implementation Spec — BaneByg Teknisk Rådgivning (BBTR)
 
**Status:** Pre-Implementation
**Last updated:** 2026-03-24
 
---
 
## Build Order
 
| Step | Description | Status | Completed | Notes / Verification |
|------|-------------|--------|-----------|----------------------|
| 0A | SPFx project scaffold (`yo @microsoft/sharepoint`) | TODO | — | — |
| 0B | Folder structure: `shared/`, `bbtr-only/`, `config/`, `models/` | TODO | — | — |
| 0C | Feature flag setup (`IS_BBTR` in `config/features.ts`) | TODO | — | — |
| 1A | Shared SP list schemas (7 lists: Poster, Bilag, Udbud, UdbudPoster, UdbudBilag, Versionslog, BilagFiler) | TODO | — | — |
| 1B | BBTR-unique SP list schemas (6 lists: ATR, ATRInfo, ATRSkema, ATRKategorier, Faser, Medarbejderkategorier) | TODO | — | — |
| 1C | List provisioning script (`elements.xml` or PnP provisioning) | TODO | — | — |
| 2A | TypeScript models — shared (Post, Bilag, Udbud, UdbudPost, UdbudBilag, Versionslog) | TODO | — | — |
| 2B | TypeScript models — BBTR (ATR, ATRInfo, ATRSkema, ATRKategori, Fase, Medarbejderkategori) | TODO | — | — |
| 2C | SP service layer (PnPjs CRUD operations, batching, error handling) | TODO | — | — |
| 2D | Navigation component (tabs: Poster, Udbud, ATR & Bemanding, Bilag + right-side admin/feedback links) | TODO | — | — |
| 3A | Poster tree component (hierarchical, expandable, search, "Søg kun i postnr./titel" checkbox) | TODO | — | — |
| 3B | Post editor (right panel: Aktiv/Udgået toggle, PostType dropdown, Nr/Navn fields, rich text, bilag section, ATR-skema checkbox, Inkludér per default checkbox) | TODO | — | — |
| 3C | Create post modal (PostType, Fagpost/Hovedpost lookups, initial fields) | TODO | — | — |
| 4A | Bilag list component (search, table: Id, Navn, Version, Aktiv, Relaterede poster, actions) | TODO | — | — |
| 4B | Bilag create/edit modal + file upload to BilagFiler library | TODO | — | — |
| 5A | Udbud list component (table with filters: Projektnr, Projektnavn, Revision, Status, Version, actions) | TODO | — | — |
| 5B | Udbud create/edit modal (Projektnr*, Projektnavn*, Offentliggørelsesdato*, Status*, Fase*, Link til projekt site, descriptions) | TODO | — | — |
| 5C | Udbud poster editor (two-column: basistekst left, udbudsspecifik kommentar right; checkbox per post; bilag per post) | TODO | — | — |
| 5D | "Hent basistekst fra nyeste version" modal (version comparison, confirm overwrite) | TODO | — | — |
| 6A | ATR list component (grouped per udbud, expand/collapse, filters: mine/alle, year, search) | TODO | — | — |
| 6B | ATR Info modal (Udbudsform*, Ændringsydelse toggle, Loft, BDK Projektleder, Ledelsesrepræsentant, Godkendt af, Rådgiver repræsentant, Eksterne rådgivere) | TODO | — | — |
| 6C | ATR-skema editor (full page: warning banner if dates missing, Overordnet beskrivelse, Omfang af ydelsen, Ressourcer, dynamic categories repeater with "+ Tilføj kategori", Tilbage button) | TODO | — | — |
| 6D | ATR auto-generation logic (Power Automate flow: on Udbud creation, create ATR per included fagpost where ATRSkemaPåkrævet = true) | TODO | — | — |
| 7A | Admin: Standard tekster (5 sections via dropdown: Hvis ikke andet, Vejledning, Tidsplan, Normal udbudsform, Omvendt udbudsform; rich text editor) | TODO | — | — |
| 7B | Admin: Fase management (CRUD table: SorteringsNr, FaseNavn, FaseNr, Deaktiveret flag, Ændret af; inline edit) | TODO | — | — |
| 7C | Admin: Medarbejderkategori management (CRUD table: KategoriNavn, Aktiv flag) | TODO | — | — |
| 8A | Role-based access control (SP groups → SPFx permission checks, route guarding) | TODO | — | — |
| 8B | Poster/Bilag admin-only restriction (hide tabs + server-side SP permissions) | TODO | — | — |
| 9A | ATR preview document generation (Azure Function + Word template) | TODO | — | — |
| 9B | Bemandingsplan document generation (Azure Function + Excel template) | TODO | — | — |
| 10A | End-to-end testing (all sections, all roles, edge cases) | TODO | — | — |
| 10B | Deployment configuration (tenant-level app catalog, site provisioning) | TODO | — | — |
 
---
 
## Acceptance Criteria
 
### Phase 0 — Project Scaffolding
- **0A:** `gulp serve` runs without errors; SPFx workbench loads
- **0B:** Folder structure matches planned layout; all directories exist
- **0C:** `IS_BBTR` flag toggles ATR & Bemanding tab visibility; false hides BBTR-only components
 
### Phase 1 — SharePoint List Provisioning
- **1A:** All 7 shared lists created with correct columns, types, and lookups
- **1B:** All 6 BBTR-unique lists created with correct columns, types, and lookups
- **1C:** Provisioning script creates all lists on a clean site; idempotent re-run doesn't duplicate
 
### Phase 2 — Shared Foundation
- **2A:** All shared model interfaces match PRD field definitions; exported from `models/shared/`
- **2B:** All BBTR model interfaces match PRD field definitions; exported from `models/bbtr/`
- **2C:** CRUD operations (get, getById, create, update, delete) work for all 13 lists; batch operations supported
- **2D:** Navigation renders 4 tabs (3 if `IS_BBTR=false`); active tab highlighted; right-side links functional
 
### Phase 3 — Poster Section
- **3A:** Tree shows 25 root posts with correct hierarchy; expand/collapse works; search filters by postnr/title
- **3B:** Selecting a post loads editor; all fields editable; save persists to SP list; Aktiv/Udgået toggle updates status
- **3C:** Modal creates new post with correct PostType; appears in tree after save
 
### Phase 4 — Bilag Section
- **4A:** Table shows all bilag with correct columns; search works; Relaterede poster shows linked posts
- **4B:** Modal creates bilag with file upload; edit updates metadata; file stored in BilagFiler library
 
### Phase 5 — Udbud Section
- **5A:** Table shows all tenders with correct columns; filters by status/year
- **5B:** Modal creates/edits udbud; Fase dropdown populated from BBTR_Faser; all required fields validated
- **5C:** Two-column editor: basistekst (read-only from post) on left, udbudsspecifik kommentar (editable) on right; checkboxes toggle post inclusion; bilag attachable per post
- **5D:** Modal shows version diff; confirms overwrite; updates basistekst to latest version
 
### Phase 6 — ATR & Bemanding
- **6A:** ATRs grouped by udbud; expand shows ATRs for that udbud; filters (mine/alle, year, search) work
- **6B:** Modal loads ATR metadata; all fields editable; person fields resolve against Azure AD
- **6C:** Full-page editor with all fields; categories repeater adds/removes rows; Tilbage navigates back
- **6D:** Creating a new udbud auto-generates ATR records for each selected fagpost with ATRSkemaPåkrævet=true
 
### Phase 7 — Admin Section
- **7A:** Dropdown selects section; rich text editor loads/saves content per section
- **7B:** Table shows all phases; inline edit for name/number; deactivation hides from Udbud Fase dropdown
- **7C:** Table shows all categories; add/edit/deactivate; used categories cannot be deleted
 
### Phase 8 — Roles & Permissions
- **8A:** SP groups (Administrator, Projektleder, Bruger, Læser) map to correct permissions; unauthorized actions blocked
- **8B:** Non-admin users cannot see Poster/Bilag tabs; direct URL access returns 403/redirect
 
### Phase 9 — Document Generation
- **9A:** "Preview ATR" button generates Word document with correct ATR data; opens in browser
- **9B:** "Preview Bemandingsplan" generates Excel with categories and hours; opens in browser
 
### Phase 10 — Testing & Deployment
- **10A:** All user flows pass for all 4 roles; edge cases (empty states, max items, concurrent edits) handled
- **10B:** App package deploys to tenant app catalog; site-level activation works; provisioning script runs clean
 
---
 
## Blockers
 
_None currently._
 
---
 
## Next Up
 
**Phase 0:** Steps 0A, 0B, 0C — Scaffold SPFx project and establish folder structure with feature flags.
 
---
 
## Adopted External Patterns
 
| Pattern | Level | Used In | Why Adopted | Adoption Status |
|---------|-------|---------|-------------|-----------------|
| PnPjs for SP list operations | Architecture | All SP interactions (Step 2C) | Type-safe SharePoint API with batching, caching, and fluent syntax | Planned |
| SPFx React component model | Architecture | All webparts | Microsoft-standard pattern for SP customization; supports React lifecycle | Planned |
| Feature flag (`IS_BBTR`) | Architecture | `config/features.ts`, conditional rendering | Single codebase for BBE + BBTR; avoids maintaining two solutions | Planned |
| Hierarchical self-referencing list | Data | Poster tree (Steps 3A–3C) | `ParentPostId` lookup enables n-level hierarchy in a flat SP list | Planned |
| Soft delete pattern | Data | Faser (Deaktiveret), Poster (Udgået) | Preserves referential integrity; historical tenders still reference retired items | Planned |
| Modal-based CRUD | UX | Udbud, Bilag, ATR Info (Steps 5B, 4B, 6B) | Consistent interaction pattern; keeps user on list view while editing | Planned |
| Grouped list with expand/collapse | UX | ATR list (Step 6A) | ATRs naturally belong to Udbud; grouping reduces visual noise | Planned |
| Rich text CMS pattern | UX | Poster editor, Admin tekster (Steps 3B, 7A) | Reusable rich text editing for basistekster and standard texts | Planned |
| Power Automate for server-side logic | Runtime | ATR auto-generation, versioning (Step 6D) | No Azure subscription needed for MVP; triggers on SP list events | Planned |
| Document generation via Office templates | Future | ATR/Bemanding preview (Steps 9A, 9B) | Azure Function + Word/Excel templates for formatted output | Deferred |
