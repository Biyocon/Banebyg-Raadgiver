# Claude Code Prompt — Videoanalyse & PRD for BaneByg-platformkloning

Brug denne prompt i Claude Code med begge videoer tilgængelige i projektmappen.

---

## PROMPT

```
Du er en senior platform-arkitekt og kravspecialist. Din opgave er at analysere to screenoptagelser af to Banedanmark-platforme og producere én selvstændig, detaljeret PRD per platform, som en udvikler kan bruge til at klone dem 1:1 som SharePoint-baserede løsninger.

## VIDEOER
- Video 1: BaneByg Enterprise (BBE)
- Video 2: BaneByg Rådgiver (BBR / BBTR)

## ANALYSEMETODE

Gennemgå HVER video systematisk i denne rækkefølge:

### Trin 1 — Strukturel kortlægning
- Identificér alle sider, undersider og navigationsniveauer
- Kortlæg sitemap med hierarki (top-nav, side-nav, breadcrumbs)
- Dokumentér URL-mønstre og routinglogik (hvis synlig)

### Trin 2 — UI-komponent-inventar
For HVER unik skærm/view, dokumentér:
- Layout-struktur (grid, kolonner, sektioner)
- Alle UI-komponenter (tabeller, formularer, dropdowns, modaler, kort, faner, knapper, ikoner)
- Komponenttilstande (tom, udfyldt, fejl, loading, hover, aktiv)
- Typografi (overskrifter, brødtekst, labels — beskriv hierarki)
- Farvebrug (primær, sekundær, accent, baggrunde, statusfarver)
- Spacing og alignment-mønstre

### Trin 3 — Datamodel-analyse
- Identificér alle entiteter/objekter (projekter, kontrakter, fagpakker, dokumenter, brugere osv.)
- Kortlæg felter per entitet (feltnavn, datatype, påkrævet/valgfri, værdiliste hvis synlig)
- Relationer mellem entiteter (1:1, 1:N, N:M)
- Statusflows og tilstandsovergange (f.eks. "Kladde → Godkendt → Afsluttet")

### Trin 4 — Funktionalitet & interaktion
- CRUD-operationer per entitet (hvad kan oprettes, redigeres, slettes, arkiveres?)
- Filtrering, sortering, søgning — beskriv præcist hvor og hvordan
- Brugerflows: Dokumentér hvert klikflow fra start til slut
- Rollebaseret adgang (hvis synligt: hvilke roller ser/gør hvad?)
- Validering og fejlhåndtering
- Notifikationer, statusbeskeder, bekræftelsesdialoger

### Trin 5 — Integrationer & data
- Hvilke eksterne systemer refereres (Tracé, QualiWare, SharePoint, ESDH osv.)?
- Import/eksport-funktionalitet (Excel, PDF, CSV)
- API-indikatorer (loading-states, asynkrone operationer)

### Trin 6 — SharePoint-kloningsstrategi
For hver platform, angiv:
- Hvilke SharePoint-komponenter der skal bruges (lister, biblioteker, SPFx webparts, Power Automate flows)
- Datamodellering i SharePoint (lister, kolonner, lookups, beregnede felter)
- Hvad der kræver custom SPFx-udvikling vs. out-of-the-box SharePoint
- Kendte begrænsninger i SharePoint ift. originalplatformen og foreslåede workarounds

## OUTPUT-FORMAT

Producér TO separate dokumenter:

### Dokument 1: PRD — BaneByg Enterprise (Kloning)
### Dokument 2: PRD — BaneByg Rådgiver (Kloning)

Hvert dokument skal følge denne struktur:

```markdown
# PRD: [Platformnavn] — SharePoint-kloning

## 1. Formål & Kontekst
- Hvad platformen gør i dag
- Hvorfor den klones til SharePoint
- Scope: 1:1 funktionel klon

## 2. Sitemap & Navigation
- Komplet sidehierarki (tabel eller træstruktur)
- Navigationstype per niveau

## 3. Skærmbeskrivelser
For HVER unik skærm:
### [Skærmnavn]
- **URL/sti:** ...
- **Formål:** ...
- **Layout:** (beskriv grid/kolonner)
- **Komponenter:** (tabel: komponent | type | placering | adfærd)
- **Data vist:** (hvilke felter fra hvilke entiteter)
- **Brugerhandlinger:** (hvad kan brugeren gøre her)
- **Screenshot-reference:** (tidskode i videoen, f.eks. "Video 1: 03:42")

## 4. Datamodel
- Entitet-oversigt (tabel: entitet | beskrivelse | primærnøgle)
- Feltdefinitioner per entitet (tabel: felt | type | påkrævet | værdiliste | note)
- Relationsdiagram (beskriv verbalt eller som mermaid)
- Statusflows per entitet

## 5. Brugerflows
- Nummererede trin-for-trin flows for alle kerneopgaver
- Beslutningspunkter og forgreninger
- Fejlscenarier

## 6. Roller & Rettigheder
- Rolleoversigt med tilladelser per skærm/handling

## 7. Integrationer
- Eksterne systemer og dataudveksling
- Import/eksport-specifikationer

## 8. SharePoint-implementeringsplan
### 8a. Datalag
- SharePoint-lister og kolonner (mapning fra datamodel)
- Beregnede kolonner og lookups
- Indholdstyper

### 8b. UI-lag
- SPFx webparts (hvilke, hvad de viser)
- Out-of-the-box komponenter
- Custom CSS/styling-behov

### 8c. Logiklag
- Power Automate flows (triggers, handlinger)
- Beregninger og validering
- Notifikationsflows

### 8d. Kendte gaps & workarounds
- Funktionalitet der ikke kan replikeres 1:1 i SharePoint
- Foreslåede alternativer

## 9. Visuelt Referencekatalog
- Tidskoder fra video for hver nøgleskærm
- Farve- og typografioversigt
- Komponentbibliotek-opsummering
```

## VIGTIGE REGLER
1. Vær UDTØMMENDE — udelad intet du kan se i videoerne
2. Brug TIDSKODER som reference til specifikke frames
3. Adskil FAKTA (hvad du ser) fra ANTAGELSER (hvad du tolker) — markér antagelser med [ANTAGELSE]
4. Hvert felt, hver knap, hver kolonne skal dokumenteres
5. Skriv så en udvikler der ALDRIG har set platformen kan bygge den fra PRD'en alene
6. Output på dansk
```

---

## ANVENDELSE I CLAUDE CODE

1. Placér begge videofiler i din projektmappe
2. Kør prompten med: `Analysér først Video 1 (BBE), producér PRD 1. Derefter Video 2 (BBR), producér PRD 2.`
3. Hvis videoerne er lange (>15 min), kan du opdele: `Start med Trin 1-3 for Video 1, gem output, fortsæt med Trin 4-6`
