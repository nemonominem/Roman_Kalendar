# Roman Calendar — Pending Changes State File

**File to edit:** `/Users/gillesdemaneuf/Work/Publications/RomanCalendar/index.html`
**Current size:** 1656 lines, single self-contained HTML (CSS+JS inline, Google Fonts only external).

---

## STRUCTURE

9 tab sections with line numbers:
- `ts-dualcal` (line 707, active default) — dual calendar center feature
- `ts-beginning` (line 769) — Lunar Beginning
- `ts-republican` (line 789) — Republican Calendar
- `ts-daynames` (line 813) — How Romans Named a Day
- `ts-religion` (line 835) — Religious Dimension / Fasti
- `ts-reform` (line 858) — Caesar's Reform
- `ts-names` (line 895) — Months Renamed
- `ts-consuls` (line 905) — Dating by Consuls
- `ts-converter` (line 950) — Try It Yourself

CSS variables at lines 11-31. Footer/sources at line 975.

---

## PENDING CHANGES (all requested, NONE implemented yet)

### 1. Add source: Hacquard guide
In footer (line 975), add: `G. Hacquard, Guide Romain Antique, Hachette (1952)`

### 2. Increase ALL small font sizes by +2pt (~+0.125rem)
From grep, key values to bump: .62rem→.75, .68rem→.8, .7rem→.83, .72rem→.85, .76rem→.89, .78rem→.9, .8rem→.93, .82rem→.95, .85rem→.98, .88rem→1.0, .9rem→1.03, .92rem→1.05, .95rem→1.08, 15px→17px, .7em→.83em, .9em→1.03em
(See TODO_STATE.md part 2 for exact line numbers — too many to list here, use grep to find them all.)

### 3. Moon-phase axis visual (Section: Lunar Beginning, line 769-787)
Add CSS/SVG horizontal axis with moon icons (🌑→🌓→🌕) at Kalends/Nones/Ides positions.
Use Roman numerals on the axis. Explain:
- Kalends = new moon, from *calare* "to call out" (pontiffs announced it)
- Nones = first quarter, from *nonus* "ninth" (9 days before Ides inclusive)
- Ides = full moon, from Etruscan *iduare* "to divide" (midpoint)
- Did they track the moon? Initially yes (observation), but Numa's 355-day year was already off, and by late Republic they were conventional fossilised names.

### 4. Origin of every month name (table in Lunar Beginning or new panel)
- Ianuarius = Janus (doors/gates, two faces)
- Februarius = Februa (purification festival)
- Martius = Mars (war god, originally first month)
- Aprilis = *aperire* "to open" (buds) or Aphrodite
- Maius = Maia (growth) or *maiores* (elders)
- Iunius = Juno or *iuniores* (young)
- Quintilis→Iulius = "fifth", renamed 44 BC for Caesar
- Sextilis→Augustus = "sixth", renamed 8 BC for Augustus
- September/October/November/December = 7th/8th/9th/10th

### 5. March/May/July/October distinction (Section: Day Names, line 813-833)
These 4 months have Nones=7, Ides=15 (not 5/13).
Reason: they were the original 31-day "full" months in Romulus's 10-month calendar.
The extra 2 days pushed Nones from 5→7 and Ides from 13→15.
Other months were 29-day "hollow" (Nones=5, Ides=13).
January and February got the short pattern when Numa added them.
This distinction survived all reforms even after lunar connection was lost.
---

## IMPLEMENTATION APPROACH

Use a single Python script (via `run_commands` heredoc) to make ALL string replacements at once.

### Key insertion points:
- **Moon phase axis + month origins**: Insert into `ts-beginning` section (~line 774)
- **March/May/July/October explanation**: Insert into `ts-daynames` section (~line 821)
- **Festival calendar**: Insert into `ts-religion` section (~line 848)
- **Font sizes**: Global string replacements across CSS
- **Hacquard source**: Replace in footer (~line 975)

### Verification after changes:
1. `grep -c '<section' index.html` == `grep -c '</section>' index.html`
2. `grep -c '</html>' index.html` == 1
3. Node JS syntax check: extract `<script>` block and run `new Function()` on it
4. `open index.html` to view

---

## IMPORTANT NOTES FOR NEXT MODEL
- Read `index.html` ONCE (it's 1656 lines), then make ALL changes in a single Python script.
- DO NOT read the file repeatedly — that's what caused the previous model to get stuck.
- The user cares deeply about historical accuracy — all facts are from standard scholarship.
- Use Roman numerals in visual/axis representations (Hachette guide style).
- The user referenced images from "Guide Romain Antique" (Hachette 1952) showing axis representations with Roman numerals and moon phases — replicate that style with CSS/SVG.
- Font increases: bump ALL font-size values below .9rem by at least +0.125rem. Use `grep -n 'font-size' index.html` to find them all, then replace systematically.

### 6. Use Roman numerals in axis/table representations
- Moon-phase axis: Roman numerals for day positions
- Fasti February table: Roman numerals for day numbers
- Republican month grid: consider Roman numerals for day counts

### 7. Festival calendar with details (Section: Religion or Lunar Beginning)
Add monthly festival list with 2-3 sentence descriptions for the most important:
- Feb: Lupercalia(15), Parentalia(13-21), Terminalia(23), Regifugium(24)
- Mar: Matronalia(1), Quinquatrus(19-23)
- Apr: Cerealia(12-19), Parilia(21), Robigalia(25), Vinalia(23), Fordicidia(15)
- May: Lemuria(9,11,13)
- Jun: Vestalia(7-15), Matralia(11)
- Jul: Neptunalia(23)
- Aug: Vinalia Rustica(19), Consualia(21), Volcanalia(23)
- Sep: Ludi Romani(4-19)
- Oct: Armilustrium(19)
- Dec: Saturnalia(17-23), Opalia(19)
