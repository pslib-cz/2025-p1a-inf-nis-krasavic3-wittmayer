# Katalog požadavků — PrintTrack

Tento dokument obsahuje funkční a nefunkční požadavky informačního systému PrintTrack.

## Cíle systému

- Poskytnout centrální správu více 3D tiskáren ve sdíleném prostředí.
- Umožnit uživatelům zadávat a sledovat tiskové joby v frontě.
- Spravovat sklad filamentů a automaticky odečítat spotřebu.
- Nabídnout role a oprávnění (uživatel, technik, správce) a reporting využití.

## Stakeholdeři

- Studenti / členové (koneční uživatelé)
- Technik (údržba tiskáren, řešení poruch)
- Správce (nastavení systému, uživatelské účty, reporting)
- Administrátor sítě / provozovatel makerspace

## Označení priorit

- MUST: kritické pro minimální funkčnost
- SHOULD: důležité, ale ne kritické pro MVP
- MAY: rozšíření / budoucí funkce

---

## Funkční požadavky (FR)

FR-01 (MUST) — Správa uživatelů
- Vytvoření, úprava a smazání uživatelských účtů.
- Role: `user`, `technician`, `admin`.

FR-02 (MUST) — Autentizace a autorizace
- Přihlášení (username/password). Podpora JWT session nebo server-side session.
- Role-based access control (RBAC).

FR-03 (MUST) — Evidence tiskáren
- Přidání/úprava/odebrání tiskáren s atributy (jméno, model, umístění, parametry, status).
- Statusy: `available`, `printing`, `maintenance`, `offline`.

FR-04 (MUST) — Zadání tiskového jobu
- Uživatel nahraje soubor (gcode/zip) a zadá meta informace (název, filament, počet kusů, priority).
- Systém uloží soubor a vloží job do fronty.

FR-05 (MUST) — Fronta a plánování jobů
- Systém spravuje frontu jobů, přiřazuje joby dostupným tiskárnám podle pravidel (priority, materiál, odhad času).
- Možnost zrušit nebo pozastavit job.

FR-06 (SHOULD) — Odhad času a spotřeby
- Zobrazení odhadovaného času tisku a odhadované spotřeby filamentu při zadání jobu.

FR-07 (MUST) — Evidence a správa zásob filamentu
- Přidání cívek s atributy (materiál, barva, výrobce, hmotnost, grams_left).
- Po dokončení jobu se odečte skutečná/odhadem spotřeba z vybrané cívky.

FR-08 (SHOULD) — Upozornění na nízký stav
- Systém generuje upozornění (e-mail/notification) při poklesu grams_left pod prahem.

FR-09 (SHOULD) — Historie a logy
- Záznam historie jobů (kdo, kdy, jaký soubor, použité parametry, výsledek).

FR-10 (MUST) — Správa oprav a poruch
- Technik může evidovat hlášení poruch, přiřadit k tiskárně a změnit stav (otevřeno/zavřeno).

FR-11 (SHOULD) — Reporting a statistiky
- Export základních reportů: využití tiskáren, spotřeba materiálu, nejčastější uživatelé.

FR-12 (MAY) — Integrace s OctoPrint / Moonraker
- Volitelná integrace pro získání real-time statusu tiskáren a spouštění tisků.

FR-13 (MAY) — REST API
- Poskytnutí REST API pro integrace (zadávání jobů, dotaz na stav).

FR-14 (SHOULD) — Role-based UI
- Zobrazit ovládací prvky podle role (technici vidí údržbu, admin vidí nastavení systému).

FR-15 (MAY) — Import/Export dat
- CSV export historie, import seznamu cívek.

---

## Nefunkční požadavky (NFR)

NFR-01 (MUST) — Bezpečnost
- HTTPS pro veškerou komunikaci.
- Hesla uložena bezpečně (bcrypt/argon2).
- RBAC, auditní logy akcí adminů.

NFR-02 (MUST) — Spolehlivost a dostupnost
- Systém zajišťuje konzistentní uložení jobů a dat; zálohování databáze minimálně jednou denně.

NFR-03 (SHOULD) — Výkon
- Stránka s frontou a seznamem tiskáren by měla odpovídat < 300 ms pro běžné dotazy při malé škole (desítky uživatelů).

NFR-04 (SHOULD) — Škálovatelnost
- Architektura umožní horizontální škálování backendu a workerů.

NFR-05 (SHOULD) — Udržovatelnost
- Čistá API vrstva, testy jednotkové a integrační, CI pipeline.

NFR-06 (MUST) — Ochrana souborů
- Ukládané soubory (gcode) musí být izolovány a přístupné pouze autorizovaným uživatelům.

NFR-07 (MAY) — Lokalizace
- Možnost přidat překlady (CZ/EN) v budoucnu.

NFR-08 (SHOULD) — Logování a monitoring
- Integrace s centralizovaným logováním (např. ELK / Grafana + Prometheus) v případě nasazení.

NFR-09 (MUST) — Kompatibilita
- Podpora běžných moderních prohlížečů (Chrome, Firefox, Edge).

NFR-10 (MAY) — Přístupnost
- Základní WCAG kompatibilita pro klíčové obrazovky.

---

## Připomínky k implementaci

- Prioritizovat FR-01..FR-05 pro MVP.
- Integrace s OctoPrint je volitelná, ale doporučená pro lepší UX.
- Detaily API a datového modelu jsou navrženy v `diagrams/class_er.svg`.
