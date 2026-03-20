# Příklady použití iPad Reservation Skill

## Základní příklady

### Jednoduchá rezervace (vše volné)

**Tvůj požadavek:**
```
Rezervuj mi 15 iPad na středu 9:00-9:45
```

**Skill zjistí:**
- Středa = 2026-03-18
- Box 3 je zcela volný (301-320)
- Vezme si prvních 15: 301-315

**Potvrzení:**
```
✅ Rezervováno 15 iPadů na středu 9:00-9:45
📱 Zařízení: 301-315
📍 Box 3
📅 Kalendář aktualizován
```

---

### Částečná dostupnost

**Tvůj požadavek:**
```
Rezervuj mi 20 iPad na pondělí 8:45-10:25
```

**Skill zjistí:**
- Pondělí 8:45-10:25: Box 3 má 301-318 rezervované (Petr)
- Box 3 zbývají: 319-320 (jen 2 iPady)
- Box 4 je zcela volný (401-420)
- Box 5 je zcela volný (501-520)

**Skill se zeptá:**
```
V Box 3 zbývá jen 2 zařízení (319-320).

Chceš aby jsem:
1. Vzal 2 z Box 3 + 18 z Box 4? (319-320, 401-418)
2. Vzal všech 20 z Box 4 či Box 5?
3. Vzal jen těch 2, co jsou volné?
```

**Když řekneš "Vezmi 2 + 18":**
```
✅ Rezervováno 20 iPadů na pondělí 8:45-10:25
📱 Zařízení: 319-320 (Box 3) + 401-418 (Box 4)
📍 2 boxy
📅 Kalendář aktualizován
```

---

### Nedostatek iPadů

**Tvůj požadavek:**
```
Rezervuj mi 50 iPad na pátek 10:00-11:00
```

**Skill zjistí:**
- Pátek 10:00-11:00: Box 5 je zcela obsazený (501-520 už rezervované)
- Box 3 zbývá 8 iPadů
- Box 4 zbývá 12 iPadů
- **Celkem dostupných: 20 iPadů** (z 50 požadovaných)

**Skill nabídne:**
```
Máš k dispozici jen 20 volných iPadů (potřebuješ 50).

Dostupné:
- Box 3: 312-320 (9 zařízení)
- Box 4: 408-420 (13 zařízení)

Chceš aby jsem:
1. Rezervoval všech 20 volných?
2. Zvolil jiný čas?
3. Zkušit jiný den?
```

---


## Tipy pro efektivní používání

1. **Buď specifický s časem** — "8:45-10:25" je lepší než "dopoledne"
2. **Zeptej se, pokud není dost** — skill nabídne co dělat
3. **Řekni skill, ať si vezme jiný box** — "Vezmi z Box 5 místo Box 3"


