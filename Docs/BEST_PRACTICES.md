# Best Practices — Mini Calcio 3D

Raccolta di best practice per mantenere il progetto robusto, mantenibile e veloce da iterare.

---

## 1. Architettura & Design Patterns

### 1.1 Blueprint-First, C++ When Needed
✅ **Blueprint per**:
- Prototipazione rapida gameplay
- UI e layout widget
- Iterazione veloce su parametri
- Visual scripting logiche semplici

✅ **C++ per**:
- Sistemi core (physics helpers, managers)
- Performance critical code
- Utility riusabili (math, trajectory)
- API stabili chiamate da Blueprint

### 1.2 Data-Driven Architecture
**Principio**: Tuning e configurazione in Data Assets, mai hardcoded.

**Esempi**:
```cpp
// ❌ BAD - Hardcoded
const float KickPower = 1500.0f;

// ✅ GOOD - Data Asset
UCLASS()
class UKickTuningData : public UDataAsset
{
    GENERATED_BODY()
public:
    UPROPERTY(EditAnywhere, BlueprintReadOnly)
    float MinKickPower = 500.0f;
    
    UPROPERTY(EditAnywhere, BlueprintReadOnly)
    float MaxKickPower = 2000.0f;
    
    UPROPERTY(EditAnywhere, BlueprintReadOnly)
    UCurveFloat* PowerCurve;
};
```

**Benefici**:
- Tester modifica parametri senza ricompilare
- Versioning facile (salva preset)
- A/B testing rapido

### 1.3 Separation of Concerns
Ogni classe ha **una responsabilità chiara**:

| Classe | Responsabilità |
|--------|----------------|
| `GameMode` | Regole partita, start/end, scoring |
| `PlayerController` | Input handling, mira, UI feedback |
| `BallActor` | Fisica palla, stato, reset |
| `GoalTrigger` | Rilevamento goal, emette eventi |
| `Goalkeeper` | AI portiere, animazioni, parate |

**Regola d'oro**: Un oggetto "osserva" il mondo, ma non decide tutto.

### 1.4 Event-Driven Communication
✅ **Usa Delegates/Event Dispatchers**:
```cpp
// In GoalTrigger.h
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnGoalScoredSignature, int32, TeamID);

UCLASS()
class AGoalTrigger : public AActor
{
    GENERATED_BODY()
public:
    UPROPERTY(BlueprintAssignable)
    FOnGoalScoredSignature OnGoalScored;
};

// GameMode ascolta
void AMyGameMode::BeginPlay()
{
    GoalTrigger->OnGoalScored.AddDynamic(this, &AMyGameMode::HandleGoalScored);
}
```

❌ **Evita riferimenti diretti a catena**:
```cpp
// BAD
BallActor->GoalTrigger->GameMode->UpdateScore();
```

---

## 2. Performance & Optimization

### 2.1 Tick Management
**Regola**: Minimizza uso di `Tick()`.

✅ **Alternative preferite**:
- **Eventi**: Overlap, Hit, OnClicked
- **Timers**: `GetWorldTimerManager().SetTimer()`
- **Input Axis**: `SetupPlayerInputComponent()`

❌ **Evita Tick per**:
- Polling condizioni (usa eventi)
- Update UI (usa binding o eventi)
- Logica che può essere timer-based

✅ **Se Tick necessario**:
```cpp
void AMyActor::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);
    
    // Early exit se non necessario
    if (!bIsActive)
        return;
    
    // Logica minima
}

// Constructor
AMyActor::AMyActor()
{
    PrimaryActorTick.bCanEverTick = true;
    PrimaryActorTick.TickInterval = 0.1f; // Tick ogni 100ms invece che ogni frame
}
```

### 2.2 Memory Management
✅ **UObject pointers**:
```cpp
UPROPERTY()
AActor* MyActor; // GC managed

TWeakObjectPtr<AActor> WeakActor; // Non previene GC

TObjectPtr<UObject> ModernPointer; // UE5 recommended
```

❌ **Evita raw pointers per UObject**:
```cpp
// BAD
AActor* MyActor = new AActor(); // NEVER
delete MyActor; // NEVER
```

---

## 3. Code Style & Conventions

### 3.1 Naming Conventions

| Tipo | Convenzione | Esempio |
|------|-------------|---------|
| Classe C++ | `PascalCase` con prefix | `AKickBall`, `UKickComponent` |
| Variabili membro C++ | `camelCase` | `kickPower`, `maxSpeed` |
| Funzioni C++ | `PascalCase` | `ApplyKick()`, `GetBallVelocity()` |
| Blueprint Actor | `BP_PascalCase` | `BP_KickBall` |
| Blueprint Widget | `WBP_PascalCase` | `WBP_ScoreUI` |
| Data Asset | `DA_PascalCase` | `DA_KickTuning` |
| Material | `M_` o `MI_` | `M_Ball`, `MI_Ball_Red` |
| Texture | `T_PascalCase` | `T_Ball_Diffuse` |
| Static Mesh | `SM_PascalCase` | `SM_Goal` |

### 3.2 UPROPERTY Specifiers
```cpp
// Editabile solo in editor, visibile in BP
UPROPERTY(EditAnywhere, BlueprintReadOnly)
float KickPower;

// Solo lettura Blueprint, modificabile C++
UPROPERTY(BlueprintReadOnly)
bool bIsKicking;

// Esposto a Blueprint, modificabile ovunque
UPROPERTY(EditAnywhere, BlueprintReadWrite)
float MaxSpeed;

// Categorizzato per editor pulito
UPROPERTY(EditAnywhere, Category = "Kick Settings")
float Power;

// Con tooltip
UPROPERTY(EditAnywhere, meta = (ToolTip = "Maximum kick power in Newtons"))
float MaxPower;
```

### 3.3 UFUNCTION Specifiers
```cpp
// Chiamabile da Blueprint
UFUNCTION(BlueprintCallable)
void ApplyKick(FVector Direction, float Power);

// Pure function (no side effects, icona diversa in BP)
UFUNCTION(BlueprintPure)
float GetKickPower() const;

// Implementabile in Blueprint (virtual)
UFUNCTION(BlueprintNativeEvent)
void OnKickApplied();

// Override in C++ se necessario
void OnKickApplied_Implementation();

// Categorizzato
UFUNCTION(BlueprintCallable, Category = "Kick System")
void PerformKick();
```

### 3.4 Commenti
✅ **Commenta quando**:
- Algoritmo complesso (math, AI)
- Workaround per bug engine
- Codice non-ovvio necessario

❌ **Non commentare**:
- Codice auto-esplicativo
- Ripetere cosa fa il codice

```cpp
// ❌ BAD - commento inutile
// Set kick power to 1000
kickPower = 1000.0f;

// ✅ GOOD - spiega perché
// Cap power at 2000 to prevent ball from escaping physics bounds
kickPower = FMath::Min(kickPower, 2000.0f);
```

---

## 4. Unreal-Specific Best Practices

### 4.1 Blueprint-Friendly C++ API
Progetta API pensando a come saranno usate in Blueprint:

```cpp
// ✅ GOOD - API chiara per BP
UFUNCTION(BlueprintCallable)
void SetupKick(float Power, FVector Direction);

// ❌ BAD - troppo complesso per BP
void ProcessKickData(const FKickParams& Params, TArray<FVector>& OutTrajectory, 
                     EKickResult& Result);
```

### 4.2 Logging Strutturato
```cpp
// Definisci categorie log
DECLARE_LOG_CATEGORY_EXTERN(LogKick, Log, All);
DECLARE_LOG_CATEGORY_EXTERN(LogGoal, Log, All);

// In .cpp
DEFINE_LOG_CATEGORY(LogKick);

// Uso
UE_LOG(LogKick, Warning, TEXT("Invalid kick power: %f"), Power);
UE_LOG(LogGoal, Display, TEXT("Goal scored by team %d"), TeamID);
```

### 4.3 Config Files
Per settings persistenti:
```ini
; Config/DefaultGame.ini
[/Script/FSGame.KickGameMode]
DefaultDifficulty=Medium
MaxPlayers=1
```

```cpp
UCLASS(Config=Game)
class AKickGameMode : public AGameMode
{
    GENERATED_BODY()
public:
    UPROPERTY(Config)
    FString DefaultDifficulty;
};
```

---

## 5. Gameplay Best Practices

### 5.1 Feel Over Realism
**Principio**: Gioco arcade, non simulazione.

✅ **Priorità**:
1. Risposta immediata all'input
2. Feedback forte e chiaro
3. Divertimento > Fisica perfetta

**Implementazione**:
- Aim assist leggero (magnetismo verso porta)
- Errori controllati (scatter solo ad alta potenza)
- Slow motion su eventi spettacolari
- Audio exaggerato

### 5.2 Feedback Loop Veloce
**Target**: Loop tiro → esito → reset in < 10 secondi

```cpp
void AKickGameMode::OnGoalScored()
{
    // 1. Feedback immediato (0.1s)
    PlayGoalSound();
    ShowGoalVFX();
    
    // 2. Slow motion breve (0.3s)
    UGameplayStatics::SetGlobalTimeDilation(GetWorld(), 0.3f);
    GetWorldTimerManager().SetTimer(SlowMoTimer, [this]() {
        UGameplayStatics::SetGlobalTimeDilation(GetWorld(), 1.0f);
    }, 0.3f, false);
    
    // 3. Update score (immediate)
    CurrentScore++;
    UpdateScoreUI();
    
    // 4. Reset rapido (1s)
    GetWorldTimerManager().SetTimer(ResetTimer, this, 
        &AKickGameMode::ResetBall, 1.0f, false);
}
```

### 5.3 Progressive Disclosure
Non mostrare tutto subito:
- Step 1: Solo tiro base + goal
- Step 2: Aggiungi portiere
- Step 3: Aggiungi difficoltà e target

---

## 6. Debug & Testing

### 6.1 Debug Overlay
Aggiungi toggle debug (`D` key):

```cpp
void APlayerController::ToggleDebug()
{
    bShowDebug = !bShowDebug;
}

void AKickBall::Tick(float DeltaTime)
{
    if (PlayerController->bShowDebug)
    {
        // Visualizza traiettoria prevista
        DrawDebugLine(GetWorld(), StartPos, PredictedLandingPos, 
                     FColor::Green, false, -1.0f, 0, 2.0f);
        
        // Visualizza potenza
        DrawDebugSphere(GetWorld(), GetActorLocation(), 
                       Power * 10.0f, 12, FColor::Red);
    }
}
```

### 6.2 Cheat Commands
Per testing rapido:

```cpp
UFUNCTION(Exec)
void CheatSetPower(float NewPower)
{
    KickPower = NewPower;
}

// In console: CheatSetPower 2000
```

### 6.3 Unit Testing (Opzionale)
Per utility math:

```cpp
IMPLEMENT_SIMPLE_AUTOMATION_TEST(FKickMathTest, "FSGame.Utils.KickMath", 
                                 EAutomationTestFlags::ApplicationContextMask | 
                                 EAutomationTestFlags::ProductFilter)

bool FKickMathTest::RunTest(const FString& Parameters)
{
    FVector Result = UKickMath::ComputeKickImpulse(
        FVector::ForwardVector, 1000.0f, 0.0f);
    
    TestEqual("Impulse magnitude", Result.Size(), 1000.0f, 0.1f);
    return true;
}
```

---

## 7. Git & Version Control

### 7.1 Commit Atomici
**Regola**: Un commit = una cosa logica

✅ **GOOD**:
```
git commit -m "Add kick power calculation"
git commit -m "Add goalkeeper basic AI"
```

❌ **BAD**:
```
git commit -m "Various fixes and features"
```

### 7.2 Branch Strategy
```
main              # sempre giocabile, compilabile
  ↓
feature/goal-trigger    # una feature alla volta
feature/goalkeeper-ai
```

### 7.3 Pull Request Checklist
Prima di merge su main:
- [ ] Codice compila senza warning
- [ ] Livello principale si avvia
- [ ] Feature testata (vedi TESTCASES.md)
- [ ] Nessun Binaries/Intermediate committato
- [ ] Code review fatto (anche auto-review)

---

## 8. Definition of Done

Una feature è **Done** quando:

1. ✅ **Funzionale**: Testabile in < 30 sec nel livello principale
2. ✅ **Comprensibile**: Non richiede aprire 10 BP per capire cosa fa
3. ✅ **Tunabile**: Parametri in Data Asset (se applicabile)
4. ✅ **Performante**: No Tick() inutili o memory leak
5. ✅ **Debuggable**: Log o debug overlay per eventi chiave
6. ✅ **Committabile**: Compila, non crasha, branch pulito

---

## 9. Anti-Patterns da Evitare

### 9.1 Spaghetti References
❌ **BAD**:
```cpp
Ball->Trigger->GameMode->UI->Widget->UpdateScore();
```

✅ **GOOD**:
```cpp
// Event dispatcher
OnGoalScored.Broadcast(TeamID);

// GameMode ascolta
void AGameMode::HandleGoal(int32 Team)
{
    UpdateScore(Team);
}
```

### 9.2 Magic Numbers
❌ **BAD**:
```cpp
AddImpulse(Direction * 1500.0f);
```

✅ **GOOD**:
```cpp
// In Data Asset
UPROPERTY(EditAnywhere)
float KickImpulseMultiplier = 1500.0f;

// In codice
AddImpulse(Direction * TuningData->KickImpulseMultiplier);
```

### 9.3 Tick Hell
❌ **BAD**:
```cpp
void Tick(float DeltaTime)
{
    if (IsGoalScored())
        OnGoalScored();
}
```

✅ **GOOD**:
```cpp
void OnOverlapBegin(AActor* OtherActor)
{
    if (OtherActor->IsA<ABall>())
        OnGoalScored.Broadcast();
}
```

---

## 10. Resources & Learning

### Must-Read
- [Unreal Engine Coding Standard](https://docs.unrealengine.com/5.0/en-US/epic-cplusplus-coding-standard-for-unreal-engine/)
- [Blueprint Best Practices](https://docs.unrealengine.com/5.0/en-US/blueprint-best-practices-in-unreal-engine/)
- [Gameplay Framework](https://docs.unrealengine.com/5.0/en-US/gameplay-framework-in-unreal-engine/)

### Community Wisdom
- Tom Looman's Blog: [unrealist.org](https://www.unrealist.org/)
- Alex Forsythe: [YouTube Unreal C++](https://www.youtube.com/@AlexForsythe)
- Unreal Slackers Discord: Best practice discussions

---

**Ricorda**: Meglio codice semplice che funziona che codice perfetto che non finisci mai! 🚀
