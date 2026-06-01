# Architektura a nasazení — PrintTrack

Tento dokument popisuje navrženou architekturu systému, komponenty a doporučené způsoby nasazení.

## Vysoká úroveň

- Frontend: SPA (React) nebo server-side renderovaný HTML pro jednoduché nasazení.
- Backend: REST API (Node.js + Express nebo Python FastAPI). Zpracování dlouhých operací (scheduling, integrace) přes background worker.
- Databáze: PostgreSQL pro relační data (users, jobs, printers, spools).
- Objektové úložiště: lokální disk nebo S3-compatible storage pro nahrané soubory (gcode).
- Scheduler/Worker: samostatný proces (celery / RQ / Bull) pro přiřazování jobů a komunikaci s tiskárnami.

## Komponenty

1. Web Client
   - UI pro nahrávání jobů, správu tiskáren, inventory.
2. API Server
   - Auth, CRUD operace, business logika, validace.
3. Worker / Scheduler
   - Periodicky vyhodnocuje frontu, přiřazuje joby, volá integrace s OctoPrint/Moonraker.
4. Databáze
   - Relace: `users`, `print_jobs`, `printers`, `filament_spools`, `maintenance_reports`.
5. Storage
   - Ukládá nahrané soubory a případné zpracované artefakty.

## Datový tok (příklad)

1. Uživatel nahrává job přes Web Client -> API uloží soubor do Storage, vytvoří záznam `print_jobs`.
2. Worker vezme první ready job -> najde vhodnou tiskárnu (shodný materiál/volná) -> pošle task do PrinterService (OctoPrint)
3. Po dokončení tiskárna notifikací (webhook) nebo poll worker aktualizuje `print_jobs` a odečte `filament_spools.grams_left`.

## Integrace s externími službami

- OctoPrint / Moonraker: použití REST API pro start/stop a polling stavů.
- SMTP / WebPush: notifikace o dokončení nebo nízkém stavu.

## Bezpečnost a provoz

- HTTPS (Let's Encrypt) + bezpečné uložení tajemství (env vars, secret manager).
- Minimální RBAC: oddělené role v DB a enforcement v API vrstvě.
- Zálohy: pravidelný dump PostgreSQL a záloha storage.

## Nasazení (doporučení)

- Vývoj: Docker Compose (Postgres, Redis, API, Worker, Web)
- Produkce: kontejnerizace (Docker) + orchestrátor (k8s) nebo PaaS (DigitalOcean App Platform / Heroku-like)
- Cron/Worker: Redis jako fronta zpráv (Bull / RQ / Celery)

## Monitoring & Logging

- Logování: strukturované JSON logy; centralizace (ELK/Graylog).
- Metrics: Prometheus + Grafana pro sledování latencí a využití workerů.

## Schéma sítí a portů

- Frontend: 80/443
- API: 443 (interně 8000)
- DB: soukromá síť, port 5432
- Redis: soukromá síť, port 6379

## Poznámky k škálovatelnosti

- Stateles backend instance => horizontální škálování
- Worker pool škálovatelný podle počtu jobů
- Storage: S3 pro škálovatelné ukládání velkých souborů

---

Vizualizace architektury je v `diagrams/deployment.svg`.
