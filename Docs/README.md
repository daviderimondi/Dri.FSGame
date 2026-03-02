# Documentazione — Mini Calcio 3D

Benvenuto nella documentazione del progetto! Questa cartella contiene tutte le guide e i riferimenti necessari per sviluppare il gioco.

---

## 📑 Indice Documenti

### 🚀 Per Iniziare

#### [SETUP.md](SETUP.md)
**Guida completa setup ambiente di sviluppo**
- Installazione Visual Studio 2022
- Configurazione Unreal Engine 5.x
- Creazione progetto C++
- Workflow sviluppo e debug
- Troubleshooting comuni

**Leggi questo**: Se è la tua prima volta sul progetto o devi configurare un nuovo PC.

---

#### [QUICKREF.md](QUICKREF.md)
**Quick Reference — Guida rapida**
- Comandi rapidi Git e Visual Studio
- Shortcuts essenziali
- Checklist quotidiana
- Test rapidi (< 5 min)
- Troubleshooting veloce

**Leggi questo**: Come reference veloce durante lo sviluppo quotidiano.

---

### 📋 Pianificazione & Tracking

#### [ROADMAP.md](ROADMAP.md)
**Piano di sviluppo a 3 step**
- **Step 1 — "Giocabile"** (1 sera): Tiro + goal + reset + UI
- **Step 2 — "Divertente"** (2-3 sere): Portiere + audio + VFX + serie
- **Step 3 — "Gioco"** (1 settimana): Difficoltà + menu + save

**Leggi questo**: Per capire dove siamo e cosa fare dopo.

---

#### [NOTES.md](NOTES.md)
**Note di sviluppo — Living document**
- Idee dal tester (figlio)
- Bug trovati
- Priorità prossimo step
- Decisioni di design
- Parametri da tuning

**Leggi questo**: Prima di iniziare una sessione di sviluppo, per vedere le priorità.

---

#### [TESTCASES.md](TESTCASES.md)
**Test da eseguire ogni build**
- Test core (sempre): Avvio, Tiro, Goal, Reset, UI
- Test Step 2: Portiere, Audio, Serie
- Test Step 3: Difficoltà, Menu, Save
- Test regressione

**Leggi questo**: Prima di committare, per verificare che tutto funzioni.

---

### 🌟 Best Practices & Standards

#### [BEST_PRACTICES.md](BEST_PRACTICES.md)
**Standard di codice e architettura**
- Architettura (Blueprint vs C++, Data-driven, Event-driven)
- Performance (Tick management, Memory)
- Code style (Naming, UPROPERTY, UFUNCTION)
- Unreal best practices
- Gameplay best practices
- Debug & Testing
- Git workflow

**Leggi questo**: Quando scrivi codice, per seguire gli standard del progetto.

---

#### [CONTRIBUTING.md](CONTRIBUTING.md)
**Guida per contribuire**
- Workflow contribuzione (branch, develop, commit, PR)
- Coding standards dettagliati
- Testing guidelines
- Commit message format
- Pull Request checklist
- Definition of Done

**Leggi questo**: Prima di contribuire al progetto, per capire il processo.

---

## 🎯 Percorsi Consigliati

### 👋 Nuovo Sviluppatore
1. Leggi [../README.md](../README.md) per panoramica progetto
2. Segui [SETUP.md](SETUP.md) per setup ambiente
3. Consulta [ROADMAP.md](ROADMAP.md) per capire il piano
4. Leggi [BEST_PRACTICES.md](BEST_PRACTICES.md) per gli standard
5. Tieni [QUICKREF.md](QUICKREF.md) aperto durante lo sviluppo

### 🔧 Sviluppo Quotidiano
1. Controlla [NOTES.md](NOTES.md) per priorità del giorno
2. Sviluppa seguendo [BEST_PRACTICES.md](BEST_PRACTICES.md)
3. Usa [QUICKREF.md](QUICKREF.md) per comandi rapidi
4. Prima di commit, esegui [TESTCASES.md](TESTCASES.md)
5. Aggiorna [NOTES.md](NOTES.md) se necessario

### 🐛 Troubleshooting
1. [QUICKREF.md → Troubleshooting Veloce](QUICKREF.md#troubleshooting-veloce)
2. [SETUP.md → Troubleshooting Comuni](SETUP.md#troubleshooting-comuni)
3. Community Unreal (Discord, Forums)

### 🎮 Tester / Game Designer
1. Leggi [../README.md](../README.md) per capire il gioco
2. Consulta [ROADMAP.md](ROADMAP.md) per vedere cosa aspettarsi
3. Esegui [TESTCASES.md](TESTCASES.md) dopo ogni build
4. Aggiungi idee e bug in [NOTES.md](NOTES.md)

---

## 📊 Struttura Documentazione

```
Docs/
├── README.md              # ⬅️ Questo file (indice)
│
├── SETUP.md               # Setup completo ambiente
├── QUICKREF.md            # Quick reference guide
│
├── ROADMAP.md             # Piano sviluppo 3 step
├── NOTES.md               # Idee, bug, priorità
├── TESTCASES.md           # Test ogni build
│
├── BEST_PRACTICES.md      # Best practices dettagliate
└── CONTRIBUTING.md        # Guida contribuzione
```

---

## 🔄 Aggiornamenti Documenti

### Chi Aggiorna Cosa

| Documento | Chi | Quando |
|-----------|-----|--------|
| SETUP.md | Developer | Setup cambia, nuovi tool |
| ROADMAP.md | Developer | Fine step, revisione piano |
| NOTES.md | Developer + Tester | Continuo (idee, bug) |
| TESTCASES.md | Developer | Nuova feature richiede test |
| BEST_PRACTICES.md | Developer | Nuovi pattern emersi |
| QUICKREF.md | Developer | Nuovi shortcut/workflow |
| CONTRIBUTING.md | Developer | Processo cambia |

### Frequency
- **Continuo**: NOTES.md
- **Per feature**: TESTCASES.md, BEST_PRACTICES.md
- **Per step**: ROADMAP.md
- **Raro**: SETUP.md, QUICKREF.md, CONTRIBUTING.md

---

## 💡 Tips per la Documentazione

### Mantenere Docs Aggiornati
- ✅ Aggiorna NOTES.md ogni sessione di sviluppo
- ✅ Aggiungi test in TESTCASES.md quando crei feature
- ✅ Aggiorna ROADMAP.md quando completi uno step
- ✅ Scrivi best practice quando scopri pattern utili

### Scrivere Docs Efficaci
- 📝 Brevi e concisi (no wall of text)
- 📝 Esempi concreti
- 📝 Formatting chiaro (headers, lists, code blocks)
- 📝 Link incrociati tra documenti

### Non Duplicare
- Se info già esiste in doc A, link a doc A da doc B
- QUICKREF è "quick", BEST_PRACTICES è "deep"
- README è overview, SETUP è dettaglio

---

## 📖 Risorse Esterne

### Unreal Engine
- [Official Documentation](https://docs.unrealengine.com/)
- [C++ API Reference](https://docs.unrealengine.com/5.0/en-US/API/)
- [Blueprint API](https://docs.unrealengine.com/5.0/en-US/BlueprintAPI/)
- [Learning Portal](https://www.unrealengine.com/learn)

### Visual Studio
- [VS + Unreal Integration](https://learn.microsoft.com/en-us/visualstudio/gamedev/unreal/)
- [C++ in Visual Studio](https://learn.microsoft.com/en-us/cpp/)

### Community
- [Unreal Slackers Discord](https://unrealslackers.org/)
- [Unreal Forums](https://forums.unrealengine.com/)
- [r/unrealengine](https://www.reddit.com/r/unrealengine/)

---

## ❓ FAQ

### Q: Quale documento leggo prima?
**A**: Se nuovo → SETUP.md. Se sviluppi quotidianamente → QUICKREF.md.

### Q: Dove trovo le priorità di oggi?
**A**: NOTES.md → sezione "Priorità prossimo step"

### Q: Come so se una feature è "finita"?
**A**: Segui "Definition of Done" in CONTRIBUTING.md

### Q: Dove aggiungo idee nuove?
**A**: NOTES.md → sezione "Idee da implementare"

### Q: Come configuro Visual Studio?
**A**: SETUP.md → sezione 2-4

### Q: Quali test eseguire prima di commit?
**A**: TESTCASES.md → "Test Core (sempre)"

---

**Buon sviluppo! ⚽🎮**
