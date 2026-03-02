# Roadmap — Mini Calcio 3D

## Obiettivo
Creare un prototipo 3D di rigori/tiri in porta robusto, mantenibile e veloce da iterare.

---

## Step 1 — "Giocabile" (1 sera)
**Obiettivo**: Avere un loop di gioco base funzionante

### Deliverable
- [x] Setup progetto Unreal Engine
- [x] Setup Visual Studio Professional
- [x] Struttura cartelle (Content/Source)
- [x] .gitignore configurato
- [ ] Livello `Map_Main`:
  - Campo (plane con materiale base)
  - Porta (mesh + BoxTrigger per goal detection)
  - Palla (sphere con Physics enabled)
  - Camera fissa o semi-fissa
  - Player start
- [ ] Input base (Enhanced Input System):
  - Mira: mouse/stick
  - Carica potenza: hold/release
  - Tiro: release button
  - Reset rapido: tasto `R`
  - Debug toggle: tasto `D`
- [ ] Meccanica di tiro:
  - Calcolo direzione da camera/mira
  - Applicazione impulso alla palla
  - Reset palla dopo goal o fuori campo
- [ ] Goal detection:
  - `GoalTrigger` (BoxTrigger sulla porta)
  - Evento `OnGoalScored`
- [ ] UI base:
  - Punteggio (gol segnati)
  - Indicatore potenza tiro
- [ ] Sistema di reset:
  - Ferma fisica palla
  - Riposiziona palla
  - Reset camera
  - Reset UI

**Definition of Done**:
- Posso tirare la palla, segnare un goal, vedere il punteggio aggiornato e resettare con `R`
- Il tutto richiede < 30 secondi per essere testato

---

## Step 2 — "Divertente" (2–3 sere)
**Obiettivo**: Aggiungere feedback e challenge di base

### Deliverable
- [ ] Portiere base:
  - Mesh/skeletal mesh posizionato
  - AI semplice (movimento laterale verso palla)
  - Animazioni base (idle, dive, save)
  - Collision per parate
- [ ] Audio:
  - Suono calcio
  - Suono rete
  - Suono palo
  - Suono parata
  - Musica di sottofondo (opzionale)
- [ ] Effetti visivi:
  - Particelle su goal
  - Trail palla (opzionale)
  - Camera shake su tiro potente
- [ ] Serie di tiri:
  - GameMode gestisce serie di 5 tiri
  - Schermata risultato finale
  - Calcolo punteggio totale
- [ ] Feedback avanzato:
  - Slow motion su goal (0.3s)
  - Replay breve (2-3 secondi)
  - Vibrazione gamepad (se supportato)

**Definition of Done**:
- Il gioco è "divertente" anche solo per 5 tiri
- Audio/VFX rendono ogni azione soddisfacente
- Serie completa con schermata risultato

---

## Step 3 — "Gioco" (1 settimana a pezzetti)
**Obiettivo**: Aggiungere progressione e polish

### Deliverable
- [ ] Sistema difficoltà:
  - 3 livelli: Facile, Medio, Difficile
  - Portiere più veloce/reattivo ai livelli alti
  - Data Asset per parametri portiere
- [ ] Target bonus:
  - Visualizzazione angoli porta (target zones)
  - Punti extra per colpire gli angoli
  - Feedback visivo su target colpiti
- [ ] Progressione:
  - Unlock difficoltà successive
  - Statistiche salvate (high score, accuracy)
  - Save system (GameInstance + SaveGame)
- [ ] Menu sistema:
  - Main menu (Play, Options, Quit)
  - Pause menu
  - Settings:
    - Sensibilità mouse/stick
    - Volume audio
    - Difficoltà
- [ ] Polish:
  - Tutorial overlay (primo avvio)
  - Transizioni tra schermate
  - Cursor management
  - Input remapping (opzionale)
- [ ] Data-driven tuning:
  - `DA_KickTuning` (forza, curve, scatter)
  - `DA_GoalkeeperTuning` (velocità, reazione, range)
  - `DA_DifficultySettings`

**Definition of Done**:
- Gioco completo con menu, settings, progressione
- Tuning facilmente modificabile via Data Assets
- Esperienza "finita" anche se minimalista

---

## Backlog / Idee future
- Modalità allenamento (solo target, no portiere)
- Multiplayer locale (2 giocatori alternati)
- Skin palla/guanti sbloccabili
- Leaderboard locale
- Weather system (pioggia influenza physics)
- Power-ups temporanei
- Replay salvabili e condivisibili

---

## Note di iterazione
- Ogni sera: una feature piccola, committata, testata
- Prima grafica: validare meccanica con primitive
- Bug ambiguo: ridurre problema con test level minimo
- Raccogliere feedback tester dopo ogni step

---

**Ultimo aggiornamento**: 2026-03-02
