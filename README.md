# Dri.FSGame — Mini Calcio 3D (Unreal Engine)

![Unreal Engine](https://img.shields.io/badge/Unreal%20Engine-5.x-informational)
![Visual Studio](https://img.shields.io/badge/Visual%20Studio-2022-purple)
![C++](https://img.shields.io/badge/C%2B%2B-17-blue)

## 🎯 Obiettivo del Progetto

Prototipo 3D di **rigori e tiri in porta** per Unreal Engine, pensato come progetto "padre + tester" ma con standard da team professionale.

**Focus**: Arcade feel, loop veloce (1-3 min), progressione semplice.

---

## 🚀 Quick Start

### Prerequisiti
- **Unreal Engine 5.x** (Epic Games Launcher)
- **Visual Studio Professional 2022** con:
  - Desktop development with C++
  - Game development with C++
  - MSVC toolset v143+
  - Windows 10/11 SDK
- **Git** (per version control)

### Setup Iniziale

1. **Clone repository**:
   ```bash
   git clone https://github.com/daviderimondi/Dri.FSGame.git
   cd Dri.FSGame
   ```

2. **Configurare Visual Studio**:
   - Installare "Visual Studio Tools for Unreal Engine" dal Visual Studio Installer
   - In Unreal Editor: `Edit → Editor Preferences → Source Code → Visual Studio 2022`
   - Refresh project: `Tools → Refresh Visual Studio Project`

3. **Aprire progetto Unreal**:
   - Aprire file `.uproject` (quando creato)
   - Compilare progetto se richiesto

---

## 📁 Struttura Progetto

```
Dri.FSGame/
├── Content/                 # Asset Unreal Engine
│   └── Game/
│       ├── Blueprints/      # BP_* (actors, components)
│       ├── UI/              # WBP_* (widgets)
│       ├── Maps/            # Livelli di gioco
│       ├── Data/            # DA_* (Data Assets, tuning)
│       ├── Audio/           # Suoni ed effetti audio
│       ├── VFX/             # Effetti particellari
│       ├── Meshes/          # Modelli 3D
│       └── Materials/       # Materiali e texture
│
├── Source/                  # Codice C++
│   └── FSGame/
│       ├── Core/            # GameMode, GameInstance, manager
│       ├── Gameplay/        # Ball, Kick, Goalkeeper, Scoring
│       ├── UI/              # Widget logic C++
│       └── Utils/           # Helper, math utilities
│
├── Docs/                    # Documentazione progetto
│   ├── NOTES.md             # Idee, bug, priorità
│   ├── ROADMAP.md           # Piano sviluppo (3 step)
│   └── TESTCASES.md         # Test da eseguire ogni build
│
└── README.md                # Questo file
```

---

## 🎮 Gameplay — MVP

### Loop Base
1. **Mira** → carica potenza → tiro
2. **Esito**: goal / palo / parata / fuori
3. **Reset** automatico o manuale (`R`)
4. **Progressione**: serie di 5-10 tiri, difficoltà portiere crescente

### Controlli (Target)
- **Mira**: Mouse / Stick analogico
- **Carica potenza**: Hold / Release button
- **Tiro**: Release
- **Reset**: `R`
- **Debug overlay**: `D`

---

## 🛠️ Best Practice Adottate

### Architettura
- **Blueprint-first** per prototipazione rapida gameplay/UI
- **C++** per sistemi core, performance, utility riusabili
- **Data-driven**: tuning in Data Assets (no hardcode)
- **Event-driven**: Delegates/Dispatchers per comunicazione componenti

### Naming Conventions
- Classi: `PascalCase`
- Blueprint: `BP_`, `WBP_`, `DA_` prefixes
- Variabili: `camelCase`

### Git Workflow
- `main` sempre giocabile
- `feature/<nome>` per ogni nuova funzionalità
- Commit frequenti, build testata

### Definition of Done
Una feature è completa quando:
- ✅ Testabile in < 30 secondi nel livello principale
- ✅ Parametri in Data Asset (se tuning)
- ✅ Nessun Tick() inutile
- ✅ Log/debug overlay dove utile
- ✅ Build compila e non crasha

---

## 📚 Documentazione

Consulta la cartella `Docs/` per:
- **[NOTES.md](Docs/NOTES.md)**: Idee tester, bug, priorità
- **[ROADMAP.md](Docs/ROADMAP.md)**: Roadmap a 3 step (Giocabile → Divertente → Gioco)
- **[TESTCASES.md](Docs/TESTCASES.md)**: Test base da eseguire ogni build

---

## 🎯 Roadmap Sintetica

### Step 1 — "Giocabile" (1 sera)
Tiro + goal + reset + UI punteggio

### Step 2 — "Divertente" (2–3 sere)
Portiere + audio/VFX + serie 5 tiri + risultato finale

### Step 3 — "Gioco" (1 settimana)
Difficoltà + target bonus + menu + settings + replay

---

## 💡 Idee Future

- "Super tiro" ogni N goal
- Portiere AI avanzata
- Target bonus negli angoli
- Vento casuale
- Modalità arcade ("palo vale doppio")
- Skin/customization
- Replay condivisibili

---

## 📖 Riferimenti

- [Unreal Engine Documentation](https://docs.unrealengine.com/)
- [Visual Studio Tools for Unreal](https://learn.microsoft.com/en-us/visualstudio/gamedev/unreal/)
- [Blueprint Best Practices](https://docs.unrealengine.com/5.0/en-US/blueprint-best-practices-in-unreal-engine/)
- [C++ in Unreal](https://docs.unrealengine.com/5.0/en-US/programming-with-cplusplus-in-unreal-engine/)

---

## 👨‍👦 Team

- **Developer**: Padre (setup, sistemi, architettura)
- **Tester / Game Designer**: Figlio (idee, feedback, test play)

---

## 📝 Licenza

Progetto hobby personale — Tutti i diritti riservati.

---

**Buon divertimento!** ⚽🎮