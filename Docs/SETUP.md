# Guida Setup — Visual Studio + Unreal Engine

Guida completa per configurare l'ambiente di sviluppo per il progetto Mini Calcio 3D.

---

## 1. Prerequisiti

### 1.1 Software Richiesto
- **Windows 10/11** (64-bit)
- **Visual Studio Professional 2022** (o Community)
- **Unreal Engine 5.x** (Epic Games Launcher)
- **Git** per version control

### 1.2 Requisiti Hardware (Consigliati)
- CPU: Intel i7 / AMD Ryzen 7 o superiore
- RAM: 16 GB (minimo), 32 GB consigliato
- GPU: NVIDIA GTX 1060 / AMD RX 580 o superiore
- SSD con almeno 50 GB liberi

---

## 2. Installazione Visual Studio 2022

### 2.1 Download
Scarica da: https://visualstudio.microsoft.com/downloads/

### 2.2 Componenti da Installare
Apri **Visual Studio Installer** → Click **Modifica** (o **Install** per nuova installazione)

#### Workload Necessari:
✅ **Desktop development with C++**
✅ **Game development with C++**

#### Componenti Individuali Raccomandati:
Vai su tab "Individual components":
- ✅ MSVC v143 - VS 2022 C++ x64/x86 build tools
- ✅ Windows 10 SDK (10.0.19041.0 o più recente)
- ✅ Windows 11 SDK (se su Windows 11)
- ✅ C++ CMake tools for Windows
- ✅ C++ profiling tools
- ✅ IntelliCode

### 2.3 Plugin Opzionali Utili
Dopo installazione, da Visual Studio:
**Extensions → Manage Extensions**:
- Visual Assist (opzionale, a pagamento, ma molto utile per C++)
- ReSharper C++ (opzionale, a pagamento)
- VS Chromium (opzionale, per ricerca codice veloce)

---

## 3. Installazione Unreal Engine

### 3.1 Epic Games Launcher
1. Scarica e installa Epic Games Launcher: https://www.epicgames.com/store/download
2. Crea account Epic Games (se non presente)
3. Accedi al launcher

### 3.2 Installare Unreal Engine
1. Nel launcher: **Unreal Engine** → **Library** tab
2. Click sul **+** accanto a "Engine Versions"
3. Seleziona versione **5.3** o più recente (consigliato 5.3 per stabilità)
4. Click **Install**
5. Scegli percorso installazione (preferibilmente su SSD)
6. Attendi installazione (~40 GB)

### 3.3 Installare Visual Studio Tools for Unreal
1. Apri **Visual Studio Installer**
2. Click **Modifica** sulla tua installazione VS 2022
3. Vai su **Individual components**
4. Cerca "Unreal Engine"
5. Seleziona: ✅ **Visual Studio Tools for Unreal Engine**
6. Click **Modify** per installare

---

## 4. Configurazione Visual Studio per Unreal

### 4.1 Impostazioni Editor di Codice in Unreal
1. Apri Unreal Engine Editor
2. **Edit → Editor Preferences**
3. Cerca "Source Code"
4. In **Source Code Editor**, seleziona: **Visual Studio 2022**
5. Chiudi e riapri Unreal se necessario

### 4.2 Configurazione Visual Studio
Nel caso il progetto C++ non si apra correttamente:

1. In Unreal Editor, click destro sul file `.uproject`
2. Seleziona **Generate Visual Studio project files**
3. Apri il file `.sln` generato con Visual Studio

### 4.3 Impostazioni Visual Studio Raccomandate
In Visual Studio:

**Tools → Options → Text Editor → C/C++ → Formatting**:
- ✅ Automatically format on: paste
- ✅ Automatically format completed statement on ;

**Tools → Options → Text Editor → C/C++ → Advanced**:
- IntelliSense Engine: Default
- Disable Squiggles: False
- Max Cached Translation Units: 8 (o più se hai RAM)

---

## 5. Creazione Progetto Unreal

### 5.1 Nuovo Progetto C++
1. Apri Epic Games Launcher
2. **Unreal Engine → Library → Launch** (UE 5.3)
3. Nel Unreal Project Browser:
   - Template: **Blank** o **Third Person** (consigliato Blank per controllo totale)
   - Project Type: **C++** (non Blueprint!)
   - Platform: **Desktop**
   - Quality: **Maximum**
   - Starter Content: **No** (per progetto pulito)
   - Raytracing: No (a meno che GPU RTX)
4. Nome progetto: `FSGame`
5. Percorso: Scegli cartella questo repository
6. Click **Create**

### 5.2 Primo Avvio
- Unreal compilerà progetto (può richiedere 5-10 minuti)
- Visual Studio si aprirà automaticamente con il progetto
- Verifica che nel Solution Explorer vedi `FSGame` e `UE5`

---

## 6. Workflow Sviluppo

### 6.1 Editing Codice C++

**Metodo 1 - Da Unreal Editor**:
1. In Unreal: **Tools → New C++ Class**
2. Scegli classe parent (es. Actor, Component)
3. Nome classe (es. `KickBall`)
4. Unreal genera `.h` e `.cpp` e apre Visual Studio

**Metodo 2 - Da Visual Studio**:
1. Crea manualmente `.h` e `.cpp` in cartella appropriata
2. In Unreal: **Tools → Refresh Visual Studio Project**
3. Ricompila da Visual Studio o da Unreal

### 6.2 Compilazione

**Da Visual Studio**:
- **Build → Build Solution** (Ctrl+Shift+B)
- Configurazione: **Development Editor** per sviluppo
- Piattaforma: **Win64**

**Da Unreal Editor**:
- **Compile** button nella toolbar (icona ingranaggio)
- Hot Reload (se editor aperto): cambiamenti C++ ricompilati on-the-fly

### 6.3 Debug

**Avvio Debug**:
1. In Visual Studio: Assicurati configurazione = **Development Editor**
2. **Debug → Start Debugging** (F5)
3. Unreal Editor si avvierà in debug mode
4. Imposta breakpoint nel codice C++
5. Avvia Play in Editor (PIE)
6. Breakpoint si attiveranno quando codice viene eseguito

**Tips Debug**:
- Usa `UE_LOG` per logging custom
- `DrawDebugLine`, `DrawDebugSphere` per debug visivo
- Visual Studio "Watch" window per ispezionare variabili UE

---

## 7. Git Setup

### 7.1 .gitignore
Già configurato nel repository. Verifica che escluda:
- `Binaries/`
- `Intermediate/`
- `Saved/`
- `DerivedDataCache/`
- `.vs/`
- `*.sln`
- `*.suo`

### 7.2 Git Workflow
```bash
# Crea branch per feature
git checkout -b feature/nome-feature

# Lavora, testa, committa
git add .
git commit -m "Implement kick mechanics"

# Push branch
git push origin feature/nome-feature

# Merge su main quando completato e testato
```

### 7.3 Regola d'Oro
**Ogni commit su main deve**:
- Compilare senza errori
- Permettere di avviare livello principale senza crash
- Essere testato almeno una volta in PIE

---

## 8. Struttura Cartelle (Dopo Creazione Progetto)

```
Dri.FSGame/
├── .git/
├── .gitignore
├── README.md
├── Docs/
│   ├── NOTES.md
│   ├── ROADMAP.md
│   ├── TESTCASES.md
│   └── SETUP.md (questo file)
│
├── FSGame.uproject          # File progetto Unreal
├── FSGame.sln               # Solution Visual Studio (gitignored)
│
├── Content/
│   └── Game/
│       ├── Blueprints/
│       ├── UI/
│       ├── Maps/
│       ├── Data/
│       ├── Audio/
│       ├── VFX/
│       ├── Meshes/
│       └── Materials/
│
├── Source/
│   ├── FSGame/
│   │   ├── Core/
│   │   ├── Gameplay/
│   │   ├── UI/
│   │   └── Utils/
│   └── FSGame.Target.cs
│
├── Config/                   # Configurazione progetto Unreal
├── Binaries/                 # (gitignored)
├── Intermediate/             # (gitignored)
└── Saved/                    # (gitignored)
```

---

## 9. Troubleshooting Comuni

### Problema: "Visual Studio non trova Unreal Engine headers"
**Soluzione**:
1. Chiudi Visual Studio
2. In Unreal: **Tools → Refresh Visual Studio Project**
3. Riapri `.sln`

### Problema: "Hot Reload fallisce"
**Soluzione**:
- Chiudi Unreal Editor
- Compila da Visual Studio (Build Solution)
- Riapri Unreal Editor

### Problema: "Unreal si blocca all'avvio"
**Soluzione**:
1. Cancella cartelle: `Binaries/`, `Intermediate/`, `Saved/`
2. Click destro `.uproject` → **Generate Visual Studio project files**
3. Apri `.sln` → Build Solution
4. Riavvia Unreal

### Problema: "IntelliSense lento o non funzionante"
**Soluzione**:
- VS Options → Text Editor → C/C++ → Advanced
- Disable Database: True (poi False dopo riavvio)
- Delete `.vs/` folder, riavvia VS

---

## 10. Best Practices Workflow

### 10.1 Sviluppo Quotidiano
1. **Mattina**: Pull da Git, verifica build compila
2. **Sviluppo**: Piccoli incrementi, compila spesso
3. **Test**: Testa ogni 30-60 min in PIE
4. **Commit**: Fine giornata o dopo feature completa
5. **Sera**: Push su feature branch

### 10.2 Prima di Commitare
✅ Codice compila (Build Solution in VS)
✅ Livello principale si avvia senza crash
✅ Funzionalità testata almeno 1 volta
✅ Nessun warning critico
✅ `.gitignore` rispettato (no Binaries/Intermediate)

### 10.3 Code Review (Auto-Review)
Prima di merge su main:
1. Rileggi diff delle modifiche
2. Verifica naming convention
3. Rimuovi codice commentato inutile
4. Verifica che tuning sia in Data Assets (no hardcode)
5. Aggiungi log per eventi importanti

---

## 11. Shortcuts Utili

### Visual Studio
- `F5`: Start Debugging
- `Ctrl+Shift+B`: Build Solution
- `Ctrl+K, Ctrl+D`: Format Document
- `F12`: Go to Definition
- `Ctrl+F`: Find in File
- `Ctrl+Shift+F`: Find in Solution

### Unreal Editor
- `F7`: Compile C++ (se modifiche)
- `Alt+P`: Play in Editor (PIE)
- `Esc`: Stop PIE
- `F11`: Fullscreen PIE
- `Ctrl+S`: Save All

---

## 12. Risorse di Apprendimento

### Documentazione Ufficiale
- [Unreal C++ API Reference](https://docs.unrealengine.com/5.0/en-US/API/)
- [Unreal C++ Programming Guide](https://docs.unrealengine.com/5.0/en-US/programming-with-cplusplus-in-unreal-engine/)
- [Visual Studio Unreal Integration](https://learn.microsoft.com/en-us/visualstudio/gamedev/unreal/)

### Tutorial Consigliati
- Unreal Engine Official: C++ Fundamentals
- Tom Looman's C++ Survival Game Tutorial
- Stephen Ulibarri's Blueprint → C++ series

### Community
- [Unreal Slackers Discord](https://unrealslackers.org/)
- [Unreal Engine Forums](https://forums.unrealengine.com/)
- [r/unrealengine](https://www.reddit.com/r/unrealengine/)

---

## Prossimi Passi

Dopo aver completato il setup:
1. ✅ Verifica che tutto compili
2. ✅ Crea primo livello `Map_Main`
3. ✅ Aggiungi `BP_KickBall` (palla con fisica)
4. ✅ Testa PIE senza crash
5. 📖 Consulta [ROADMAP.md](ROADMAP.md) per Step 1

---

**Setup completato! Pronti per sviluppare! ⚽🎮**
