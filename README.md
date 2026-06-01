# PrintTrack

Webový informační systém pro správu 3D tiskáren, tiskových jobů a skladu filamentu ve sdíleném prostředí (makerspace, školní dílna, kroužek).

## Perex (koncept projektu)

PrintTrack je manažerský Informační Systém pro koordinaci více 3D tiskáren a uživatelů v jednom sdíleném prostoru. Umožní plánování a frontování tiskových jobů, automatické odečítání spotřebovaného filamentu, správu uživatelů a oprávnění, reporty využití a historii tisků. Cílem je nahradit ruční záznamy, zjednodušit rezervace tiskáren a zlepšit sledování zásob materiálu.

## Hlavní funkčnosti

- Evidence tiskáren: stav, konfigurace, historie a přiřazení jobů
- Správa tiskových jobů: upload, fronta, odhad času, priorita, historie
- Sklad filamentu: evidence cívek, spotřeba, upozornění na nízký stav
- Uživatelské role a oprávnění: student / člen / správce / technik
- Reporting: statistiky využití, spotřeby materiálu, seznam chyb a poruch

## Rozsah projektu pro tento předmět

- Koncept + perex (termín: 27.5.) — hotovo
- Katalog požadavků (funkční + nefunkční) — dokončit do 3.6.
- Diagramy (role/use-cases, třídní/ER, sekvenční, nasazení) — dokončit do 10.6.
- Výstupy: `README.md`, `requirements.md` (katalog požadavků), `diagrams/` (SVG/draw.io)

## Doporučená struktura repozitáře

- `README.md` — tento souhrn + plán
- `requirements.md` — katalog funkčních a nefunkčních požadavků (MarkDown)
- `diagrams/` — SVG nebo draw.io soubory (ER, class, use-case, deployment)
- `docs/` — doplňkové popisy, případné wireframy

## Plán práce (krátce)

1. Dokončit katalog požadavků (funkční + nefunkční) — separátní `requirements.md` (do 3.6.)
2. Navrhnout role a use-case diagramy (role, funkcionalita, scénáře)
3. Navrhnout datový model (ER / UML Class)
4. Navrhnout architekturu a navrhnout technologie (backend, frontend, DB, hosting)
5. Vytvořit diagramy v draw.io a exportovat do SVG
6. Sladit dokumentaci a připravit finální odevzdání

## Technologie (návrh)

- Backend: Node.js + Express nebo Python (Flask/FastAPI)
- Databáze: PostgreSQL (relace pro uživatele, joby, tiskárny, zásoby)
- Frontend: React nebo jednoduchý server-side renderovaný UI
- Diagramy: draw.io / diagrams.net, export SVG
- Volitelně: integrace s OctoPrint / Moonraker API pro real-time stav tiskáren
