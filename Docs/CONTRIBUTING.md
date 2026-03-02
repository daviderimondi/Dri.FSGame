# Contributing Guide

Benvenuto! Questa guida spiega come contribuire al progetto Mini Calcio 3D.

---

## 🎯 Filosofia del Progetto

- **Semplicità**: Meglio codice semplice che funziona che codice perfetto incompiuto
- **Iterazione rapida**: Small commits, test frequenti, feedback loop veloce
- **Standard professionali**: Anche se hobby, seguiamo best practice da team
- **Divertimento**: È un gioco padre+figlio, non dimenticare il fun factor!

---

## 🚀 Getting Started

### 1. Setup Ambiente
Segui la guida completa in [Docs/SETUP.md](SETUP.md).

**In breve**:
- Visual Studio Professional 2022
- Unreal Engine 5.x
- Git configurato

### 2. Clone & Branch
```bash
git clone https://github.com/daviderimondi/Dri.FSGame.git
cd Dri.FSGame
git checkout -b feature/nome-tua-feature
```

### 3. Familiarizza con la Struttura
- Leggi [README.md](../README.md)
- Consulta [ROADMAP.md](ROADMAP.md)
- Vedi [BEST_PRACTICES.md](BEST_PRACTICES.md)

---

## 📝 Workflow Contribuzione

### Step 1: Scegli una Task
Controlla:
- [ROADMAP.md](ROADMAP.md) per feature pianificate
- [NOTES.md](NOTES.md) per idee e bug
- GitHub Issues (se presenti)

### Step 2: Crea Feature Branch
```bash
git checkout main
git pull origin main
git checkout -b feature/nome-feature
```

**Naming convention branch**:
- `feature/nome-feature` per nuove funzionalità
- `bugfix/nome-bug` per correzioni
- `docs/descrizione` per documentazione

### Step 3: Sviluppa
1. **Scrivi codice seguendo best practices** (vedi sotto)
2. **Testa frequentemente** in Play in Editor
3. **Committa incrementalmente** (non aspettare fine feature)

### Step 4: Test
Prima di considerare completa una feature:
- [ ] Esegui test in [TESTCASES.md](TESTCASES.md)
- [ ] Build compila senza warning
- [ ] Livello principale si avvia senza crash
- [ ] Feature funziona come previsto

### Step 5: Commit & Push
```bash
git add .
git commit -m "Descrizione chiara della modifica"
git push origin feature/nome-feature
```

### Step 6: Pull Request (se collaborativo)
Se stai contribuendo a un progetto collaborativo:
1. Apri PR su GitHub
2. Descrivi cosa hai fatto e perché
3. Link a issue/task se rilevante
4. Attendi review

### Step 7: Merge
Una volta approvato:
```bash
git checkout main
git merge feature/nome-feature
git push origin main
```

---

## 🎨 Coding Standards

### Naming Conventions

#### C++ Classes
```cpp
// Actor
class AKickBall : public AActor { };

// Component
class UKickComponent : public UActorComponent { };

// Object
class UKickTuningData : public UDataAsset { };
```

#### Variables & Functions
```cpp
// Variabili membro: camelCase
float kickPower;
bool bIsKicking;  // bool sempre prefisso 'b'

// Funzioni: PascalCase
void ApplyKick();
float GetKickPower() const;
```

#### Blueprint Assets
- **Actor**: `BP_KickBall`
- **Widget**: `WBP_ScoreUI`
- **Data Asset**: `DA_KickTuning`
- **Material**: `M_Ball` o `MI_Ball_Instance`

### Code Style

#### UPROPERTY Usage
```cpp
// Editabile in editor, visibile in Blueprint
UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Kick")
float MaxPower = 2000.0f;

// Solo Blueprint (no editor)
UPROPERTY(BlueprintReadOnly)
bool bIsActive;

// Configurazione (salvata in .ini)
UPROPERTY(Config)
FString DefaultDifficulty;
```

#### UFUNCTION Usage
```cpp
// Chiamabile da Blueprint
UFUNCTION(BlueprintCallable, Category = "Kick")
void PerformKick(FVector Direction, float Power);

// Pure function (no side effects)
UFUNCTION(BlueprintPure, Category = "Kick")
float CalculatePower() const;

// Implementabile in Blueprint
UFUNCTION(BlueprintNativeEvent)
void OnKickPerformed();
// Implementa come OnKickPerformed_Implementation()
```

#### Comments
```cpp
// ✅ GOOD - Spiega il "perché"
// Clamp power to prevent physics instability
Power = FMath::Clamp(Power, 0.0f, MaxPower);

// ❌ BAD - Ripete il codice
// Set power to 1000
Power = 1000.0f;

// ✅ GOOD - Header class documentation
/**
 * Manages kick mechanics and ball physics
 * Handles power calculation, direction, and trajectory prediction
 */
class AKickBall : public AActor { };
```

---

## 🧪 Testing Guidelines

### Test Ogni Build
Esegui almeno questi test (da [TESTCASES.md](TESTCASES.md)):
1. **TC001**: Avvio progetto senza crash
2. **TC002**: Tiro base funziona
3. **TC003**: Goal detection funziona
4. **TC004**: Reset funziona

### Debug Tools
Aggiungi debug overlay per nuove feature:
```cpp
void AMyActor::DrawDebugInfo()
{
    if (!bShowDebug) return;
    
    DrawDebugLine(GetWorld(), Start, End, FColor::Green);
    DrawDebugSphere(GetWorld(), Location, Radius, 12, FColor::Red);
}
```

### Logging
Usa log categorizzati:
```cpp
DEFINE_LOG_CATEGORY_STATIC(LogKick, Log, All);

UE_LOG(LogKick, Display, TEXT("Kick applied with power: %f"), Power);
UE_LOG(LogKick, Warning, TEXT("Power exceeded max: %f > %f"), Power, MaxPower);
UE_LOG(LogKick, Error, TEXT("Invalid kick direction"));
```

---

## 📦 Commit Guidelines

### Commit Message Format
```
<type>: <descrizione breve>

[corpo opzionale con dettagli]
```

**Types**:
- `feat`: Nuova feature
- `fix`: Bug fix
- `docs`: Documentazione
- `refactor`: Refactoring (no behavior change)
- `perf`: Performance improvement
- `test`: Aggiunta test
- `chore`: Maintenance (build, config)

**Esempi**:
```bash
git commit -m "feat: Add goalkeeper basic AI movement"
git commit -m "fix: Ball physics instability at high speeds"
git commit -m "docs: Update ROADMAP with Step 2 progress"
git commit -m "refactor: Extract kick calculation to utility class"
```

### Cosa Committare
✅ **DO**:
- Codice sorgente (`.h`, `.cpp`)
- Blueprint (`.uasset`) se in Content/
- Config files (`.ini`)
- Documentazione (`.md`)

❌ **DON'T**:
- `Binaries/`
- `Intermediate/`
- `Saved/`
- `DerivedDataCache/`
- `.vs/`
- `.sln` (generato)

Verifica `.gitignore` sia correttamente configurato.

---

## 🔄 Pull Request Checklist

Prima di aprire PR (se progetto collaborativo):
- [ ] Branch aggiornato con `main`
- [ ] Build compila senza errori/warning
- [ ] Test base passano (vedi TESTCASES.md)
- [ ] Codice segue naming conventions
- [ ] Nessun file Binaries/Intermediate committato
- [ ] Commit messages chiari
- [ ] Feature documentata (se necessario)

**Descrizione PR**:
```markdown
## Feature: [Nome Feature]

### Cosa fa
Breve descrizione della funzionalità

### Come testare
1. Apri Map_Main
2. Play in Editor
3. Premi X per fare Y
4. Verifica Z

### Checklist
- [x] Build compila
- [x] Test TC001-TC004 passano
- [x] Nessun crash in PIE
- [x] Parametri in Data Asset (se applicabile)
```

---

## 🎯 Definition of Done

Una feature è **completa** quando:

### Funzionalità
- [ ] Implementata come da spec/roadmap
- [ ] Testabile in < 30 secondi nel livello principale
- [ ] Funziona senza crash/errori critici

### Codice
- [ ] Segue naming conventions
- [ ] Nessun magic number (usa Data Asset)
- [ ] Log per eventi importanti
- [ ] No Tick() inutili
- [ ] Commenti dove necessario (non ovunque)

### Testing
- [ ] Test manuale eseguito
- [ ] Test case documentato (se rilevante)
- [ ] Edge case considerati

### Integrazione
- [ ] Build compila senza warning
- [ ] Non rompe funzionalità esistenti
- [ ] Committata su branch pulito
- [ ] .gitignore rispettato

---

## 🌟 Best Practices Reminder

### Architettura
- **Blueprint-first** per gameplay
- **C++** per sistemi core
- **Data Assets** per tuning
- **Event Dispatchers** per comunicazione

### Performance
- Minimizza `Tick()`
- Early exit in funzioni
- Cache riferimenti quando possibile
- Usa `const` e `const&` appropriatamente

### Debugging
- Log eventi importanti
- Debug overlay toggle (`D`)
- DrawDebug* per visualizzazione

### Git
- Commit atomici (una cosa alla volta)
- Main sempre giocabile
- Feature branch per ogni task

---

## 🆘 Aiuto e Supporto

### Documenti di Riferimento
- [SETUP.md](SETUP.md) — Setup ambiente
- [ROADMAP.md](ROADMAP.md) — Piano sviluppo
- [BEST_PRACTICES.md](BEST_PRACTICES.md) — Standard codice
- [QUICKREF.md](QUICKREF.md) — Quick reference
- [TESTCASES.md](TESTCASES.md) — Test da eseguire

### Troubleshooting
Vedi sezione Troubleshooting in:
- [SETUP.md](SETUP.md#troubleshooting-comuni)
- [QUICKREF.md](QUICKREF.md#troubleshooting-veloce)

### Community
- [Unreal Slackers Discord](https://unrealslackers.org/)
- [Unreal Forums](https://forums.unrealengine.com/)
- Stack Overflow (tag: `unreal-engine`)

---

## 📜 License & Credits

Progetto hobby personale — Tutti i diritti riservati.

**Team**:
- Developer: Padre (architettura, sistemi)
- Tester/Designer: Figlio (idee, feedback)

---

**Grazie per contribuire! ⚽🎮**
