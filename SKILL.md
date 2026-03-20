---
name: ipad-reservation
description: Automatická rezervace iPadů v Google Calendar. Použij když potřebuješ iPady do vyuky - staci říci "rezervuj mi X iPad na [pondělí/úterý/atd] [čas]" a já budu automaticky hledat volné zařízení, kontrolovat dostupnost boxů a vytvářet rezervaci. Ideální pro učitele, kteří potřebují rychlé rezervace bez ruční kontroly kalendáře. Zvládám situace kdy není dost iPadů - nabídnu alternativy nebo rezervuji jen kolik je volného.
compatibility: |
  - Google Calendar API (gcal_list_events, gcal_create_event)
---

# iPad Reservation Skill

## Quick Start

Just tell me: **"Rezervuj mi [počet] iPad na [den] [čas]"**

Examples:
- "Rezervuj mi 20 iPad na pondělí 8:45-10:25"
- "Potřebuji 15 iPad v pátek na 9:00-9:45"
- "Vyrezeruj mi 10 iPad na úterý od 11:00"

I'll automatically:
1. ✅ Check availability in all 3 iPad boxes
2. ✅ Find available devices
3. ✅ Create a calendar reservation with device numbers
4. ✅ Confirm what you got

---

## iPad Inventory

**Three Google Calendar boxes:**
- **Box 3** → devices 301–320 (20 total)
  - Calendar ID: `vlož url`

- **Box 4** → devices 401–420 (20 total)
  - Calendar ID: `vlož url`

- **Box 5** → devices 501–520 (20 total)
  - Calendar ID: `vlož url`

---

## The Workflow

### Step 1: Parse the request
Extract three things from what you say:
- **How many iPads?** (e.g., 15, 20)
- **Which day?** (pondělí, úterý, středa, čtvrtek, pátek → convert to date: today is 2026-03-14, so pondělí = 2026-03-16)
- **What time?** (e.g., 8:45-10:25, 9:00-9:45)

### Step 2: Check availability
For each of the three boxes, call `gcal_list_events()` on that calendar ID for the requested day and time window.

**How to read the results:**
- Event summary shows what devices are booked (e.g., "301-318 Jakub" = devices 301 to 318 are taken)
- "celý box" or "#celý box" = all 20 devices in that box are occupied
- Devices NOT mentioned in any event = FREE

**Example analysis:**
```
Box 3 (301-320):
  - Found event "301-318 Jakub" from 8:45-10:25
  - Result: devices 319-320 are free (2 devices)

Box 4 (401-420):
  - No events at this time
  - Result: all 20 devices free (401-420)

Box 5 (501-520):
  - Found event "501-510 M7" from 10:45-11:30
  - At your time (8:45-10:25), no conflict
  - Result: all 20 devices free (501-520)
```

### Step 3: Select devices
**Priority:** Always choose from ONE box first if possible. Only split across boxes if you need more than 20.

If one box has enough free devices, take them from that box.
If not, combine boxes (Box 3 first, then Box 4, then Box 5).

**Examples:**
- Need 18 iPad? → Take 301-318 from Box 3 (all free)
- Need 15 iPad? → Take 511-525... wait, that's only 10 free. Use 501-515 from Box 5 instead
- Need 25 iPad? → Can't fit in one box. Take all 20 from Box 3 (301-320), then 5 from Box 4 (401-405)

### Step 4: Create the reservation
Call `gcal_create_event()` with:
- **Calendar ID:** Use the calendar ID of the box you chose
- **Summary/title:** Format: `"XXX-YYY Name"` (device numbers + name)
  - Example: `"301-318 Jakub"` or `"511-520 Jakub"`
- **Start time:** RFC3339 format with Prague timezone (Europe/Prague)
  - Example: `2026-03-16T08:45:00+01:00`
- **End time:** Same format
  - Example: `2026-03-16T10:25:00+01:00`

### Step 5: Confirm
Report back:
- ✅ Devices reserved (e.g., "301-318")
- 📅 Date and time
- 📍 Which box (Box 3, 4, or 5)

---

## Edge Cases

**Not enough devices available?**
- Explain what's booked and what's free
- Ask: "Want me to reserve just the [X] free devices?" or "Want a different time?"
- If user agrees, reserve only what's free with that number

**Multiple days or times?**
- Make separate reservations for each day/time — don't combine into one event

**Need to change/cancel?**
- Cancellations are outside this skill (handled separately)

---

## Important Details

- **Always use device numbers in the event title** — this is how others see what's booked
- **Account:** Always use `school email` (school account, not personal)
- **Timezone:** Prague time (Europe/Prague, +01:00 in March)
- **Naming:** Title is always "XXX-YYY NAME" — that's how others identify your reservations
