# PRD: BaneByg Teknisk Rådgivning (BBTR) — SharePoint-kloning

**Version:** 1.0
**Dato:** 2026-03-24
**Kilde:** Videoanalyse af BBTR.mp4 (8:18 min, 100 frames @ 5s interval)
**Forfatter:** Claude Code — automatisk PRD-generering

---

## 1. Formål & Kontekst

### Hvad platformen gør i dag
BaneByg Teknisk Rådgivning (BBTR) er en SharePoint-baseret webapplikation (SPFx) hos Banedanmark. Platformen bruges til **udarbejdelse af udbudsmateriale for teknisk rådgivning** i anlægssektionen. Den adskiller sig fra BaneByg Entreprise (BBE) ved at inkludere en fjerde sektion — **ATR & Bemanding** — der håndterer rådgiverens arbejds- og tidsskemaer, bemandingsplaner og kontraktuelle krav.

Platformens fire sektioner:
1. **Poster** — Hierarkisk bibliotek af tekniske fagposter/basistekster (inkl. fasebaserede poster)
2. **Udbud** — Oprettelse og styring af udbudsdokumenter med faser
3. **ATR & Bemanding** — Arbejds-, tids- og ressourceskemaer per fagpost/udbud (unikt for BBTR)
4. **Bilag** — Centralt bibliotek med standardbilag

### Formål med kloningen
Producere en 1:1 funktionel klon som SharePoint-baseret løsning.

### Scope
1:1 funktionel klon af al synlig funktionalitet. Forskelle fra BBE dokumenteres eksplicit.

### Nøgleforskelle fra BBE

| Dimension | BBE | BBTR |
|-----------|-----|------|
| Sektioner | 3 (Poster, Udbud, Bilag) | 4 (Poster, Udbud, **ATR & Bemanding**, Bilag) |
| Udbud - Stadier | Ja (manuelt definerede stadier) | Nej (erstattet af Fase-felt) |
| Udbud - Fase | Nej | Ja (påkrævet dropdown) |
| Udbud - Delentreprise | Ja | Nej |
| Post - ATR-skema | Nej | Ja (checkbox: "ATR-skema påkrævet") |
| Post - Default inklusion | Nej | Ja (checkbox: "Inkludér post per default") |
| Post - Udgået toggle | Nej (Aktiv/Inaktiv dropdown) | Ja (toggle switch: Aktiv/Udgået) |
| Admin - Faser | Nej | Ja (Rediger faser) |
| Admin - Medarbejderkategorier | Nej | Ja (Medarbejderkategori admin) |
| Admin - ATR-tekster | Nej | Ja (Standard ATR- og bemandingstekster) |
| Excel-import tilbudsliste | Ja | Nej synligt |

---

## 2. Sitemap & Navigation

### 2.1 Topniveau-navigation

| Lag | Elementer | Type |
|-----|-----------|------|
| **Global topbar (venstre)** | BaneByg (logo) + "Banebyg Teknisk Rådgivning" | Branding |
| **Global topbar (menu)** | Hjem, Papirkurv, Rediger | Globale sidelinks |
| **Global topbar (højre)** | Følger ikke (stjerne), Webstedsadgang | SharePoint standard |
| **Sub-navigation** | Poster \| Udbud \| ATR & Bemanding \| Bilag | Primær app-navigation |
| **Sub-navigation (højre)** | Feedback & Forespørgsler, Eksempeludtræk ▾, Admin ▾ | Handlinger og admin |

### 2.2 Sitemap

```
BaneByg Teknisk Rådgivning (Rod)
├── Forside (Velkomstside)
├── Poster
│   ├── [1] Generelle ydelser
│   │   ├── 1.1 Digitalt samarbejde mellem leverandør og bygherre
│   │   ├── 1.2 Projektstyring
│   │   ├── 1.3 Modtagerkontrol
│   │   ├── 1.4 Dispensationer (BN)
│   │   ├── 1.5 Faglig ledelse
│   │   ├── 1.6 CSM-dokumentation
│   │   ├── 1.7 TSI ydelser
│   │   ├── 1.8 Tekniske forespørgsler
│   │   ├── 1.10 Møder med Banedanmark
│   │   ├── 1.11 Arbejdsmiljø ydelser
│   │   ├── 1.12 Bæredygtighed
│   │   ├── 1.12–1.14 XXX (UDGÅET)
│   │   └── 1.X Projektspecifikke arbejder ifm. Indledning
│   ├── [2] Banebyg
│   ├── [3] Spor
│   │   ├── 3.1 Banedanmark grundlag
│   │   ├── 3.2 Spor 01
│   │   ├── 3.3 Dispensationsansøgninger
│   │   ├── 3.4 Spor 02
│   │   ├── 3.5 Dispensationsansøgninger
│   │   ├── 3.6 Faglig ledelse - runde 1
│   │   ├── 3.7 Spor 03
│   │   ├── 3.8 Faglig ledelse - runde 2
│   │   ├── 3.9 Assistance under udbudsprocessen
│   │   ├── 3.10 Projektgennemgang for vindende entreprenør
│   │   ├── 3.11 Projektopfølgning i udførelsen
│   │   ├── 3.12 CSM i udførelsesfasen
│   │   └── 3.13 As built-dokumentation
│   ├── [4] Banens underbygning (UDGÅET)
│   ├── [5] Afvanding (UDGÅET)
│   ├── [6] Føringsveje
│   │   ├── 6.1 Banedanmark grundlag
│   │   ├── 6.2 Føringsveje 01
│   │   └── 6.3 Dispensationsansøgninger
│   ├── [7] Veje (UDGÅET)
│   ├── [8] Perroner (UDGÅET)
│   ├── [9] Kørstrøm (UDGÅET)
│   ├── [10] Sikling (UDGÅET)
│   ├── [11] Stærkstrøm (UDGÅET)
│   ├── [12] Konstruktioner
│   ├── [13] Miljø (UDGÅET)
│   ├── [14] Arealer (Fagpakke skabelon) (UDGÅET)
│   ├── [15–18] XXX (UDGÅET)
│   ├── [19] Banebyg
│   ├── [20] Generelle ydelser
│   ├── [21] Definitionsfase (UDGÅET)
│   ├── [22] Programfasen
│   ├── [23] Projekteringsfase
│   ├── [24] Udførelsesfase
│   └── [25] Afslutningsfase
├── Udbud
│   ├── Udbud-liste (filtrerbar)
│   └── [Per Udbud] Poster-editor med udbudsspecifik tilpasning
├── ATR & Bemanding
│   ├── ATR-liste (grupperet per udbud)
│   ├── [Per ATR] ATR Info (modal)
│   ├── [Per ATR] ATR-skema (editor)
│   └── [Per ATR] Bemandingsplan (preview)
├── Bilag
│   └── Bilag-liste (filtrerbar, redigerbar)
└── Admin
    ├── Sektioner (CMS-redigering af forside)
    ├── Indstillinger
    └── ATR og Bemandingsindstillinger
        ├── Standard ATR- og bemandingstekster
        ├── Rediger faser
        └── Medarbejderkategori admin
```

---

## 3. Skærmbeskrivelser

### 3.1 Forside (Velkomstside)
- **URL/sti:** `/sites/ANL12308/SitePages/Raadgiver.aspx`
- **Formål:** Introduktion, rolleforklaring, kontakt og vejledningslinks
- **Layout:** Mørk grågrøn baggrund (mørkere end BBE). To-kolonner i footer.
- **Komponenter:**

| Komponent | Type | Placering | Adfærd |
|-----------|------|-----------|--------|
| Velkomstoverskrift | H1 | Centreret | "Velkommen til Banebyg Teknisk Rådgivning" |
| Platformsbeskrivelse | Brødtekst | Under overskrift | Beskriver formål: udbudsmateriale for teknisk rådgivning |
| Sektionsforklaring | Bulletliste (4 pkt.) | Centreret | Poster, Udbud, Bilag, **ATR & Bemanding** |
| Admin-note | Kursiv tekst | Under bullets | "*'Poster' og 'Bilag' kan kun tilgås af administratorer.*" |
| Journaliseringsinfo | Brødtekst | Under note | SPO-linking, journalisering |
| Kontakt Information | Boksseksjon | Footer venstre | Banebyg@bane.dk, ask@bane.dk |
| Vejledning | Boksseksjon | Footer højre | Guide til Ejer, Bruger, **ATR & Bemanding**, Adgangsstyring (links markeret "Link virker ikke") |

- **Screenshot-reference:** Video BBTR: 00:00–00:09

---

### 3.2 Poster — Liste
- **URL/sti:** Poster-tab
- **Formål:** Overblik over alle fagposter med 25 rodniveauer (mange markeret UDGÅET)
- **Layout:** Identisk med BBE. Mørk baggrund, hvid tekst.
- **Komponenter:** Søgefelt, "Søg kun i postnr./titel" checkbox, "+ Opret ny post" knap, hierarkisk post-liste med expand-pile
- **Forskelle fra BBE:**
  - 25 rodniveau-poster (vs 17 i BBE)
  - Mange poster markeret "(UDGÅET)" med orange/gul tekst
  - Poster inkluderer fasebaserede poster (22–25: Programfasen, Projekteringsfase, Udførelsesfase, Afslutningsfase)
- **Screenshot-reference:** Video BBTR: 00:14–00:19

---

### 3.3 Poster — Post-editor
- **URL/sti:** Inline editor (split-view)
- **Formål:** Opret/rediger fagpost med tilhørende metadata, bilag og ATR-indstillinger
- **Layout:** Split-view: venstre = navigations-træ, højre = editor
- **Komponenter (forskelle fra BBE markeret med ★):**

| Komponent | Type | Placering | Note |
|-----------|------|-----------|------|
| Titel + Status toggle | H2 + Toggle | Top | **★ Toggle switch: Aktiv/Udgået** (vs dropdown i BBE) |
| Version | Label | Under titel | F.eks. "Version: 6.0" |
| Post type | Dropdown | Editor | Værdier: **"Fagpost"**, **"Post"** (vs "Hovedpost"/"Underpost" i BBE) |
| Fagpost* | Dropdown | Editor | Påkrævet. F.eks. "Generelle ydelser" |
| **★ Hovedpost*** | Dropdown | Editor | **Påkrævet. F.eks. "Dispensationer (BN)". Ikke i BBE.** |
| Nr. | Tekstfelt | Editor | F.eks. "1.4.1" |
| Navn* | Tekstfelt | Editor | Påkrævet |
| Beskrivelse | Rich text editor | Editor | WYSIWYG |
| Bilag | Sektion | Editor | **★ Viser tilknyttede bilag med × lukknap** (f.eks. "Bilag 7 Teknisk Forespørgsel (Skabelon) ×") + "Tilføj bilag" |
| Tillad udbudsspecifik post | Checkbox | Bund | Identisk med BBE |
| **★ Tillad ikke udbudsspecifikke kommentarer...** | Checkbox | Bund | **Blokerer kommentarer for fagpost inkl. underliggende poster** |
| Standardteksten kan tilpasses | Checkbox | Bund | Identisk med BBE |
| **★ ATR-skema påkrævet** | Checkbox | Bund | **Unik for BBTR — kræver ATR-skema for denne post** |
| **★ Inkludér post per default** | Checkbox | Bund | **Unik for BBTR — post inkluderes automatisk i nye udbud** |
| Gem ændringer / Annuller | Knapper | Bund | Identisk med BBE |

- **Screenshot-reference:** Video BBTR: 00:24–00:49

---

### 3.4 Poster — Ny post
- **URL/sti:** Åbnes via "+ Opret ny post"
- **Formål:** Opret helt ny post
- **Layout:** Samme editor men med toggle "Aktiv" (off per default) og tomme felter
- **Felter:** Post type, Fagpost*, Hovedpost* (vises kun for "Post" type), Nr., Navn*, Beskrivelse, Bilag, Checkboxes
- **Screenshot-reference:** Video BBTR: 05:39–06:04

---

### 3.5 Udbud — Liste
- **URL/sti:** Udbud-tab
- **Formål:** Oversigt over alle udbud
- **Layout:** Identisk layout med BBE men med færre kolonner
- **Komponenter:**

| Komponent | Type | Adfærd |
|-----------|------|--------|
| Filterdropdown | Dropdown | "Mine aktive udbud" (default) |
| Søgefelt | Input | "Søg på projektnavn eller nr." |
| Årsfilter | Dropdown | "Vælg år" |
| "+ Nyt udbud" | Primær knap | Åbner Nyt udbud-modal |

**Tabelkolonner (Udbud-liste):**

| Kolonne | Note |
|---------|------|
| Checkbox | Selektion |
| Projektnummer- og navn | F.eks. "001 Skabelon", "NFSP0592 Aalborg-Frederikshavn (del 2)" |
| Revision | F.eks. 1.0 |
| Beskrivelse | F.eks. "Skabelon", "Fagpakke Føringsveje & Perroner" |
| Offentliggørelsesdato | F.eks. 19-01-2026 |
| Status | "Aktiv" |
| Rediger udbudsinfo | Ikon |
| Tilføj/rediger ... | Ikon |
| Preview | Ikoner |
| Udtræk | Ikon |
| Kommentarer | 💬 + tal |
| Version | F.eks. 33.0, 169.0, 63.0, 466.0 |
| Bilag | "Vis bilag" |

**★ Manglende kolonner (vs BBE):** Delentreprisenavn- og nummer, Importer tilbudsliste

**Kendte udbud (observeret):**

| Projektnr | Navn | Beskrivelse | Version |
|-----------|------|-------------|---------|
| 001 | Skabelon | Skabelon | 33.0 |
| NFSP0592 | Aalborg-Frederikshavn (del 2) | Fagpakke Føringsveje & Perroner | 169.0 |
| 0001 | Test Workspace/legeplads (Hovedrådgivers ydelsesbeskrivelse (RY)) | Test Workspace... | 63.0 |
| H1004_01 | Kapacitetsudvidelse og hastighedsopgradering ved Ringsted Station - Fjenneslev | Kapacitetsudvidelse... | 466.0 |
| NFSP0527 | Sportfornyelse (Hovedgård) – (Aarhus) | Sportfornyelse... | 5.0 |

- **Screenshot-reference:** Video BBTR: 00:54–01:09

---

### 3.6 Nyt / Rediger udbud (modal)
- **URL/sti:** Modal overlay
- **Formål:** Opret eller rediger udbud stamdata
- **Layout:** Centreret modal (~500px bred)
- **Komponenter:**

| Komponent | Type | Påkrævet | Note |
|-----------|------|----------|------|
| **Stamdata** (sektionsheader) | Label | — | |
| Projektnr.* | Tekstfelt | Ja | |
| Projektnavn* | Tekstfelt | Ja | |
| Beskrivelse | Tekstfelt | Nej | |
| Offentliggørelsesdato* | Datovælger | Ja | Calendar picker med måned+år navigation |
| Status* | Dropdown | Ja | "Aktiv" |
| **★ Fase*** | **Dropdown** | **Ja** | **Unik for BBTR. F.eks. "Detail". Påkrævet.** |
| Link til projekt site* | URL-felt | Ja | |
| **Deling** (sektionsheader) | Label | — | |
| Eksterne rådgivere | Tekstfelt med ℹ | Nej | |
| Fremhæv udbud for | Tekstfelt med ℹ | Nej | |
| "Nyt udbud" / "Gem ændringer" | Primær knap | — | Knaptekst afhænger af opret/rediger |
| "Annuller" | Sekundær knap | — | |

**★ Manglende felter (vs BBE):** Delentreprisenr., Delentreprisenavn, Projekt stadier (hele sektionen)

- **Screenshot-reference:** Video BBTR: 01:09–01:34

---

### 3.7 Udbud — Poster-editor
- **URL/sti:** Åbnes via Tilføj/rediger-ikon
- **Formål:** Tilpas poster i udbudskontekst
- **Layout:** Identisk med BBE: to-kolonner (basistekst venstre, udbudsspecifik kommentar højre)
- **Komponenter:** Identiske med BBE (checkbox pr. post, expand, blyant-redigering, "Se/hent basistekst fra nyeste version", kommentartæller, Gem/Annuller, Vedhæft bilag)
- **Ekstra funktioner:**
  - **"Hent basistekst fra nyeste version" modal**: Popup der viser fuld basistekst med knapper "Hent basistekst fra nyeste version" | "Annuller"
  - **"Opdaterer data..." knap**: Synlig under redigering, indikerer auto-save/refresh
  - **"Tilføj udbudsspecifik post"** knap: Tilføjer ny underpost specifikt for dette udbud
- **Poster i udbud-kontekst (aktive, observeret):**
  - 1.1–1.12 (Generelle ydelser underposter)
  - 2 Banebyg
  - 3 Spor (med underposter 3.1–3.13)
  - 6 Føringsveje (med underposter 6.1–6.3)
  - 12 Konstruktioner
  - 19 Banebyg
  - 20 Generelle ydelser
  - 22 Programfasen
  - 23 Projekteringsfase
  - 24 Udførelsesfase
  - 25 Afslutningsfase

- **Screenshot-reference:** Video BBTR: 01:44–03:14

---

### 3.8 ATR & Bemanding — Liste (★ UNIKT FOR BBTR)
- **URL/sti:** ATR & Bemanding-tab
- **Formål:** Oversigt over alle ATR'er (Arbejds-, Tids- og Ressourceskemaer) grupperet per udbud
- **Layout:** Fuld bredde. Header "ATR & Bemanding". Filterdropdown + søgefelt + årsfilter.
- **Komponenter:**

| Komponent | Type | Placering | Adfærd |
|-----------|------|-----------|--------|
| Filterdropdown | Dropdown | Toolbar venstre | "Se mine ATR'er" (default) |
| Søgefelt | Input | Toolbar midt | "Søg på udbud eller ATR-nr." |
| Årsfilter | Dropdown | Toolbar højre | "Vælg år" |
| Grupperet tabel | Datatabel | Hoved-areal | Grupperet per udbud med expand/collapse |

**Tabelkolonner:**

| Kolonne | Indhold | Handling |
|---------|---------|---------|
| Expand (▼) | Gruppeheader | Folder udbud-gruppe ud/ind |
| ATR navn- og nummer | F.eks. "Sporges 2030.01", "Programfasen 2220.01" | Link |
| Kontrakt navn- og nummer | F.eks. "12 12", "13 13", "sdfds" | Tekst |
| Udbud - Fagpost | F.eks. "Hassan Teste Projekt", "Kapacitetsudvidelse og ha..." | Tekst |
| Start | Dato, f.eks. "26-11-2025" | Tekst |
| Slut | Dato, f.eks. "26-11-2025" | Tekst |
| Status | "Aktiv" | Badge |
| Rediger ATR info | Ikon (📝) | Åbner ATR Info-modal |
| Udfyld ATR-skema | Ikon (📋) | Åbner ATR-skema editor |
| Preview ATR | Ikon (👁) | Preview ATR-dokument |
| Preview Bemandingsplan | Ikon (📊) | Preview bemandingsplan |
| Version | F.eks. 0.0, 1.0, 2.0 | Tal |
| Import hist | "Vis" | Link til import-historik |

**Gruppeheaders (observeret):**
- "Hassan Teste Projekt (11)" — 11 ATR-rækker
- "Kapacitetsudvidelse og hastighedsopgradering ved Ringsted Station - Fjenneslev (16)"
- "Skabelon (3)"
- "Sportfornyelse (Hovedgård) – (Aarhus) (1)"
- "Test bilag nr (1)"
- "Test Workspace/legeplads (Hovedrådgivers ydelsesbeskrivelse (RY)) (4)"

**ATR-navngivningsmønster:** `[Fagpostnavn] [Nummer].[Udbudsnr]`
- F.eks. "Sporges 2030.01", "Banens underbygning 1040.01", "Konstruktioner 2120.01"

- **Screenshot-reference:** Video BBTR: 03:19–04:44

---

### 3.9 ATR Info (modal) (★ UNIKT FOR BBTR)
- **URL/sti:** Modal overlay fra Rediger ATR info-ikon
- **Formål:** Rediger metadata for en specifik ATR
- **Layout:** Centreret modal (~500px bred). Mørk baggrund med hvide felter.
- **Komponenter:**

| Felt | Type | Påkrævet | Eksempel/Værdiliste |
|------|------|----------|---------------------|
| Udbudsform* | Dropdown | Ja | "Normal" |
| Ændringsydelse | Toggle (Ja/Nej) | Nej | Default: Nej |
| Loft | Tekstfelt | Nej | Tom |
| BDK Projektleder | Tekstfelt | Nej | "BDK Projektleder" (placeholder) |
| BDK Ledelsesrepræsentant | Tekstfelt | Nej | "BDK Ledelsesrepræsentant" |
| Godkendt af | Tekstfelt | Nej | "Godkendt af" |
| Rådgiver repræsentant | Tekstfelt | Nej | "Rådgiver repræsentant" |
| Eksterne rådgivere | Tekstfelt med ℹ | Nej | "Eksterne rådgivere" |
| "Gem ændringer" | Primær knap | — | |
| "Annuller" | Sekundær knap | — | |

- **Screenshot-reference:** Video BBTR: 03:44

---

### 3.10 ATR-skema (editor) (★ UNIKT FOR BBTR)
- **URL/sti:** Fuldside under ATR & Bemanding
- **Formål:** Udfyld ATR-skema med overordnet beskrivelse, omfang, ressourcer og kategorier
- **Layout:** Fuld bredde. Warning-banner øverst (hvis manglende data). Felter vertikalt.
- **Komponenter:**

| Komponent | Type | Placering | Adfærd |
|-----------|------|-----------|--------|
| Warning-banner | Info-boks (gul) | Øverst | "Du mangler at angive start- og estimeret slutdato for ATR'en fra dens ATR info" |
| Overordnet beskrivelse | Textarea | Hovedindhold | Fritekst — beskrivelse af ATR |
| Omfang af ydelsen | Textarea | Under beskrivelse | Fritekst — hvad ydelsen omfatter |
| Ressourcer | Textarea | Under omfang | Fritekst — ressourcer |
| Kategorier | Dynamisk liste | Under ressourcer | Dropdown-elementer med 🗑 slet-knap per kategori |
| "+ Tilføj kategori" | Knap | Under kategorier | Tilføjer ny kategori-dropdown |

**Kategori-dropdown-værdier (observeret):** "Kategori 0" (yderligere værdier konfigureres via Medarbejderkategori admin)

- **Screenshot-reference:** Video BBTR: 04:09–04:14

---

### 3.11 Bilag — Liste
- **URL/sti:** Bilag-tab
- **Formål:** Administrer alle standard-bilag
- **Layout:** Identisk med BBE
- **Komponenter:** Søgefelt, "+ Tilføj bilag", tabel med Id↑, Navn, Version, Aktiv, Bilag relateret til poster, Rediger
- **Upload funktionalitet:** "Overfør fil" panel med fil-vælger + "Uploade" knap + "Annullere"

**Kendte bilag (observeret):**

| Id | Navn | Version | Relateret til |
|----|------|---------|---------------|
| 42 | Bilag 8 Timeliste (Skabelon) | 1.0 | Projektstyring |
| 43 | Bilag 7 Teknisk Forespørgsel (Skabelon) | 1.0 | Tekniske forespørgsler |
| 79 | Dokumentationsplaner.xlsx | 1.0 | Som udtræk-dokumentation (NYT), … |
| 80 | Paradigme_og_eksempel_stadieplan.xlsx | 1.0 | |
| 81 | Slettes | 3.0 | |
| 82 | Projekt-og_ændringslog.xlsx | 1.0 | |
| 83 | Tilbudsliste.xlsx | 1.0 | |
| 84 | Paradigme_Ansøgningsgangsblánket_dispensation.docx | 1.0 | Dispensationer |
| 85 | BBTR Bilag X Dokumentationsplaner (alle fag).xlsx | 2.0 | |
| 86 | BBTR Bilag X Dokumentliste (skabelon for dokumentfortegnelse).xlsx | 1.0 | |

- **Screenshot-reference:** Video BBTR: 04:44–04:59

---

### 3.12 Admin — Sektioner & Indstillinger
- **URL/sti:** Via Admin ▾ dropdown
- **Formål:** CMS-redigering af forsideindhold og indstillinger
- **Layout:** Identisk med BBE
- **Komponenter:**
  - Sektioner: Dropdown → rich text editor → "Gem" / "Til forsiden"
  - Indstillinger: Dropdown → "Gem" / "Til forsiden"
- **Screenshot-reference:** Video BBTR: 06:29–06:54

---

### 3.13 Admin — ATR og Bemandingsindstillinger (★ UNIKT FOR BBTR)
- **URL/sti:** Via Admin ▾ dropdown → ATR og Bemandingsindstillinger
- **Formål:** Konfigurér ATR-standardtekster, faser og medarbejderkategorier
- **Layout:** Fuldside med 3 faner øverst
- **Fane 1: Standard ATR- og bemandingstekster**

| Komponent | Type | Adfærd |
|-----------|------|--------|
| Sektioner dropdown | Dropdown | Værdier: "Hvis ikke andet...", "Vejledning", "Tidsplan", "Normal udbudsform", "Omvendt udbudsform" |
| Rich text editor | WYSIWYG | Redigér standardtekst for valgt sektion |
| "Gem" | Knap | Gemmer ændringer |
| "Til forsiden" | Knap | Navigerer til forsiden |

- **Fane 2: Rediger faser**

| Komponent | Type | Adfærd |
|-----------|------|--------|
| Fase-tabel | Datatabel | Se kolonner nedenfor |
| "+ Tilføj fase" | Knap | Tilføjer ny fase-række |

**Fase-tabelkolonner:**

| Kolonne | Type | Eksempel |
|---------|------|---------|
| Sorterings nr. | Tal | 1, 2, 3, 4, 5, 6 |
| Fase navn | Tekst | "Pre-afgrænsningsfase", "Afgrænsningsfase", "Detail", "Udførelse", "Afslutning", "Test" |
| Fase nr. | Tal | 1, 1, 1, 2, 3, 4, 5, 6 |
| Deaktiveret | Checkbox (✓/☐) | ✓ = fase er deaktiveret og vises ikke i udbud |
| Ændret af | Tekst | "Hassan Mohamed Dahir (HMDR) (10-09-2025)" |
| Rediger | Blyant-ikon | Åbner redigering for fase |

**Kendte faser (observeret):**

| Sort# | Fase | Fase# | Aktiv |
|-------|------|-------|-------|
| 1 | Pre-afgrænsningsfase | 1 | Deaktiveret |
| 1 | Afgrænsningsfase | 1 | Aktiv |
| 2 | Slet | 1 | Deaktiveret |
| 2 | Detail | 2 | Aktiv |
| 3 | Udførelse | 3 | Deaktiveret |
| 4 | Afslutning | 4 | Deaktiveret |
| 5 | Slet | 5 | Deaktiveret |
| 6 | Test | 6 | Deaktiveret |

- **Fane 3: Medarbejderkategori admin**
  - [ANTAGELSE: Konfiguration af medarbejderkategorier brugt i ATR-skema "Kategorier"-dropdown. Ikke fuldt synlig i video.]

- **Screenshot-reference:** Video BBTR: 07:14–07:54

---

## 4. Datamodel

### 4.1 Entitet-oversigt

| Entitet | Beskrivelse | Primærnøgle | Note |
|---------|-------------|-------------|------|
| Post | Teknisk fagpost/basistekst | PostId | Identisk med BBE + ekstra felter |
| Bilag | Standard-bilagsdokument | BilagId | Identisk med BBE |
| PostBilag | Post ↔ Bilag relation | PostId + BilagId | |
| Udbud | Udbudsdokument | UdbudId | Ændret: +Fase, -Delentreprise, -Stadier |
| UdbudPost | Udbud ↔ Post tilpasning | UdbudId + PostId | Identisk med BBE |
| UdbudBilag | Udbud ↔ Bilag relation | UdbudId + BilagId | Identisk med BBE |
| **ATR** | **Arbejds-/tids-/ressourceskema** | **ATRId** | **★ Unik for BBTR** |
| **ATRInfo** | **Metadata for ATR** | **ATRId** | **★ Unik for BBTR** |
| **ATRSkema** | **Skema-indhold for ATR** | **ATRSkemaId** | **★ Unik for BBTR** |
| **ATRKategori** | **Kategorier tilknyttet ATR-skema** | **ATRSkemaId + Rækkefølge** | **★ Unik for BBTR** |
| **Fase** | **Projekt-fase definition** | **FaseId** | **★ Unik for BBTR** |
| **Medarbejderkategori** | **Kategori for bemandingsplan** | **KategoriId** | **★ Unik for BBTR** |
| **ATRStandardtekst** | **CMS-tekster til ATR/bemanding** | **SektionNavn** | **★ Unik for BBTR** |
| Versionslog | Ændringshistorik | LogId | Identisk med BBE |

---

### 4.2 Feltdefinitioner — kun BBTR-specifikke

#### Post (ændringer fra BBE)

| Felt | Type | Påkrævet | Note |
|------|------|----------|------|
| Status | Toggle | Ja | **★ Aktiv/Udgået toggle** (vs dropdown i BBE) |
| PostType | Dropdown | Ja | **★ "Fagpost", "Post"** (vs "Hovedpost"/"Underpost") |
| HovedpostId | Lookup (Post) | Betinget | **★ Påkrævet for PostType="Post". Dropdown-felt.** |
| ATRSkemaPaakraevet | Bool | Nej | **★ Unik for BBTR** |
| InkluderPostPerDefault | Bool | Nej | **★ Unik for BBTR** |
| TilladIkkeUdbudsspecifikkeKommentarer | Bool | Nej | **★ Blokerer kommentarer for fagpost inkl. underliggende** |

#### Udbud (ændringer fra BBE)

| Felt | Type | Påkrævet | Note |
|------|------|----------|------|
| Fase | Lookup (Fase) | Ja | **★ Unik for BBTR. Erstatter Stadier-sektionen.** |
| ~~DelentrepriseNr~~ | — | — | **Fjernet i BBTR** |
| ~~DelentrepriseNavn~~ | — | — | **Fjernet i BBTR** |

#### ATR (★ UNIK FOR BBTR)

| Felt | Type | Påkrævet | Eksempel |
|------|------|----------|---------|
| ATRId | Int (auto) | Ja | PK |
| UdbudId | Lookup (Udbud) | Ja | FK — tilknyttet udbud |
| FagpostId | Lookup (Post) | Ja | FK — hvilken fagpost ATR dækker |
| ATRNavn | Tekst | Ja | Auto-genereret: "[Fagpost] [Nr].[UdbudNr]" |
| ATRNummer | Tekst | Ja | F.eks. "2030.01" |
| KontraktNavn | Tekst | Nej | |
| KontraktNummer | Tekst | Nej | |
| Start | Date | Nej | |
| Slut | Date | Nej | |
| Status | Dropdown | Ja | Aktiv, Inaktiv |
| Version | Decimal | Ja | Auto-increment |

#### ATRInfo (★ UNIK FOR BBTR)

| Felt | Type | Påkrævet | Eksempel |
|------|------|----------|---------|
| ATRId | Lookup (ATR) | Ja | FK (1:1) |
| Udbudsform | Dropdown | Ja | "Normal", "Omvendt" |
| Aendringsydelse | Bool | Nej | Toggle: Ja/Nej |
| Loft | Tekst | Nej | |
| BDK_Projektleder | Tekst | Nej | Personnavn |
| BDK_Ledelsesrepraesentant | Tekst | Nej | |
| GodkendtAf | Tekst | Nej | |
| RaadgiverRepraesentant | Tekst | Nej | |
| EksterneRaadgivere | Tekst | Nej | |

#### ATRSkema (★ UNIK FOR BBTR)

| Felt | Type | Påkrævet | Note |
|------|------|----------|------|
| ATRSkemaId | Int (auto) | Ja | PK |
| ATRId | Lookup (ATR) | Ja | FK (1:1) |
| OverordnetBeskrivelse | Multiline tekst | Nej | |
| OmfangAfYdelsen | Multiline tekst | Nej | |
| Ressourcer | Multiline tekst | Nej | |

#### ATRKategori (★ UNIK FOR BBTR)

| Felt | Type | Påkrævet | Note |
|------|------|----------|------|
| ATRSkemaId | Lookup (ATRSkema) | Ja | FK |
| MedarbejderkategoriId | Lookup (Medarbejderkategori) | Ja | FK |
| Raekkefoelge | Int | Ja | Sorteringsrækkefølge |

#### Fase (★ UNIK FOR BBTR)

| Felt | Type | Påkrævet | Note |
|------|------|----------|------|
| FaseId | Int (auto) | Ja | PK |
| FaseNavn | Tekst | Ja | F.eks. "Detail", "Afgrænsningsfase" |
| FaseNummer | Int | Ja | F.eks. 1, 2, 3, 4 |
| SorteringsNr | Int | Ja | Bestemmmer rækkefølge |
| Deaktiveret | Bool | Ja | Skjult i udbud-dropdown hvis true |
| AendretAf | Person/gruppe | Auto | |
| AendretDato | DateTime | Auto | |

#### Medarbejderkategori (★ UNIK FOR BBTR)

| Felt | Type | Påkrævet | Note |
|------|------|----------|------|
| KategoriId | Int (auto) | Ja | PK |
| KategoriNavn | Tekst | Ja | F.eks. "Kategori 0" |
| Aktiv | Bool | Ja | |

#### ATRStandardtekst (★ UNIK FOR BBTR)

| Felt | Type | Påkrævet | Note |
|------|------|----------|------|
| SektionNavn | Tekst | Ja | PK. "Hvis ikke andet...", "Vejledning", "Tidsplan", "Normal udbudsform", "Omvendt udbudsform" |
| Indhold | Rich Text (HTML) | Nej | CMS-tekst |

---

### 4.3 Relationsdiagram

```
Post (1) ←——— (N) UdbudPost (N) ———→ (1) Udbud
Udbud (1) ←——— (N) ATR (N) ———→ (1) Post [Fagpost]
ATR (1) ←——— (1) ATRInfo
ATR (1) ←——— (1) ATRSkema (1) ←——— (N) ATRKategori (N) ———→ (1) Medarbejderkategori
Udbud (N) ———→ (1) Fase
Post er selvrelationerende: Post (ForaelderPostId) → Post
Post er selvrelationerende: Post (HovedpostId) → Post
```

---

## 5. Brugerflows

### Flow 1: Opret nyt udbud med fase
1. Bruger klikker "Udbud"-tab
2. Klikker "+ Nyt udbud"
3. Modal "Nyt udbud" åbner
4. Udfylder Projektnr.*, Projektnavn*, Offentliggørelsesdato*, Status*, **Fase***, Link til projekt site*
5. Valgfrit: Beskrivelse, Eksterne rådgivere, Fremhæv udbud for
6. Klikker "Nyt udbud"
7. Udbud oprettes — ATR'er auto-genereres per aktiv fagpost i udbud

### Flow 2: Rediger ATR info
1. Bruger navigerer til "ATR & Bemanding"
2. Finder ATR i grupperet liste
3. Klikker Rediger ATR info-ikon
4. Modal "ATR Info" åbner
5. Udfylder/redigerer: Udbudsform, Ændringsydelse, Loft, BDK Projektleder, BDK Ledelsesrepræsentant, Godkendt af, Rådgiver repræsentant, Eksterne rådgivere
6. Klikker "Gem ændringer"

### Flow 3: Udfyld ATR-skema
1. Bruger finder ATR i ATR & Bemanding-liste
2. Klikker Udfyld ATR-skema-ikon
3. ATR-skema editor åbner (fuldside)
4. Udfylder: Overordnet beskrivelse, Omfang af ydelsen, Ressourcer
5. Tilføjer kategorier via "+ Tilføj kategori" dropdown
6. [ANTAGELSE: Gemmer via automatisk gemmefunktion eller dedikeret gem-knap]

### Flow 4: Administrer faser
1. Admin klikker Admin ▾ → ATR og Bemandingsindstillinger
2. Vælger fanen "Rediger faser"
3. Ser fase-tabel med alle faser
4. Klikker "+ Tilføj fase" for at oprette ny
5. Eller klikker blyant-ikon for at redigere eksisterende
6. Afkrydser "Deaktiveret" for at skjule en fase fra udbud-dropdown

### Flow 5: Hent basistekst fra nyeste version
1. Bruger redigerer poster i udbuds-kontekst
2. Ser en post markeret med 🔒 "Se/hent basistekst fra nyeste version"
3. Klikker linket
4. Modal viser fuld basistekst fra nyeste version
5. Klikker "Hent basistekst fra nyeste version" for at opdatere
6. Eller "Annuller" for at beholde nuværende version

---

## 6. Roller & Rettigheder

| Rolle | Poster | Udbud | ATR & Bemanding | Bilag | Admin |
|-------|--------|-------|-----------------|-------|-------|
| Læser | Se (kun) | Nej | Nej | Nej | Nej |
| Bruger | Nej (kun admin) | Se egne + redigér | Se egne ATR'er | Nej (kun admin) | Nej |
| Projektleder | Nej (kun admin) | Se alle + redigér egne | Se alle + redigér egne | Nej (kun admin) | Nej |
| Administrator | Fuld adgang | Fuld adgang | Fuld adgang | Fuld adgang | Fuld adgang |

**Vigtig forskel fra BBE:** I BBTR kan *Poster* og *Bilag* "kun tilgås af administratorer" (jf. forsiden).

---

## 7. Integrationer

| System | Integration | Retning | Note |
|--------|-------------|---------|------|
| SharePoint Online | Basis platform | Begge | SPFx webparts, Lists, Libraries |
| Azure Active Directory | Brugerautentifikation | Indgående | Login, brugernavne |
| SPO Projektsite | Link til projektsite | Udgående | URL-felt i Rediger udbud |
| ProjectWise | [Ref. i basistekst] | Reference | Nævnt i post 1.1 (Digitalt samarbejde) |
| SharePoint Online | Dokumentbibliotek | Begge | Bilag-filer opbevares her |
| Excel export | Tilbudsliste, ATR, Bemandingsplan | Udgående | Preview/udtræk funktioner |
| BIM-systemer | [Ref. i basistekst] | Reference | BIM-modeller nævnt i tekniske poster |

---

## 8. SharePoint-implementeringsplan

### 8a. Datalag — SharePoint-lister

**Identiske med BBE:** BaneByg_Poster (med ekstra kolonner), BaneByg_Bilag, BaneByg_Udbud (ændret), BaneByg_UdbudPoster, BaneByg_UdbudBilag, BaneByg_Versionslog

**★ Ændringer til BBE-lister:**

**BaneByg_Poster — ekstra kolonner:**

| SP Kolonne | Type | Note |
|------------|------|------|
| HovedpostId | Lookup (BaneByg_Poster) | FK til overordnet hovedpost |
| ATRSkemaPaakraevet | Ja/Nej | |
| InkluderPerDefault | Ja/Nej | |
| TilladIkkeKommentarer | Ja/Nej | Blokerer udbudsspecifikke kommentarer |
| ErUdgaaet | Ja/Nej | Status toggle (erstatter Status dropdown) |

**BaneByg_Udbud — ændringer:**

| SP Kolonne | Type | Note |
|------------|------|------|
| FaseId | Lookup (BBTR_Faser) | **★ Nyt felt. Påkrævet.** |
| ~~DelentrepriseNr~~ | — | **Fjernet** |
| ~~DelentrepriseNavn~~ | — | **Fjernet** |

**★ Nye lister (unikke for BBTR):**

**BBTR_ATR:**

| SP Kolonne | Type |
|------------|------|
| Title | Enkelt tekst (ATR-navn) |
| ATRNummer | Enkelt tekst |
| UdbudId | Lookup (BaneByg_Udbud) |
| FagpostId | Lookup (BaneByg_Poster) |
| KontraktNavn | Enkelt tekst |
| KontraktNummer | Enkelt tekst |
| StartDato | Dato |
| SlutDato | Dato |
| Status | Valg (Aktiv; Inaktiv) |
| Version | Tal |

**BBTR_ATRInfo:**

| SP Kolonne | Type |
|------------|------|
| ATRId | Lookup (BBTR_ATR) |
| Udbudsform | Valg (Normal; Omvendt) |
| Aendringsydelse | Ja/Nej |
| Loft | Enkelt tekst |
| BDK_Projektleder | Enkelt tekst |
| BDK_Ledelsesrepraesentant | Enkelt tekst |
| GodkendtAf | Enkelt tekst |
| RaadgiverRepraesentant | Enkelt tekst |
| EksterneRaadgivere | Enkelt tekst |

**BBTR_ATRSkema:**

| SP Kolonne | Type |
|------------|------|
| ATRId | Lookup (BBTR_ATR) |
| OverordnetBeskrivelse | Flerlinjet tekst |
| OmfangAfYdelsen | Flerlinjet tekst |
| Ressourcer | Flerlinjet tekst |

**BBTR_ATRKategorier:**

| SP Kolonne | Type |
|------------|------|
| ATRSkemaId | Lookup (BBTR_ATRSkema) |
| KategoriId | Lookup (BBTR_Medarbejderkategorier) |
| Raekkefoelge | Tal |

**BBTR_Faser:**

| SP Kolonne | Type |
|------------|------|
| Title | Enkelt tekst (Fasenavn) |
| FaseNummer | Tal |
| SorteringsNr | Tal |
| Deaktiveret | Ja/Nej |

**BBTR_Medarbejderkategorier:**

| SP Kolonne | Type |
|------------|------|
| Title | Enkelt tekst (Kategorinavn) |
| Aktiv | Ja/Nej |

**BBTR_ATRStandardtekster:**

| SP Kolonne | Type |
|------------|------|
| Title | Enkelt tekst (Sektionsnavn) |
| Indhold | Flerlinjet tekst (rig tekst) |

---

### 8b. UI-lag — SPFx Webparts

**Identiske med BBE:** BBE-Navigation (tilpasset), BBE-Forside, BBE-PosterListe, BBE-PostEditor, BBE-UdbudListe, BBE-UdbudEditor, BBE-PosterUdbudEditor, BBE-Versionslog, BBE-BilagListe, BBE-Admin

**★ Nye webparts (unikke for BBTR):**

| Webpart | Formål | Teknologi |
|---------|--------|-----------|
| `BBTR-ATRListe` | Grupperet oversigt over ATR'er per udbud med handlingsknapper | SPFx, React |
| `BBTR-ATRInfoModal` | Modal til redigering af ATR metadata | SPFx, React |
| `BBTR-ATRSkemaEditor` | Fuldside editor til ATR-skema (textareas + kategorier) | SPFx, React |
| `BBTR-ATRBemandingsIndstillinger` | Admin: 3-fane interface til ATR-tekster, faser, medarbejderkategorier | SPFx, React |
| `BBTR-FaseAdmin` | Admin: Fase-tabel med CRUD og deaktivering | SPFx, React |
| `BBTR-MedarbejderkategoriAdmin` | Admin: Kategori-tabel med CRUD | SPFx, React |

**Styling:** Mørk gråbrun/koksgrå baggrund (mørkere end BBE's grøn). Hvid tekst. Samme primær accent-farve.

---

### 8c. Logiklag

**Identiske flows med BBE:** Versionslog, Post versionering

**★ Nye flows (unikke for BBTR):**

| Flow/Logik | Trigger | Handling |
|-----------|---------|---------|
| `BBTR-AutoGenererATR` | Nyt udbud oprettet | For hver aktiv fagpost med "Inkludér post per default" → opret ATR-række |
| `BBTR-ATRVersionering` | ATR-skema eller ATRInfo ændret | Increment ATR version |
| `BBTR-FaseValidering` | Udbud oprettet/ændret | Validér at valgt fase er aktiv (ikke deaktiveret) |

---

### 8d. Kendte gaps og workarounds

**Identiske med BBE:** Hierarkisk poster-liste, Rich text diff, Inline redigering, Dokument-generering, URL-routing

**★ Ekstra gaps (unikke for BBTR):**

| Funktionalitet | Problem i SharePoint | Foreslået workaround |
|----------------|----------------------|----------------------|
| ATR auto-generering per fagpost | Kompleks forretningslogik ved udbud-oprettelse | Power Automate flow eller SPFx-baseret server-side logik |
| Grupperet ATR-tabel | SP standard ListView understøtter ikke gruppering med handlingsknapper | Fuld custom SPFx-webpart med React gruppering |
| Dynamiske kategorier i ATR-skema | SP har ikke native dynamiske felter | SPFx-webpart med React state management |
| Fase-administration med deaktivering | SP har ingen native "soft delete" for lookup-værdier | Custom SP-liste med Deaktiveret-kolonne; SPFx filtrerer aktive |
| Preview ATR / Bemandingsplan | Dokumentgenerering med dynamisk indhold | Azure Function til Word/Excel generering; alternativt PnP-Docx |
| ATR-nummerering | Auto-genereret format "[Fagpost] [Nr].[UdbudNr]" | Beregnet kolonne eller SPFx-logik ved oprettelse |

---

## 9. Visuelt Referencekatalog

### 9.1 Nøgle-tidskoder

| Skærm | Tidskode |
|-------|----------|
| Forside (velkomst) | 0:00–0:09 |
| Poster-liste (alle 25 poster) | 0:14–0:19 |
| Post-editor: Generelle ydelser (Fagpost) | 0:24–0:29 |
| Post-editor: underposter med checkboxes + bilag + ATR-skema | 0:34 |
| Post-editor: XXX (Post) med Hovedpost-dropdown + Udgået toggle | 0:39–0:49 |
| Udbud-liste (5 udbud) | 0:54–1:04 |
| Nyt udbud modal (Stamdata + Fase + Deling) | 1:09–1:34 |
| Rediger udbud modal (udfyldt, med "Detail" fase) | 1:39 |
| Poster i udbud-kontekst (poster-editor) | 1:44–2:14 |
| Hent basistekst fra nyeste version (modal) | 1:59–2:04 |
| Post: Dispensationsansøgninger i udbud-redigering | 2:29–2:39 |
| Føringsveje redigering i udbud med tomme felter | 2:49–2:54 |
| ATR & Bemanding liste (grupperet) | 3:19–4:39 |
| ATR Info modal | 3:44 |
| ATR-skema editor | 4:09–4:14 |
| Bilag-liste | 4:49–4:59 |
| Bilag upload ("Overfør fil") | 4:44 |
| Post-editor: Tekniske forespørgsler med bilag tilknyttet | 5:14 |
| Ny post (Fagpost type, tom) | 5:39 |
| Ny post (Post type, Hovedpost-dropdown) | 6:04 |
| Admin: Sektioner + Indstillinger | 6:29–6:54 |
| ATR og Bemandingsindstillinger: Standard tekster | 7:14 |
| ATR og Bemandingsindstillinger: Sektioner dropdown | 7:34 |
| ATR og Bemandingsindstillinger: Rediger faser | 7:54 |

### 9.2 Farve og typografi

| Element | Farve / Stil |
|---------|-------------|
| Baggrund (primær) | Mørk koksgrå/brungrøn ca. #2A2A2A / #333333 |
| Tekst (primær) | Hvid #FFFFFF |
| Links | Lys blå/cyan toner |
| Poster-rækker (udbud-editor) | Mørk grå baggrund med hvid kant |
| UDGÅET-tekst | Orange/gul farvekode |
| Aktiv status toggle | Grøn = Aktiv, Grå = Udgået |
| Modal baggrund | Mørk grå med hvide input-felter |
| Validerings-fejl | Rød tekst ("Påkrævet felt!", "Field is required") |
| Warning-banner (ATR-skema) | Gul baggrund med ⚠-ikon |
| Knapper: Gem | Blå/grøn primær |
| Knapper: Annuller | Grå sekundær |

### 9.3 Logo
- Banedanmark-logo (hvid) øverst til venstre
- "Banebyg Teknisk Rådgivning" tekst i topbar
