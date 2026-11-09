# TwinCAT 3 Git Configuration Checklist

> ⚠️ **BELANGRIJK**: Nadat je de `.gitignore` hebt toegepast, moeten er ook instellingen in TwinCAT XAE zelf worden aangepast om optimaal met Git te werken.

Deze checklist is gebaseerd op de officiële Beckhoff best practices voor Git integratie.  
Bron: [BA-Belgium/TwinCAT3-Git-TwinCAT-Settings](https://github.com/BA-Belgium/TwinCAT3-Git-TwinCAT-Settings)

---

## 📋 Verplichte TwinCAT XAE Instellingen

### 1. LineIDs configuratie

**Probleem**: TwinCAT slaat standaard LineIDs op in `.TcPOU` bestanden, wat zorgt voor onnodige Git wijzigingen.

**Oplossing**:
1. Open TwinCAT XAE (Visual Studio)
2. Ga naar: **Tools → Options → TwinCAT → PLC Environment → Write Options**
3. Configureer als volgt:

   **Voor TwinCAT 4024.x**:
   - ✅ **Enable:** "Separate LineIDs"
   - ❌ **Disable:** "Write Line Ids" (indien beschikbaar in jouw versie)

   **Voor TwinCAT 4026.x en hoger**:
   - ❌ **Disable:** "Write Line Ids" 
   - Dit zorgt ervoor dat LineIDs helemaal niet meer worden opgeslagen

**Resultaat**: 
- LineIDs worden opgeslagen in `LineIDs.dbg` (wordt door `.gitignore` uitgesloten)
- Of helemaal niet opgeslagen (TwinCAT 4026+)
- Code wijzigingen in Git bevatten geen LineID noise meer

---

### 2. Git Compare Tool configuratie

**Probleem**: Standard git diff werkt niet goed voor TwinCAT XML bestanden.

**Oplossing**:
1. Ga naar: **Tools → Options → TwinCAT → XAE Environment → Project Compare**
2. Selecteer: **TwinCAT Project Compare Tool**
3. Configureer Git client:

   Voor **Git** (Visual Studio Git integration):
   - De configuratie gebeurt automatisch als je Git selecteert als Source Control Client
   - Verifieer in: **Team → Manage Connections → Local Git Repositories**

**Resultaat**: 
- TwinCAT Project Compare Tool wordt gebruikt voor diffs
- Structured vergelijking van PLC code en configuraties

---

### 3. Project structuur instellingen

**Aanbeveling**: Maak gebruik van de volgende best practices:

#### Standalone PLC projecten
- **Voordeel**: PLC project is onafhankelijk te beheren in Git
- **Let op**: Bij gebruik van Events → TMC bestand MOET gecommit worden!
- Aanmaken: Rechtermuisknop op `SYSTEM` → `Add New Item` → `PLC Project (Standalone)`

#### Separate files voor componenten
- **NC Axes**: Sla op als separate file via InfoSys instructies
- **IO Devices**: Sla op als separate file via InfoSys instructies
- **Voordeel**: Betere merge capabilities, duidelijkere Git history

---

### 4. Library management

**Configuratie**:
- Standaard libraries: Komen van TwinCAT installatie (niet in Git)
- Custom/third-party libraries: 
  - Plaats in subfolder genaamd `Compiled Library`
  - Deze worden WEL gecommit (zie `.gitignore` exception rule)

**In project verwijzen naar libraries**:
- Gebruik: **Install Libraries from Project** functionaliteit
- Vermijd handmatige library referenties die niet reproduceerbaar zijn

---

## 🔍 Verificatie

### Check of instellingen correct zijn:

1. **LineIDs test**:
   - Open een `.TcPOU` bestand in text editor
   - Voeg commentaar toe aan code
   - Save project
   - Check of `.TcPOU` bestand niet vol staat met `<LineId Id="...">` tags

2. **GitIgnore test**:
   ```bash
   git status
   ```
   - Je zou GEEN `_Boot/`, `_CompileInfo/`, `*.tpy`, `LineIDs.dbg` moeten zien
   - Je ZOU wel source `.TcPOU`, `.TcPLC`, `.tsproj` bestanden moeten zien

3. **TMC file check**:
   - Standalone PLC project MET events? → TMC moet zichtbaar zijn in Git
   - Normale PLC project? → TMC moet ignored worden
   - Pas `.gitignore` aan indien nodig (zie comments in bestand)

---

## 📚 Meer informatie

- [BA-Belgium TwinCAT3 Git Settings - 4024.x](https://github.com/BA-Belgium/TwinCAT3-Git-TwinCAT-Settings/blob/main/Source/README_4024.md)
- [BA-Belgium TwinCAT3 Git Settings - 4026.x](https://github.com/BA-Belgium/TwinCAT3-Git-TwinCAT-Settings/blob/main/Source/README_4026.md)
- [Beckhoff InfoSys - Source Control](https://infosys.beckhoff.com/content/1033/tc3_sourcecontrol/index.html)
- [AllTwinCAT - .gitignore guide](https://alltwincat.com/2019/12/02/gitignore-for-twincat/)

---

## ✅ Quick Checklist

- [ ] LineIDs configuratie aangepast (separate of disabled)
- [ ] TwinCAT Project Compare Tool ingesteld
- [ ] `.gitignore` toegepast in project root
- [ ] Git cache gecleared: `git rm -r --cached . && git add .`
- [ ] Eerste commit gemaakt met nieuwe settings
- [ ] Verificatie tests uitgevoerd
- [ ] Team geïnformeerd over nieuwe Git workflow
