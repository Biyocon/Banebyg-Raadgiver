# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

BaneByg Teknisk Rådgivning (BBTR) — a SharePoint Online (SPFx + React) application for Banedanmark's construction division. Used to create tender documents for technical consulting services. This repo currently contains **PRDs, reference images, and planning documents** — no source code yet.

BBTR is a **superset of BaneByg Entreprise (BBE)**. Everything in BBE exists in BBTR, plus the ATR & Bemanding module. The two should share a single SPFx solution with feature flags (`IS_BBTR`).

## Key Documents

- `PRD_BBTR_BaneByg_Raadgiver.md` — Full PRD generated from video analysis (primary spec)
- `PRD_BaneByg_Teknisk_Raadgivning_SharePoint-kloning.md` — SharePoint cloning PRD with implementation details
- `README_BBTR.md` — Architecture overview, data model, differences from BBE, SharePoint list definitions
- `claude-code-prompt-platform-kloning.md` — The prompt template used to generate PRDs from video analysis
- `frame_*.jpg` — Video frames from the BBTR screen recording (reference screenshots)
- `contact_BBTR_*.jpg` — Contact information screenshots

## Architecture (Target)

**4 sections:** Poster (posts/specs), Udbud (tenders), ATR & Bemanding (work/time/resource schemas), Bilag (attachments)

**Tech stack:** SharePoint Online, SPFx (SharePoint Framework), React, Azure AD auth, SharePoint Lists (13 total)

**Planned code structure:**
```
banebyg-spfx/
  src/
    webparts/
      shared/        # Shared with BBE: Navigation, Poster, Udbud, Bilag, Admin
      bbtr-only/     # BBTR-specific: ATR, Bemanding, FaseAdmin, etc.
    config/
      features.ts    # Feature flags: IS_BBTR = true/false
    models/
      shared/        # Post, Bilag, Udbud, UdbudPost, etc.
      bbtr/          # ATR, ATRInfo, ATRSkema, Fase, Medarbejderkategori
```

**SharePoint Lists — shared with BBE (7):** BaneByg_Poster, BaneByg_Bilag, BaneByg_Udbud, BaneByg_UdbudPoster, BaneByg_UdbudBilag, BaneByg_Versionslog, BaneByg_BilagFiler

**SharePoint Lists — BBTR-unique (6):** BBTR_ATR, BBTR_ATRInfo, BBTR_ATRSkema, BBTR_ATRKategorier, BBTR_Faser, BBTR_Medarbejderkategorier

## Key Domain Concepts

- **Poster** = hierarchical catalog of 25 technical specification posts (fagposter), some phase-based (posts 22-25)
- **Udbud** = tender documents with phases (Fase dropdown replaces BBE's manual stages; no Delentreprise)
- **ATR** = Arbejds-, Tids- og Ressourceskema — unique to BBTR, generated per tender/post combination
- **Faser** = project phases (admin-managed): Programfasen, Projekteringsfase, Udførelsesfase, Afslutningsfase
- Posts have: Aktiv/Udgået toggle, "ATR-skema påkrævet" checkbox, "Inkludér post per default" checkbox

## Roles

- **Administrator** — full access to all sections including Poster and Bilag admin
- **Projektleder** — all active tenders + all ATRs
- **Bruger** — own tenders and ATRs only
- **Læser** — read-only on Poster

## Language

All UI text, field names, and documentation are in **Danish**. Use Danish for user-facing strings and comments in code.
