# Source/FSGame

Questa cartella contiene il codice sorgente C++ del progetto.

## Struttura

### Core/
Sistemi fondamentali del gioco:
- `GameMode`: Regole di gioco, gestione partita
- `GameInstance`: Persistenza cross-level, settings
- `PlayerController`: Gestione input giocatore
- Manager e subsystem

### Gameplay/
Logica gameplay specifica:
- `Ball`: Actor palla con fisica
- `Kick`: Sistema di calcio e traiettoria
- `Goalkeeper`: AI e comportamento portiere
- `GoalTrigger`: Rilevamento goal
- `Scoring`: Sistema punteggio

### UI/
Widget logic in C++ (se necessario):
- HUD components
- Menu systems
- Widget controllers

### Utils/
Utility e helper functions:
- Math helpers (trajectory, prediction)
- Extension methods
- Shared utilities

## Best Practices

- Preferisci `UPROPERTY()` per esposizione a Blueprint
- Usa `UFUNCTION()` per metodi chiamabili da BP
- Evita `new/delete` per UObject (usa NewObject/SpawnActor)
- Commenta solo codice non-ovvio
- Crea utility pure functions per calcoli riusabili

## Esempi

```cpp
// Utils/KickMath.h
class UKickMath
{
public:
    static FVector ComputeKickImpulse(FVector Direction, float Power, float Spin);
    static FVector PredictBallLandingPoint(FVector StartPos, FVector Velocity);
};
```

```cpp
// Gameplay/KickBall.h
UCLASS()
class AKickBall : public AActor
{
    GENERATED_BODY()
    
public:
    UFUNCTION(BlueprintCallable)
    void ApplyKick(FVector Direction, float Power);
    
private:
    UPROPERTY(VisibleAnywhere)
    UStaticMeshComponent* BallMesh;
};
```
