# Quick Reference — Mini Calcio 3D

Guida rapida per sviluppatori e tester.

---

## 🎯 Obiettivo Progetto
Prototipo 3D rigori/tiri in porta — Arcade, veloce, divertente.

---

## 📂 Navigazione Repository

```
Dri.FSGame/
├── README.md              # Panoramica progetto
├── .gitignore             # File da ignorare in Git
│
├── Docs/
│   ├── SETUP.md           # 📘 Guida setup Visual Studio + UE
│   ├── ROADMAP.md         # 🗺️ Piano sviluppo (3 step)
│   ├── NOTES.md           # 📝 Idee, bug, priorità
│   ├── TESTCASES.md       # ✅ Test da eseguire ogni build
│   ├── BEST_PRACTICES.md  # 🌟 Standard di codice
│   └── QUICKREF.md        # ⚡ Questa guida
│
├── Content/Game/          # Asset Unreal (BP, UI, Maps, Data)
└── Source/FSGame/         # Codice C++ (Core, Gameplay, UI, Utils)
```

---

## 🚀 Comandi Rapidi

### Setup Iniziale
```bash
# Clone repo
git clone https://github.com/daviderimondi/Dri.FSGame.git
cd Dri.FSGame

# Crea feature branch
git checkout -b feature/nome-feature
```

### Workflow Sviluppo
```bash
# Update da main
git checkout main
git pull origin main

# Torna al tuo branch e merge main
git checkout feature/nome-feature
git merge main

# Lavora, poi committa
git add .
git commit -m "Descrizione modifiche"
git push origin feature/nome-feature
```

### Visual Studio
```bash
# Refresh progetto Unreal (se necessario)
# In Unreal: Tools → Refresh Visual Studio Project

# Build da command line (opzionale)
msbuild FSGame.sln /t:Build /p:Configuration="Development Editor" /p:Platform=Win64
```

---

## ⌨️ Shortcuts Essenziali

### Visual Studio
| Shortcut | Azione |
|----------|--------|
| `F5` | Start Debugging (avvia Unreal) |
| `Ctrl+Shift+B` | Build Solution |
| `F12` | Go to Definition |
| `Ctrl+K, Ctrl+D` | Format Document |
| `Ctrl+F` | Find in File |
| `Ctrl+Shift+F` | Find in Solution |

### Unreal Editor
| Shortcut | Azione |
|----------|--------|
| `Alt+P` | Play in Editor (PIE) |
| `Esc` | Stop PIE |
| `F7` | Compile C++ |
| `F11` | Fullscreen PIE |
| `Ctrl+S` | Save All |
| `~` | Open Console |

### In-Game (Target)
| Input | Azione |
|-------|--------|
| Mouse/Stick | Mira |
| Hold Button | Carica potenza |
| Release | Tiro |
| `R` | Reset rapido |
| `D` | Toggle debug overlay |

---

## 📋 Checklist Quotidiana

### Inizio Giornata
- [ ] `git pull origin main`
- [ ] Verifica build compila
- [ ] Apri livello principale in Unreal
- [ ] Test play rapido (< 1 min)

### Durante Sviluppo
- [ ] Compila spesso (ogni 30-60 min)
- [ ] Testa in PIE frequentemente
- [ ] Commit incrementali (small changes)
- [ ] Check `.gitignore` (no Binaries/Intermediate)

### Fine Giornata
- [ ] Build finale senza errori
- [ ] Test rapido gameplay
- [ ] `git add . && git commit -m "..."`
- [ ] `git push origin feature/...`

---

## 🧪 Test Essenziali (< 5 min)

### TC001 — Avvio
1. Apri Unreal Editor
2. Play in Editor (PIE)
3. ✅ No crash, no errori critici

### TC002 — Tiro Base
1. Punta verso porta
2. Tieni premuto, rilascia
3. ✅ Palla si muove correttamente

### TC003 — Goal
1. Tira in porta
2. ✅ Goal rilevato, punteggio aggiornato

### TC004 — Reset
1. Premi `R`
2. ✅ Palla torna in posizione, velocità = 0

---

## 🎮 Roadmap (3 Step)

### Step 1 — "Giocabile" (1 sera)
- Livello base (campo, porta, palla)
- Input (mira, carica, tiro, reset)
- Goal detection + UI punteggio

### Step 2 — "Divertente" (2-3 sere)
- Portiere base
- Audio (calcio, rete, palo)
- Serie 5 tiri + risultato

### Step 3 — "Gioco" (1 settimana)
- Difficoltà (3 livelli)
- Target bonus angoli
- Menu + Settings
- Save/Load

---

## 🛠️ Troubleshooting Veloce

### Problema: "Visual Studio non compila"
```bash
# Soluzione 1: Refresh project
# In Unreal: Tools → Refresh Visual Studio Project

# Soluzione 2: Rebuild
# In VS: Build → Rebuild Solution

# Soluzione 3: Clean
# Chiudi Unreal + VS
# Cancella Binaries/, Intermediate/, Saved/
# Rigenera project files (click dx su .uproject)
```

### Problema: "Unreal si blocca all'avvio"
```bash
# Cancella cache
rm -rf Binaries/ Intermediate/ Saved/

# Rigenera project
# Click dx .uproject → Generate Visual Studio project files

# Ricompila
# Apri .sln, Build Solution
```

### Problema: "IntelliSense lento"
```bash
# Cancella cache VS
rm -rf .vs/

# Riavvia Visual Studio
```

### Problema: "Git ha committato Binaries/"
```bash
# Rimuovi da Git (NON cancella file)
git rm -r --cached Binaries/
git rm -r --cached Intermediate/

# Verifica .gitignore
cat .gitignore | grep Binaries

# Committa rimozione
git commit -m "Remove binary files from Git"
```

---

## 💡 Tips & Tricks

### Performance
- ⚡ Evita Tick() quando possibile (usa eventi)
- ⚡ Usa Data Assets per tuning (no hardcode)
- ⚡ Early exit nelle funzioni

### Debug
- 🐛 `UE_LOG(LogTemp, Warning, TEXT("Value: %f"), value);`
- 🐛 `DrawDebugLine` / `DrawDebugSphere` per debug visivo
- 🐛 Toggle debug (`D` key) per overlay info

### Blueprint
- 🔵 Preferisci Event Dispatcher a Get/Cast
- 🔵 Usa `Pure` functions per getter
- 🔵 Categorizza variabili per editor pulito

### C++
- 🔴 `UPROPERTY(EditAnywhere)` per editor
- 🔴 `UFUNCTION(BlueprintCallable)` per BP
- 🔴 `const` e `const&` per parametri read-only

---

## 📖 Risorse Veloci

### Documentazione
- [Unreal C++ API](https://docs.unrealengine.com/5.0/en-US/API/)
- [Blueprint API](https://docs.unrealengine.com/5.0/en-US/BlueprintAPI/)
- [Gameplay Framework](https://docs.unrealengine.com/5.0/en-US/gameplay-framework-in-unreal-engine/)

### Community
- [Unreal Slackers Discord](https://unrealslackers.org/)
- [Unreal Forums](https://forums.unrealengine.com/)
- [/r/unrealengine](https://www.reddit.com/r/unrealengine/)

### Tutorial
- Tom Looman's C++ Tutorials
- Stephen Ulibarri's Blueprint → C++
- Official Unreal Learning Portal

---

## 🎯 Priorità Correnti

Vedi sempre `Docs/NOTES.md` per:
- ✨ Idee tester
- 🐛 Bug trovati
- 🚀 Top 3 priorità prossimo step

---

## 📝 Note Finali

**Regola d'oro**: _Meglio feature piccola finita che feature grande a metà._

- Committa spesso
- Testa sempre
- Chiedi aiuto se bloccato > 30 min
- Divertiti! ⚽🎮

---

**Ultimo aggiornamento**: 2026-03-02
