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

## New Features (from Banebyg_Nye funktioner (2).xlsx)
 
Features prioriteret efter Rating (1 = højest, 5 = lavest, 0 = ej relevant).
 
### Ej relevant / Udskudt (Rating 0)
 
| Nr | Funktion | Begrundelse |
|----|----------|-------------|
| 6 | Udbud: Totalrådgivning | Ikke relevant for fagpakker BBTR; venter til ny platform for RY |
| 14 | ATR: Afregningstyper (RY/Totalrådgivning) | Kun relevant for RY; fejl i kontrakt skal rettes separat |
| 23 | Øvrige: Afgrænsningsfasen | Indarbejdes direkte i nuværende BBTR via faseopdelte poster |
| 24 | Øvrige: RY (Totalrådgivning) | Skal være særskilt platform; ikke kompatibelt med fagpakker setup |
 
### Prioritet 1 — Kritisk (Rating 1)
 
| Nr | Sektion | Funktion | Kort beskrivelse | Planlagt fase |
|----|---------|----------|------------------|---------------|
| 2 | Poster | Skrifttyper/afsnit typer | Manglende skrifttyper og afsnittyper i rich text editor | Phase 3 (3B) |
| 3 | Poster | Slette poster som admin | Admin kan permanent slette poster (ikke kun Udgået) | Phase 3 (3A/3B) |
| 4 | Poster | Vejledende tekst ved projektspecifik tekst | Hjælpetekst (tooltip/inline) ved projektspecifikke tekstfelter | Phase 5 (5C) |
| 5 | Poster | Drag & Drop rækkefølge | Drag & drop til omarrangering af poster i hierarkiet | Phase 3 (3A) |
| 9 | ATR | Kontrol over ATR tekstfelter | Fast ATR-tekst per fagpost defineret af admin | Phase 6 (6C) / Phase 7 |
| 11 | ATR | Formatering/skrifttyper | Rich text formatering i ATR-felter | Phase 6 (6C) |
| 15 | ATR | Bemandingsplanen tilpasning | Tilpas/definér poster/aktiviteter i bemandingsplan (CSM, Dispensationer, etc.) | Phase 6 (6C) |
| 16 | ATR | Adgang for eksterne konsulenter (Xbruger) | Xbruger-rolle med adgang til ATR visning/redigering | Phase 8 (8A) |
| 17 | ATR | ATR skabelon: Excel → Word + ændringslog | Nyt Word-paradigme for ATR med ændringslog | Phase 9 (9A) |
| 18 | ATR | Ændringslog i bemandingsplan | Ændringslog-funktion ved udtræk af bemandingsplaner | Phase 9 (9B) |
| 20 | Bilag | Automatisk dokumentfortegnelse | Auto-genereret dokument- og tegningsfortegnelse fra valgte bilag | Phase 4 (ny) |
| 25 | Udtræk | Tilvælge dokumenter i udtræk (rettelsesblad) | Vælg/fravælg bilag ved samlet udtræk efter version 1.0 | Phase 9 (ny) |
 
### Prioritet 2 — Vigtig (Rating 2)
 
| Nr | Sektion | Funktion | Kort beskrivelse | Planlagt fase |
|----|---------|----------|------------------|---------------|
| 8 | Udbud | Slettefunktion | Admin kan permanent slette fejloprettede udbud | Phase 5 (5A/5B) |
| 13 | ATR | Ændringsydelser | Fjern fra hoved-ATR; indarbejd i tillægs-ATR skabelon | Phase 6 (6B/6C) |
| 22 | Bilag | Slettefunktion | Admin kan permanent slette fejloprettede bilag | Phase 4 (4A/4B) |
 
### Prioritet 3–5 — Lavere prioritet
 
| Nr | Sektion | Funktion | Rating | Planlagt fase |
|----|---------|----------|--------|---------------|
| 1 | Poster | Kontrol over postnr. | 3 | Phase 3 (3B) |
| 7 | Udbud | Udtræk pr. fagposter/fagopdelt | 4 | Phase 9 (ny) |
| 12 | ATR | Hjælpetekst ikon | 5 | Phase 6 (6C) |
| 21 | Bilag | Dokumentationsplan (DKP kobling) | 4 | Udskudt (kravspec under udarbejdelse) |
 
### Uden rating
 
| Nr | Sektion | Funktion | Planlagt fase |
|----|---------|----------|---------------|
| 10 | ATR | Bilag: Tilpas bilag-titel | Phase 6 (6B) |
| 19 | ATR | Bilag 1: Nedbrud af timeforbrug — korrekt rækkefølge/nummerering | Phase 6 (6C) |

 
## Execution Tracking
 
See `implementation-spec.md` for the live build order, status table, acceptance criteria, and blockers.



