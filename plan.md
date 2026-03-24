# Plan — BaneByg Teknisk Rådgivning (BBTR)
 
Strategic roadmap for building the BBTR SharePoint application.
 
## Vision
 
A single SPFx solution serving both BBE and BBTR via the `IS_BBTR` feature flag. Shared components (Poster, Udbud, Bilag, Navigation) are reused; BBTR-specific modules (ATR & Bemanding, Fase admin, Medarbejderkategori admin) activate only when `IS_BBTR = true`.
 
## Phase Overview
 
| Phase | Name | Scope | Dependencies | Complexity |
|-------|------|-------|--------------|------------|
| 0 | Project Scaffolding | SPFx scaffold, folder structure, feature flags, dev tooling | None | Low |
| 1 | SharePoint List Provisioning | All 13 list schemas + document library, provisioning scripts | Phase 0 | Medium |
| 2 | Shared Foundation | TypeScript models, SP service layer (PnPjs), navigation component | Phase 1 | Medium |
| 3 | Poster Section | Hierarchical tree, post editor, create modal, search | Phase 2 | High |
| 4 | Bilag Section | List, create/edit modal, file upload, post relations | Phase 2 | Medium |
| 5 | Udbud Section | List, create/edit modal, poster editor, basistekst modal | Phase 2 | High |
| 6 | ATR & Bemanding | ATR list (grouped), ATR Info modal, ATR-skema editor, auto-generation | Phase 5 | Very High |
| 7 | Admin Section | Standard tekster CMS, Fase CRUD, Medarbejderkategori management | Phase 6 | Medium |
| 8 | Roles & Permissions | SP groups, permission checks, admin-only restrictions | Phase 2 (spans all) | Medium |
| 9 | Document Generation | ATR preview, Bemandingsplan — Azure Function + Office templates | Phase 6 | High |
| 10 | Testing & Deployment | End-to-end testing, deployment config, tenant provisioning | All phases | Medium |
 
## Critical Path
 
```
Phase 0 → Phase 1 → Phase 2 ─┬─→ Phase 3 (parallel)
                               ├─→ Phase 4 (parallel)
                               ├─→ Phase 5 → Phase 6 → Phase 7
                               │                  └──→ Phase 9
                               └─→ Phase 8 (spans all sections)
                                                        Phase 10 (after all)
```
 
- **0 → 1 → 2** are sequential prerequisites (no UI without models and services)
- **3 and 4** can be built in parallel after Phase 2
- **5 before 6** — ATR references Udbud and its post selections
- **7 after 6** — Admin manages Faser and Medarbejderkategorier used by ATR
- **8 spans all** — Permission checks layered onto each section as it's built
- **9 after 6** — Document generation depends on ATR data structures
 
## Key Risks
 
| Risk | Impact | Mitigation |
|------|--------|------------|
| ATR auto-generation complexity | ATRs must be created per fagpost when udbud is created; requires server-side logic | Power Automate flow triggered on Udbud creation; fallback: SPFx batch creation |
| Document generation | ATR preview + Bemandingsplan require Word/Excel template rendering | Defer to Phase 9; evaluate Azure Function + PnP-Docx vs. Office Scripts |
| Hierarchical tree performance | 25 root posts × N children, all loaded with expand/collapse | Lazy-load children on expand; cache in React state; index ParentPostId |
| Grouped ATR table | ATRs grouped by Udbud with expand/collapse, many action columns | Custom SPFx React grid — no OOTB solution; plan for virtualized rendering |
| SharePoint list thresholds | 5000-item threshold on large lists | Index key columns (UdbudId, FagpostId, Status); filter by year/project |
| Rich text editor consistency | Basistekst editing must preserve formatting across save/load cycles | Use SPFx RichText control or TinyMCE; sanitize HTML on save |
 
## Execution Tracking
 
See `implementation-spec.md` for the live build order, status table, acceptance criteria, and blockers.
