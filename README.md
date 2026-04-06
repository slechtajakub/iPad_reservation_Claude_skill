<img width="800"  alt="iPad_reservation_agent" src="https://github.com/slechtajakub/iPad_reservation_Claude_skill/blob/main/example-ipad-reservation.png?raw=true" />

# iPad Reservation Skill

Automatická rezervace iPadů v Google Calendar — Claude skill pro učitele.

## 🎯 Co umí?

Řekneš si: **"Rezervuj mi 18 iPad na pondělí 8:45-10:25"**

Skill automaticky:
- ✅ Zkontroluje dostupnost ve všech 3 boxech iPadů (box po 20 kusech)
- ✅ Najde volná zařízení
- ✅ Vytvoří rezervaci v Google Calendar
- ✅ Potvrdí, co se podařilo

Zvládá i situace, kdy není dost iPadů — nabídne alternativy nebo rezervuje jen kolik je volného.

## 📋 Dostupné iPady

| Box | Zařízení | Počet | Google Calendar ID |
|-----|----------|-------|-------------------|
| 3   | 301–320  | 20    | `url Google Calendar` |
| 4   | 401–420  | 20    | `url Google Calendar 2` |
| 5   | 501–520  | 20    | `url Google Calendar 3` |

**Celkem: 60 iPadů**

## 🚀 Začínáme

### Instalace

1. Stáhni soubor `SKILL.md` z tohoto repozitáře
2. Přidej jej do Claude Skills v nastavení
3. Nebo zkopíruj obsah do `Claude.md` v Cowork OS

### Použití

Stačí říci:
```
Rezervuj mi 15 iPad na úterý 10:30-11:15
```

nebo

```
Potřebuji 20 iPad v pátek na 8:45-10:25
```

Skill se zeptá na detaily, pokud jsou nejasné, a potvrdí rezervaci.

##  Interní fungování

Skill pracuje s:
- **Google Calendar API** (`gcal_list_events`, `gcal_create_event`)

### Algoritmus rezervace

1. Parsuje tvůj požadavek → počet iPadů, den, čas
2. Kontroluje 3 boxy v Google Calendar
3. Zjišťuje, která zařízení jsou volná
4. Vybere prioritně z jednoho boxu (nebo je kombinuje, pokud je potřeba víc než 20)
5. Vytvoří event v kalendáři s formátem: `"XXX-YYY Jméno"` (např. `"301-318 Jakub"`)
6. Potvrdí rezervaci s čísly zařízení a lokalitou boxu

## Poznámky

- Vždy se používá školní účet 
- Název rezervace jasně označuje čísla iPadů (např. `"301-318 Jakub"`)
- Ostatní učitelé vidí, která zařízení jsou rezervována


## Vytvořil

Jakub Šlechta, Brno 2026
