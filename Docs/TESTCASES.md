# Test Cases — Mini Calcio 3D

## Scopo
Questa lista contiene i test base da eseguire **ad ogni build** per verificare che il gioco sia funzionante.
Ogni test dovrebbe richiedere < 1 minuto.

---

## Test Core (sempre)

### TC001 — Avvio e Setup Base
**Obiettivo**: Verificare che il progetto si avvii senza crash
- [ ] Aprire progetto in Unreal Engine
- [ ] Compilare C++ (se modificato)
- [ ] Avviare Play in Editor (PIE)
- [ ] Verificare assenza crash/errori critici nel log

**Risultato atteso**: Livello si carica, nessun errore critico

---

### TC002 — Tiro Base
**Obiettivo**: Verificare meccanica di tiro
- [ ] Avviare play
- [ ] Puntare verso la porta
- [ ] Tenere premuto per caricare potenza
- [ ] Rilasciare per tirare
- [ ] Verificare che palla si muova nella direzione corretta

**Risultato atteso**: 
- Palla viene calciata
- Direzione coerente con mira
- Potenza influenza velocità

---

### TC003 — Goal Detection
**Obiettivo**: Verificare rilevamento goal
- [ ] Tirare palla in porta
- [ ] Verificare che goal venga rilevato
- [ ] Verificare che punteggio venga aggiornato
- [ ] Verificare feedback (audio/visual se implementato)

**Risultato atteso**:
- Goal rilevato quando palla attraversa trigger
- Punteggio incrementato correttamente
- Feedback appropriato visualizzato

---

### TC004 — Reset
**Obiettivo**: Verificare sistema di reset
- [ ] Premere tasto `R`
- [ ] Verificare che palla torni in posizione iniziale
- [ ] Verificare che fisica palla sia ferma
- [ ] Verificare che camera sia ripristinata

**Risultato atteso**:
- Palla in posizione di partenza
- Velocità palla = 0
- Stato gioco pronto per nuovo tiro

---

### TC005 — UI Base
**Obiettivo**: Verificare elementi UI
- [ ] Verificare visualizzazione punteggio
- [ ] Verificare indicatore potenza (se implementato)
- [ ] Verificare UI risponde a eventi di gioco

**Risultato atteso**:
- Punteggio visibile e aggiornato
- Indicatore potenza funzionante
- UI leggibile e posizionata correttamente

---

## Test Step 2 (quando implementato)

### TC006 — Portiere Base
**Obiettivo**: Verificare comportamento portiere
- [ ] Tirare verso sinistra/destra
- [ ] Verificare movimento portiere
- [ ] Verificare animazioni (se implementate)
- [ ] Verificare collision/parate

**Risultato atteso**:
- Portiere si muove verso palla
- Animazioni fluide
- Parate funzionanti

---

### TC007 — Audio
**Obiettivo**: Verificare feedback audio
- [ ] Verificare suono calcio palla
- [ ] Segnare goal → verificare suono rete
- [ ] Colpire palo → verificare suono palo
- [ ] Parata portiere → verificare suono parata

**Risultato atteso**:
- Tutti i suoni riproducono correttamente
- Volume appropriato
- Nessun taglio/glitch audio

---

### TC008 — Serie di Tiri
**Obiettivo**: Verificare gestione serie completa
- [ ] Completare 5 tiri
- [ ] Verificare contatore tiri rimanenti
- [ ] Verificare schermata risultato finale
- [ ] Verificare possibilità di ricominciare

**Risultato atteso**:
- Serie completa senza crash
- Risultato finale corretto
- Possibile iniziare nuova serie

---

## Test Step 3 (quando implementato)

### TC009 — Difficoltà
**Obiettivo**: Verificare livelli difficoltà
- [ ] Testare difficoltà Facile
- [ ] Testare difficoltà Medio
- [ ] Testare difficoltà Difficile
- [ ] Verificare differenza comportamento portiere

**Risultato atteso**:
- Differenza percepibile tra livelli
- Parametri caricati da Data Asset
- Nessun crash al cambio difficoltà

---

### TC010 — Menu e Settings
**Obiettivo**: Verificare sistema menu
- [ ] Aprire menu principale
- [ ] Navigare in Options
- [ ] Modificare settings (audio, sensibilità)
- [ ] Avviare partita da menu
- [ ] Pausa durante partita

**Risultato atteso**:
- Menu navigabile
- Settings salvati correttamente
- Pause/resume funzionanti

---

### TC011 — Save/Load
**Obiettivo**: Verificare persistenza dati
- [ ] Completare partita con punteggio
- [ ] Chiudere gioco
- [ ] Riaprire gioco
- [ ] Verificare statistiche/high score salvati

**Risultato atteso**:
- Dati persistono tra sessioni
- High score corretto
- Settings mantenuti

---

## Test Regressione (prima release)

### TC012 — Stress Test
- [ ] 20 tiri consecutivi senza reset manuale
- [ ] Verificare assenza memory leak
- [ ] Verificare performance stabili

### TC013 — Input Edge Cases
- [ ] Tirare senza caricare potenza
- [ ] Caricare potenza al massimo
- [ ] Input rapidi consecutivi
- [ ] Cambio input durante carica

### TC014 — Physics Edge Cases
- [ ] Palla fuori campo
- [ ] Palla ferma nel trigger goal
- [ ] Doppia collision (palo + portiere)
- [ ] Tiro verticale (fuori porta)

---

## Note
- ✅ = Test passed
- ❌ = Test failed
- ⚠️ = Test passed con warning/anomalie
- 🔧 = Test non applicabile (feature non implementata)

**Regola**: Se un test fallisce, **non committare** fino a risoluzione.
