# Note di Sviluppo — Mini Calcio 3D

## Idee da implementare

### Dal tester (figlio)
- [ ] "Super tiro" ogni 3 goal consecutivi
- [ ] Portiere che "bara" in modalità difficile (reazioni più veloci)
- [ ] Tiri a bersagli negli angoli (modalità allenamento)
- [ ] Vento casuale che influenza la traiettoria
- [ ] Modalità "palo vale doppio" (arcade mode)

### Migliorie tecniche
- [ ] Implementare aim assist leggero (opzionale tramite setting)
- [ ] Aggiungere scatter controllato quando potenza è alta
- [ ] Feedback audio per rete/palo/parata
- [ ] Slow motion su goal spettacolari
- [ ] Vibrazione gamepad su eventi importanti

## Bug trovati dal tester
- Nessun bug ancora (progetto in fase di setup)

## Priorità prossimo step
1. Completare setup ambiente Visual Studio + Unreal Engine
2. Creare livello base con porta, palla, camera
3. Implementare input e meccanica di tiro base

## Decisioni di design
- **Focus**: Arcade feel > Realismo
- **Loop**: 1-3 minuti per sessione
- **Progressione**: Difficoltà portiere incrementale + target bonus
- **Tuning**: Tutto in Data Assets per iterazione rapida

## Note tecniche
- Usare Blueprint per prototipazione rapida gameplay/UI
- Usare C++ per:
  - Sistemi core (kick/ball physics helpers)
  - Save/settings manager
  - Utility riusabili (math, trajectory prediction)
- Event Dispatchers per comunicazione tra componenti
- Evitare Tick() dove possibile (usare eventi, timer, input axis)

## Parametri da tuning (futuri Data Assets)
- Forza tiro (min/max)
- Curva potenza
- Precisione/scatter
- Velocità portiere
- Range reazione portiere
- Difficoltà per livello

## Riferimenti utili
- [Unreal Engine Documentation](https://docs.unrealengine.com/)
- [Visual Studio Tools for Unreal](https://learn.microsoft.com/en-us/visualstudio/gamedev/unreal/)
- [Blueprint Best Practices](https://docs.unrealengine.com/5.0/en-US/blueprint-best-practices-in-unreal-engine/)
