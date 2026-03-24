# Primer — BaneByg Teknisk Rådgivning (BBTR)
 
Onboarding guide for new contributors and Claude Code sessions.
 
## What is BBTR?
 
BBTR is an internal SharePoint application used by Banedanmark's construction division to **create tender documents for technical consulting services** (rådgivning). It manages specification posts, tender configurations, work/time/resource schemas, and standard attachments — all within SharePoint Online.
 
## How BBTR Relates to BBE
 
BaneByg Entreprise (BBE) is the existing platform for construction tenders (entreprise). BBTR extends it:
 
| Aspect | BBE | BBTR |
|--------|-----|------|
| Sections | 3 (Poster, Udbud, Bilag) | 4 (+ ATR & Bemanding) |
| Fagposter | 17 | 25 (incl. phase-based 22–25) |
| Tender stages | Manual stadier | Fase dropdown (admin-managed) |
| Subcontracting | Delentreprise fields | Not applicable |
| Post flags | Basic | + ATR-skema påkrævet, Inkludér per default |
| Post status | Aktiv/Inaktiv dropdown | Aktiv/Udgået toggle |
 
Both share a **single SPFx solution** with feature flag `IS_BBTR` controlling which modules render.
 
## The 4 Sections
 
### Poster (Fagposter / Specification Posts)
Hierarchical catalog of 25 technical specification posts. Each post has a numbered position (e.g., "3. Spor", "3.1 Banedanmark grundlag"), a rich-text description (basistekst), and metadata flags. Posts can be Aktiv or Udgået (retired). Admin-only section.
 
### Udbud (Tenders)
Tender documents configured per project. Each udbud selects which posts to include, allows project-specific comments alongside basistekster, and attaches bilag. Key field: **Fase** — a required dropdown replacing BBE's manual stages.
 
### ATR & Bemanding (Work/Time/Resource Schemas)
Unique to BBTR. When a tender is created, ATR records are auto-generated for each included fagpost that has "ATR-skema påkrævet". Each ATR has:
- **ATR Info:** Contract metadata, roles, contact persons
- **ATR-skema:** Descriptions (overordnet, omfang, ressourcer) + dynamic employee categories
- **Preview:** Generated ATR document and bemandingsplan
 
### Bilag (Attachments)
Standard attachments library managed by administrators. Each bilag has a name, version, file, and related poster. Referenced from both Poster and Udbud sections.
 
## Data Model Overview
 
```
Post ──1:N──> UdbudPost <──N:1── Udbud
                                    │
                                    ├──N:1── Fase
                                    │
                                    └──1:N── ATR ──1:1── ATRInfo
                                                  ──1:1── ATRSkema ──1:N── ATRKategori
                                                                              │
                                                                              N:1
                                                                              │
                                                                     Medarbejderkategori
 
Post ──self-ref──> Post (hierarchy via ParentPostId)
Post ──N:M──> Bilag (via PostBilag)
```
 
**13 SharePoint lists:**
- Shared (7): BaneByg_Poster, BaneByg_Bilag, BaneByg_Udbud, BaneByg_UdbudPoster, BaneByg_UdbudBilag, BaneByg_Versionslog, BaneByg_BilagFiler
- BBTR-unique (6): BBTR_ATR, BBTR_ATRInfo, BBTR_ATRSkema, BBTR_ATRKategorier, BBTR_Faser, BBTR_Medarbejderkategorier
 
## Key Domain Terms (Danish)
 
| Term | Meaning |
|------|---------|
| Fagpost | Technical specification post (top-level category) |
| Hovedpost | Parent post in hierarchy |
| Underpost | Child post |
| Udbud | Tender document |
| Fase | Project phase (Programfasen, Projekteringsfase, Udførelsesfase, Afslutningsfase) |
| Udgået | Retired/deprecated (post status) |
| Basistekst | Standard description text (versioned) |
| Udbudsspecifik kommentar | Project-specific comment added to a post within a tender |
| ATR | Arbejds-, Tids- og Ressourceskema (work/time/resource schema) |
| Bemanding | Staffing plan |
| Bilag | Attachment/appendix |
| Medarbejderkategori | Employee category (for ATR staffing breakdown) |
| Ændringsydelse | Change service (boolean flag on ATR) |
| Udbudsform | Tender type: Normal or Omvendt (reverse) |
 
## Roles & Access
 
| Role | Poster | Udbud | ATR & Bemanding | Bilag | Admin |
|------|--------|-------|-----------------|-------|-------|
| Læser | Read | — | — | — | — |
| Bruger | — | Own | Own | — | — |
| Projektleder | — | All active | All | — | — |
| Administrator | Full | Full | Full | Full | Full |
 
Poster and Bilag are **admin-only** sections. Bruger and Projektleder cannot access them.
 
## Technical Architecture
 
- **SPFx webparts** (React): Custom UI for all 4 sections + admin screens
- **SharePoint Lists**: Data storage (13 lists + 1 document library)
- **PnPjs**: TypeScript library for SP list operations (CRUD, batching, caching)
- **Power Automate**: Server-side flows for ATR auto-generation, version logging, notifications
- **Azure Functions** (Phase 9): Document generation for ATR preview and bemandingsplan
- **Azure AD**: Authentication and role assignment via SP groups
 
## Key Reference Documents
 
- `PRD_BBTR_BaneByg_Raadgiver.md` — Complete PRD with all screen descriptions, data model, user flows
- `PRD_BaneByg_Teknisk_Raadgivning_SharePoint-kloning.md` — SharePoint implementation PRD with list schemas, SPFx components, Power Automate flows
- `README_BBTR.md` — Architecture overview, data model (Mermaid ER diagram), differences from BBE
- `implementation-spec.md` — Current build status and execution tracking
- `plan.md` — Strategic roadmap and phase dependencies
