# PrintTrack

Webový informační systém pro správu 3D tiskáren, tiskových jobů a skladu filamentu ve sdíleném prostředí (makerspace, školní dílna, kroužek).

## Co systém dělá

1. **Evidence tiskáren** — správa tiskáren, jejich stavu (volná / tiskne / porucha) a historie použití
2. **Správa tiskových jobů** — uživatelé zadávají joby (název, soubor, filament, odhadovaný čas), systém sleduje stav od fronty po dokončení
3. **Sklad filamentu** — evidence cívek (materiál, barva, výrobce, zbývající gramáž), odpočet spotřeby po dokončení jobu

## Proč ne Mainsail / Moonraker?

Mainsail a Moonraker jsou firmware frontend pro jednu tiskárnu — řeší real-time monitoring tisku, teploty a správu souborů.
PrintTrack je manažerský IS *nad* nimi — přidává uživatelské účty, frontu jobů mezi více uživateli, historii a multi-tiskárnovou správu.