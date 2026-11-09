# Hardware

> Deze map bevat alle hardware-gerelateerde bestanden voor het project

---

## 📂 Structuur

```
hardware/
├── README.md              # Dit bestand
├── schematics/           # KiCAD schema's
│   └── [project].kicad_sch
├── pcb/                  # KiCAD PCB ontwerp (indien van toepassing)
│   └── [project].kicad_pcb
└── datasheets/           # Componentdatasheets → Verplaats naar /docs/datasheets/
```

---

## 🧩 Componentenlijst

> **Update deze lijst met alle hardware componenten die jullie gebruiken**

| Component | Type/Model | Functie | Datasheet | Aantal |
|-----------|-----------|---------|-----------|--------|
| Microcontroller | PSoC 6 | Hoofdcontroller | [Link](/docs/datasheets/P5oK6.pdf) | 1 |
| Sensor | [Type] | [Functie] | [Link](/docs/datasheets/) | 1 |
| ... | ... | ... | ... | ... |

**Vul deze tabel in met:**
- Exacte type nummers
- Wat elke component doet
- Link naar datasheet (bewaar lokaal in `/docs/datasheets/`)
- Aantal dat je nodig hebt

---

## 🔌 Blokdiagram / Schema

**Schematisch overzicht:**

> **Voeg hier een afbeelding of diagram toe waarin de bedrading en verbindingen van de componenten worden weergegeven.**
>
> - Voor week 1-2: Een handmatige schets is OK
> - Later: Fritzing of KiCAD schematic export (PNG of PDF) 

---

## ⚡ Specificaties

### Voeding
- **Spanning:** [bijv. 5V DC via USB]
- **Stroomverbruik:** [bijv. max 500mA]
- **Voedingsbron:** [bijv. USB powerbank]

### Communicatie
- **Protocollen:** [bijv. UART, I²C, SPI]
- **Pinnen:** [lijst belangrijke pinnen]
- **Logica level:** [bijv. 3.3V]

---

## 🔧 PCB Ontwerp (optioneel)

**Alleen invullen als je een PCB ontwerpt**

- **KiCAD versie:** [bijv. 7.0]
- **Aantal lagen:** [bijv. 2-layer]
- **Afmetingen:** [bijv. 100x80mm]
- **Producent:** [bijv. JLCPCB]

---

## 📝 Aantekeningen

**Belangrijke opmerkingen:**
- ...
- ...

**Bekende problemen:**
- ...
- ...

---

## ✅ Checklist

- [ ] Componentenlijst volledig ingevuld
- [ ] Schema/blokdiagram toegevoegd
- [ ] Datasheets lokaal opgeslagen in `/docs/datasheets/`
- [ ] KiCAD project werkend
- [ ] Specificaties gedocumenteerd
