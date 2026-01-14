# Memory Bank - HelpMe!

## Indice
1. [Visione del Sistema](#visione-del-sistema)
2. [Ruoli Utente](#ruoli-utente)
3. [Concetti Chiave](#concetti-chiave)
4. [Regole di Business](#regole-di-business)
5. [Flussi Principali](#flussi-principali)
6. [Sistema di Categorie](#sistema-di-categorie)
7. [Sistema di Notifiche](#sistema-di-notifiche)
8. [Sistema di Votazione](#sistema-di-votazione)

---

## Visione del Sistema

### Obiettivo
HelpMe! è una piattaforma web sociale progettata per facilitare l'aiuto reciproco tra utenti attraverso la condivisione di problemi e la collaborazione nella ricerca di soluzioni.

### Proposta di Valore
- **Per chi cerca aiuto**: Possibilità di pubblicare problemi e ricevere supporto dalla community
- **Per chi offre aiuto**: Opportunità di condividere conoscenze e costruire reputazione
- **Per la community**: Creazione di una base di conoscenza collaborativa e accessibile

### Principi Fondamentali
1. **Accessibilità**: Consultazione libera per tutti, partecipazione per utenti registrati
2. **Qualità**: Sistema di votazione per evidenziare le migliori risposte
3. **Organizzazione**: Categorizzazione per facilitare la ricerca e l'expertise
4. **Trasparenza**: Tracciamento dello stato dei problemi (aperti/chiusi)
5. **Comunità**: Incentivazione della collaborazione e del supporto reciproco

---

## Ruoli Utente

### 1. Utente Non Registrato (Visitatore)
**Permessi:**
- Visualizzare problemi pubblicati
- Visualizzare commenti e soluzioni
- Cercare problemi per categoria
- Consultare profili pubblici degli utenti

**Limitazioni:**
- Non può pubblicare problemi
- Non può commentare
- Non può votare
- Non può ricevere notifiche

### 2. Utente Registrato
**Permessi:**
- Tutti i permessi dell'utente non registrato, più:
- Pubblicare problemi con titolo, descrizione, categorie e media
- Commentare problemi altrui
- Votare commenti (positivo/negativo)
- Chiudere i propri problemi indicando la soluzione
- Modificare/eliminare i propri contenuti
- Iscriversi a categorie per ricevere notifiche
- Costruire reputazione attraverso contributi utili

**Responsabilità:**
- Pubblicare contenuti pertinenti e rispettosi
- Selezionare categorie appropriate
- Indicare chiaramente quando un problema è risolto
- Partecipare in modo costruttivo

### 3. Amministratore
**Permessi:**
- Tutti i permessi dell'utente registrato, più:
- Moderare contenuti (eliminare/modificare problemi e commenti inappropriati)
- Gestire categorie (creare, modificare, eliminare)
- Gestire utenti (sospendere, bannare, assegnare ruoli)
- Identificare e assegnare badge "Esperto" per categoria
- Visualizzare statistiche e analytics della piattaforma
- Configurare regole di moderazione

**Responsabilità:**
- Mantenere un ambiente sicuro e rispettoso
- Gestire dispute e segnalazioni
- Garantire la qualità dei contenuti
- Curare il sistema di categorie

---

## Concetti Chiave

### Problema (Post)
Rappresenta una richiesta di aiuto pubblicata da un utente.

**Attributi:**
- **ID**: Identificatore univoco
- **Titolo**: Stringa breve e descrittiva (max 200 caratteri)
- **Descrizione**: Testo dettagliato del problema (supporta formattazione)
- **Autore**: Riferimento all'utente che ha creato il problema
- **Data Creazione**: Timestamp di pubblicazione
- **Data Ultima Modifica**: Timestamp dell'ultimo aggiornamento
- **Categorie**: Lista di categorie associate (1-5 categorie)
- **Media**: Lista di allegati (immagini, video, documenti)
- **Stato**: Aperto/Chiuso
- **Soluzione**: Riferimento al commento marcato come soluzione (se chiuso)
- **Visualizzazioni**: Contatore di visualizzazioni
- **Commenti**: Lista di commenti associati

**Stati:**
- **Aperto**: Problema attivo in cerca di soluzione
- **Chiuso**: Problema risolto con soluzione identificata

### Commento (Risposta)
Rappresenta una risposta o contributo a un problema.

**Attributi:**
- **ID**: Identificatore univoco
- **Contenuto**: Testo della risposta (supporta formattazione)
- **Autore**: Riferimento all'utente che ha scritto il commento
- **Problema**: Riferimento al problema associato
- **Data Creazione**: Timestamp di pubblicazione
- **Data Ultima Modifica**: Timestamp dell'ultimo aggiornamento
- **Voti Positivi**: Contatore di voti favorevoli
- **Voti Negativi**: Contatore di voti contrari
- **Punteggio Netto**: Differenza tra voti positivi e negativi
- **È Soluzione**: Flag che indica se è la soluzione accettata
- **Media**: Lista di allegati (opzionale)

**Caratteristiche:**
- Ordinabili per data o per punteggio
- Modificabili dall'autore entro limiti temporali
- Cancellabili dall'autore o da amministratori

### Categoria
Rappresenta un'area tematica per organizzare i problemi.

**Attributi:**
- **ID**: Identificatore univoco
- **Nome**: Denominazione della categoria
- **Descrizione**: Spiegazione dell'ambito tematico
- **Icona/Colore**: Identificativi visuali
- **Categoria Padre**: Riferimento per struttura gerarchica (opzionale)
- **Sottocategorie**: Lista di categorie figlie
- **Esperti**: Lista di utenti riconosciuti come esperti
- **Numero Iscritti**: Contatore di utenti che seguono la categoria
- **Numero Problemi**: Contatore di problemi nella categoria

**Funzioni:**
- Organizzazione gerarchica (categoria > sottocategoria)
- Sistema di iscrizione per notifiche
- Identificazione di esperti

### Utente
Rappresenta un account sulla piattaforma.

**Attributi:**
- **ID**: Identificatore univoco
- **Username**: Nome utente univoco
- **Email**: Indirizzo email (privato)
- **Nome Completo**: Nome e cognome (opzionale)
- **Bio**: Descrizione personale
- **Avatar**: Immagine profilo
- **Data Registrazione**: Timestamp di iscrizione
- **Ruolo**: Non Registrato/Registrato/Amministratore
- **Categorie Seguite**: Lista di categorie a cui è iscritto
- **Badge Esperto**: Lista di categorie in cui è riconosciuto esperto
- **Statistiche**: 
  - Problemi pubblicati
  - Commenti scritti
  - Soluzioni accettate
  - Punteggio reputazione

### Notifica
Rappresenta un avviso inviato a un utente.

**Attributi:**
- **ID**: Identificatore univoco
- **Destinatario**: Riferimento all'utente
- **Tipo**: Categoria di notifica
- **Contenuto**: Messaggio della notifica
- **Riferimento**: Link al contenuto correlato
- **Data Creazione**: Timestamp di generazione
- **Letta**: Flag di lettura
- **Data Lettura**: Timestamp di visualizzazione

**Tipi di Notifica:**
- Nuovo problema in categoria seguita
- Nuovo commento su problema proprio
- Commento votato positivamente
- Soluzione accettata
- Menzione in commento
- Badge esperto assegnato

### Voto
Rappresenta una valutazione di un commento.

**Attributi:**
- **Utente**: Riferimento all'utente votante
- **Commento**: Riferimento al commento votato
- **Tipo**: Positivo/Negativo
- **Data**: Timestamp del voto

**Regole:**
- Un utente può votare un commento una sola volta
- L'utente può cambiare il proprio voto
- L'autore non può votare i propri commenti

---

## Regole di Business

### Pubblicazione Problemi
1. Solo utenti registrati possono pubblicare problemi
2. Ogni problema deve avere almeno:
   - Titolo (min 10, max 200 caratteri)
   - Descrizione (min 50 caratteri)
   - Almeno una categoria
3. Massimo 5 categorie per problema
4. Massimo 10 file media per problema
5. Dimensione massima per file: 10MB
6. Formati media supportati: immagini (JPG, PNG, GIF), video (MP4), documenti (PDF)

### Gestione Commenti
1. Solo utenti registrati possono commentare
2. Lunghezza minima commento: 20 caratteri
3. Massimo 5 file media per commento
4. I commenti possono essere modificati entro 15 minuti dalla pubblicazione
5. Le modifiche successive richiedono notazione "modificato"
6. Impossibile eliminare commenti marcati come soluzione

### Chiusura Problemi
1. Solo l'autore del problema può chiuderlo
2. La chiusura richiede la selezione di un commento come soluzione
3. Un problema chiuso può essere riaperto dall'autore se necessario
4. Alla chiusura, viene inviata notifica all'autore della soluzione
5. Problemi chiusi non possono ricevere nuovi commenti (salvo riapertura)

### Sistema di Votazione
1. Solo utenti registrati possono votare
2. Un utente può votare ogni commento una sola volta
3. È possibile cambiare il proprio voto (da positivo a negativo o viceversa)
4. È possibile rimuovere il proprio voto
5. Non è possibile votare i propri commenti
6. Non è possibile votare su problemi chiusi da più di 30 giorni

### Categorie e Expertise
1. Gli amministratori gestiscono la struttura delle categorie
2. Gli utenti possono seguire illimitate categorie
3. Il badge "Esperto" è assegnato da amministratori basandosi su:
   - Numero di soluzioni accettate nella categoria
   - Punteggio medio dei commenti nella categoria
   - Attività nella categoria
4. Un utente può essere esperto in multiple categorie
5. Il badge esperto può essere revocato da amministratori

### Sistema di Notifiche
1. Le notifiche sono abilitate per default per utenti registrati
2. Gli utenti possono configurare preferenze per tipo di notifica
3. Le notifiche vengono aggregate se multiple dello stesso tipo
4. Le notifiche più vecchie di 30 giorni vengono archiviate
5. Notifiche per nuovi problemi solo per categorie seguite

### Moderazione
1. Gli amministratori possono rimuovere contenuti inappropriati
2. Contenuti rimossi sono sostituiti con "[Contenuto rimosso per violazione policy]"
3. Utenti con 3 violazioni ricevono sospensione temporanea
4. Utenti con 5 violazioni possono essere bannati permanentemente
5. Gli utenti possono segnalare contenuti inappropriati
6. Le segnalazioni vengono riviste da amministratori

### Reputazione
1. La reputazione si basa su:
   - +10 punti per soluzione accettata
   - +2 punti per voto positivo ricevuto su commento
   - -1 punto per voto negativo ricevuto su commento
   - +5 punti per problema che riceve >10 visualizzazioni
2. La reputazione non può scendere sotto 0
3. Badge speciali assegnati a livelli di reputazione:
   - 100 punti: Contributore
   - 500 punti: Collaboratore Attivo
   - 1000 punti: Membro Esperto
   - 5000 punti: Guru della Community

---

## Flussi Principali

### Flusso 1: Pubblicazione di un Problema

**Attori:** Utente Registrato

**Precondizioni:**
- L'utente è autenticato nel sistema

**Flusso Principale:**
1. L'utente accede alla sezione "Nuovo Problema"
2. Il sistema presenta il form di creazione
3. L'utente inserisce:
   - Titolo del problema
   - Descrizione dettagliata
   - Seleziona 1-5 categorie
   - (Opzionale) Carica file media
4. L'utente conferma la pubblicazione
5. Il sistema valida i dati inseriti
6. Il sistema crea il problema con stato "Aperto"
7. Il sistema invia notifiche agli utenti iscritti alle categorie selezionate
8. Il sistema mostra conferma e reindirizza alla pagina del problema

**Flussi Alternativi:**
- 5a. Validazione fallisce:
  - Il sistema mostra messaggi di errore
  - L'utente corregge i dati
  - Ritorna al punto 4
- 6a. Errore durante la creazione:
  - Il sistema mostra messaggio di errore
  - I dati inseriti vengono salvati in bozza
  - L'utente può riprovare successivamente

**Postcondizioni:**
- Nuovo problema creato e visibile nella piattaforma
- Notifiche inviate agli utenti interessati

### Flusso 2: Rispondere a un Problema

**Attori:** Utente Registrato

**Precondizioni:**
- L'utente è autenticato
- Il problema è in stato "Aperto" o è stato aperto da meno di 30 giorni dalla chiusura

**Flusso Principale:**
1. L'utente visualizza un problema
2. L'utente scorre i commenti esistenti
3. L'utente clicca su "Aggiungi Risposta"
4. Il sistema presenta l'editor di commenti
5. L'utente scrive la risposta
6. (Opzionale) L'utente allega file media
7. L'utente conferma l'invio
8. Il sistema valida il contenuto
9. Il sistema crea il commento
10. Il sistema invia notifica all'autore del problema
11. Il sistema aggiorna la vista con il nuovo commento

**Flussi Alternativi:**
- 8a. Validazione fallisce:
  - Il sistema mostra errore
  - L'utente corregge il contenuto
  - Ritorna al punto 7
- 3a. Il problema è chiuso da più di 30 giorni:
  - Il sistema disabilita l'opzione di risposta
  - Mostra messaggio informativo

**Postcondizioni:**
- Nuovo commento aggiunto al problema
- Notifica inviata all'autore del problema

### Flusso 3: Votare un Commento

**Attori:** Utente Registrato

**Precondizioni:**
- L'utente è autenticato
- Il commento non è dell'utente stesso
- Il problema non è chiuso da più di 30 giorni

**Flusso Principale:**
1. L'utente visualizza un commento
2. L'utente clicca su icona voto positivo o negativo
3. Il sistema registra il voto
4. Il sistema aggiorna il punteggio del commento
5. Il sistema aggiorna la reputazione dell'autore del commento
6. Il sistema invia notifica all'autore (se voto positivo e raggiunge soglie significative)
7. Il sistema aggiorna l'interfaccia mostrando il voto registrato

**Flussi Alternativi:**
- 2a. L'utente aveva già votato:
  - 2a1. Clicca sullo stesso tipo di voto: il voto viene rimosso
  - 2a2. Clicca su voto opposto: il voto viene cambiato
  - Il sistema aggiorna di conseguenza punteggio e reputazione
- 2b. L'utente cerca di votare il proprio commento:
  - Il sistema disabilita i pulsanti di voto
  - Mostra tooltip esplicativo

**Postcondizioni:**
- Voto registrato o aggiornato
- Punteggio commento aggiornato
- Reputazione autore aggiornata

### Flusso 4: Chiudere un Problema con Soluzione

**Attori:** Utente Registrato (Autore del Problema)

**Precondizioni:**
- L'utente è l'autore del problema
- Il problema ha almeno un commento
- Il problema è in stato "Aperto"

**Flusso Principale:**
1. L'utente visualizza il proprio problema
2. L'utente scorre i commenti
3. L'utente identifica il commento che ha risolto il problema
4. L'utente clicca su "Marca come Soluzione" sul commento prescelto
5. Il sistema mostra dialogo di conferma
6. L'utente conferma l'azione
7. Il sistema marca il commento come soluzione
8. Il sistema cambia lo stato del problema da "Aperto" a "Chiuso"
9. Il sistema assegna punti reputazione all'autore della soluzione
10. Il sistema invia notifica all'autore della soluzione
11. Il sistema aggiorna l'interfaccia evidenziando la soluzione

**Flussi Alternativi:**
- 4a. L'utente vuole chiudere senza soluzione:
  - L'utente clicca su "Chiudi Problema"
  - Il sistema richiede spiegazione
  - L'utente può indicare "Risolto autonomamente" o "Non più rilevante"
- 3a. Non ci sono commenti utili:
  - L'utente può chiudere indicando "Nessuna soluzione trovata"

**Postcondizioni:**
- Problema marcato come "Chiuso"
- Soluzione evidenziata
- Notifica inviata
- Reputazione aggiornata

### Flusso 5: Seguire una Categoria

**Attori:** Utente Registrato

**Precondizioni:**
- L'utente è autenticato

**Flusso Principale:**
1. L'utente naviga nel catalogo categorie o visualizza una categoria
2. L'utente clicca su "Segui Categoria"
3. Il sistema registra l'iscrizione
4. Il sistema aggiorna l'interfaccia mostrando "Stai Seguendo"
5. Il sistema conferma che l'utente riceverà notifiche per nuovi problemi

**Flussi Alternativi:**
- 2a. L'utente già seguiva la categoria:
  - Il pulsante mostra "Smetti di Seguire"
  - Click rimuove l'iscrizione
  - L'utente non riceverà più notifiche

**Postcondizioni:**
- Iscrizione alla categoria registrata/rimossa
- Notifiche abilitate/disabilitate per quella categoria

### Flusso 6: Ricerca e Navigazione

**Attori:** Qualsiasi Utente (anche non registrato)

**Precondizioni:**
- Nessuna

**Flusso Principale:**
1. L'utente accede alla home page o barra di ricerca
2. L'utente può:
   - 2a. Cercare per parole chiave
   - 2b. Filtrare per categoria
   - 2c. Filtrare per stato (Aperto/Chiuso)
   - 2d. Ordinare per data, visualizzazioni, numero commenti
3. Il sistema mostra i risultati corrispondenti
4. L'utente clicca su un problema per visualizzarlo
5. Il sistema mostra la pagina del problema con tutti i dettagli

**Flussi Alternativi:**
- 2a1. Ricerca per parole chiave:
  - Il sistema cerca in titoli e descrizioni
  - Mostra risultati ordinati per rilevanza
- 2b1. Navigazione per categoria:
  - Il sistema mostra albero categorie
  - L'utente seleziona categoria o sottocategoria
  - Mostra problemi della categoria selezionata

**Postcondizioni:**
- Utente trova e visualizza contenuti di interesse

### Flusso 7: Moderazione Contenuti

**Attori:** Amministratore

**Precondizioni:**
- L'amministratore è autenticato
- Esiste contenuto da moderare (segnalato o individuato)

**Flusso Principale:**
1. L'amministratore accede alla dashboard di moderazione
2. Il sistema mostra lista di segnalazioni pendenti
3. L'amministratore seleziona una segnalazione
4. Il sistema mostra il contenuto segnalato e il contesto
5. L'amministratore rivede il contenuto
6. L'amministratore decide l'azione:
   - 6a. Approva (nessuna violazione)
   - 6b. Rimuove contenuto
   - 6c. Sospende utente
   - 6d. Banna utente
7. Il sistema applica l'azione selezionata
8. Il sistema invia notifica all'utente interessato
9. Il sistema registra l'azione nel log di moderazione

**Flussi Alternativi:**
- 6b. Rimozione contenuto:
  - Il sistema sostituisce il contenuto con messaggio standard
  - Incrementa contatore violazioni utente
- 6c. Sospensione utente:
  - Il sistema disabilita temporaneamente l'account
  - Specifica durata sospensione
- 6d. Ban utente:
  - Il sistema disabilita permanentemente l'account
  - L'utente non può più accedere

**Postcondizioni:**
- Segnalazione gestita
- Azione di moderazione applicata
- Log aggiornato

### Flusso 8: Assegnazione Badge Esperto

**Attori:** Amministratore

**Precondizioni:**
- L'amministratore è autenticato
- Esiste un utente meritevole di riconoscimento in una categoria

**Flusso Principale:**
1. L'amministratore accede alla gestione utenti/esperti
2. Il sistema mostra statistiche utenti per categoria
3. L'amministratore identifica utente da premiare
4. L'amministratore seleziona categoria e utente
5. L'amministratore clicca su "Assegna Badge Esperto"
6. Il sistema registra il badge
7. Il sistema invia notifica all'utente
8. Il sistema aggiorna il profilo dell'utente
9. Il badge appare nei problemi/commenti dell'utente in quella categoria

**Flussi Alternativi:**
- 3a. Sistema suggerisce automaticamente candidati:
  - Basato su algoritmo di reputazione per categoria
  - Amministratore rivede e approva suggerimenti

**Postcondizioni:**
- Badge esperto assegnato
- Utente notificato
- Badge visibile pubblicamente

---

## Sistema di Categorie

### Struttura

**Gerarchia:**
```
Categoria Principale
├── Sottocategoria 1
│   ├── Sotto-sottocategoria 1.1
│   └── Sotto-sottocategoria 1.2
├── Sottocategoria 2
└── Sottocategoria 3
```

**Livelli Massimi:** 3 livelli di profondità

### Esempi di Categorie

**Tecnologia**
- Programmazione
  - Frontend (HTML, CSS, JavaScript)
  - Backend (Node.js, Python, Java)
  - Mobile (iOS, Android)
- Hardware
  - Computer
  - Smartphone
  - Periferiche
- Reti e Sicurezza

**Casa e Fai-da-te**
- Idraulica
- Elettricità
- Falegnameria
- Giardinaggio

**Vita Quotidiana**
- Cucina e Ricette
- Salute e Benessere
- Finanza Personale
- Relazioni e Comunicazione

**Educazione**
- Matematica
- Scienze
- Lingue Straniere
- Arte e Musica

### Funzionalità delle Categorie

**Per gli Utenti:**
- Iscrizione/disiscrizione con un click
- Visualizzazione statistiche (numero problemi, esperti)
- Filtro e ricerca problemi per categoria
- Ricezione notifiche personalizzate

**Per gli Amministratori:**
- Creazione/modifica/eliminazione categorie
- Organizzazione gerarchica
- Assegnazione esperti
- Monitoraggio attività per categoria
- Merge di categorie simili

**Metadati Categoria:**
- Numero totale problemi
- Numero problemi aperti/chiusi
- Tasso di risoluzione
- Tempo medio di risoluzione
- Top esperti
- Utenti iscritti

---

## Sistema di Notifiche

### Tipi di Notifiche

**1. Notifiche sui Propri Contenuti**
- Nuovo commento su tuo problema
- Tuo commento votato positivamente (soglie: 5, 10, 25, 50 voti)
- Tuo commento marcato come soluzione
- Tuo problema riaperto

**2. Notifiche di Categoria**
- Nuovo problema in categoria seguita
- Problema interessante nella tua area di expertise

**3. Notifiche Sociali**
- Menzione in un commento (@username)
- Nuovo follower (se implementato)
- Risposta a tuo commento

**4. Notifiche di Sistema**
- Badge esperto assegnato
- Livello reputazione raggiunto
- Contenuto moderato/rimosso
- Sospensione account

### Canali di Notifica

**In-App:**
- Icona campanella con contatore
- Lista notifiche con dettagli
- Marcatura come letto/non letto

**Email:**
- Digest giornaliero (configurabile)
- Notifiche immediate per eventi importanti
- Opzione di disattivazione per tipo

**Push (se app mobile):**
- Notifiche push configurabili
- Priorità per eventi urgenti

### Preferenze Utente

**Configurazioni Disponibili:**
- Abilita/disabilita per tipo di notifica
- Frequenza email (immediata, giornaliera, settimanale, mai)
- Filtri per categoria
- Soglie personalizzate (es. notifica solo per >10 voti)

### Aggregazione Notifiche

**Regole:**
- Multiple notifiche simili aggregate in una
- Esempio: "5 nuovi problemi in Programmazione" invece di 5 notifiche separate
- Periodo aggregazione: 1 ora per notifiche categoria, immediato per notifiche personali

### Gestione Notifiche

**Ciclo di Vita:**
1. Evento trigger genera notifica
2. Sistema verifica preferenze utente
3. Se abilitata, notifica viene creata
4. Notifica inviata tramite canali configurati
5. Utente visualizza e marca come letta
6. Dopo 30 giorni, notifica archiviata
7. Dopo 90 giorni, notifica eliminata

---

## Sistema di Votazione

### Meccanica dei Voti

**Tipi di Voto:**
- **Voto Positivo (+1)**: Il commento è utile, accurato, ben spiegato
- **Voto Negativo (-1)**: Il commento non è utile, impreciso, fuori tema

**Calcolo Punteggio:**
```
Punteggio Netto = Voti Positivi - Voti Negativi
```

### Regole di Votazione

**Chi Può Votare:**
- Solo utenti registrati
- Non l'autore del proprio commento
- Solo una volta per commento (ma modificabile)

**Restrizioni:**
- Problemi chiusi da >30 giorni: votazione disabilitata
- Account sospesi: votazione disabilitata
- Utenti nuovi (<7 giorni): solo voti positivi

### Impatto sulla Reputazione

**Per l'Autore del Commento:**
- +2 punti per ogni voto positivo ricevuto
- -1 punto per ogni voto negativo ricevuto
- Bonus per commenti con alto punteggio:
  - +5 punti bonus al raggiungimento di 10 voti netti
  - +10 punti bonus al raggiungimento di 25 voti netti

**Per il Votante:**
- Nessun impatto diretto
- Statistiche tracking per analisi comportamentale

### Visualizzazione dei Voti

**Per Tutti:**
- Punteggio netto visibile accanto al commento
- Indicatore grafico (colore verde per positivi, rosso per negativi)

**Per l'Autore:**
- Dettaglio completo: X voti positivi, Y voti negativi
- Grafico evoluzione voti nel tempo

**Per gli Amministratori:**
- Lista completa votanti
- Analisi pattern di voto sospetti

### Ordinamento Commenti

**Criteri Disponibili:**
1. **Per Rilevanza (default)**: 
   - Soluzione in cima
   - Poi per punteggio netto
   - A parità di punteggio, più recente prima
2. **Per Data**: Cronologico (nuovo → vecchio)
3. **Per Controversia**: Commenti con molti voti sia positivi che negativi

### Protezione Anti-Abuso

**Rilevamento Pattern Sospetti:**
- Voti multipli dallo stesso IP
- Voti coordinati da gruppo utenti
- Votazione massiva in breve tempo

**Azioni Automatiche:**
- Flag per revisione amministratore
- Temporanea disabilitazione votazione per utenti sospetti
- Invalidazione voti fraudolenti

**Penalità:**
- Sospensione capacità di votare
- Riduzione reputazione per votanti fraudolenti
- Ban per abusi ripetuti

---

## Diagrammi Concettuali

### Relazioni tra Entità

```
UTENTE
│
├──> pubblica ──> PROBLEMA
│                    │
│                    ├──> appartiene a ──> CATEGORIA
│                    │
│                    └──> riceve ──> COMMENTO
│                                      │
├──> scrive ────────────────────────> │
│                                      │
├──> vota ────────────────────────────┘
│
├──> segue ──────────> CATEGORIA
│
├──> riceve ──────────> NOTIFICA
│
└──> possiede ────────> BADGE ESPERTO (per CATEGORIA)
```

### Stati del Problema

```
[Bozza] ──pubblicazione──> [Aperto] ──chiusura──> [Chiuso]
                              │                       │
                              └───── riapertura ──────┘
```

### Flusso Notifiche

```
EVENTO
  │
  ├──> Verifica Preferenze Utente
  │         │
  │         ├──> Se Disabilitate ──> STOP
  │         │
  │         └──> Se Abilitate
  │                  │
  │                  ├──> Crea Notifica In-App
  │                  │
  │                  ├──> Invia Email (se configurato)
  │                  │
  │                  └──> Invia Push (se configurato)
  │
  └──> Registra in Log Eventi
```

---

## Glossario

**Badge**: Riconoscimento visuale assegnato a utenti per meriti specifici

**Ban**: Esclusione permanente dalla piattaforma

**Categoria**: Area tematica per organizzare problemi

**Chiusura**: Azione che marca un problema come risolto

**Commento**: Risposta o contributo a un problema

**Digest**: Raccolta aggregata di notifiche inviate periodicamente

**Esperto**: Utente riconosciuto come competente in una categoria

**Expertise**: Area di competenza di un utente

**Flag**: Marcatore o segnalazione su un contenuto

**Media**: File multimediali allegati (immagini, video, documenti)

**Moderazione**: Supervisione e gestione dei contenuti da parte di amministratori

**Notifica**: Avviso inviato a un utente riguardo eventi di interesse

**Punteggio Netto**: Differenza tra voti positivi e negativi

**Reputazione**: Sistema di punti che riflette i contributi di un utente

**Segnalazione**: Reportistica di contenuto inappropriato da parte di utenti

**Soluzione**: Commento identificato come risolutivo per un problema

**Sottocategoria**: Categoria figlia di una categoria principale

**Stato**: Condizione corrente di un problema (Aperto/Chiuso)

**Sospensione**: Disabilitazione temporanea di un account

**Voto**: Valutazione positiva o negativa di un commento

---

## Metriche e KPI

### Metriche di Engagement

**Utenti:**
- Numero utenti registrati
- Utenti attivi giornalieri (DAU)
- Utenti attivi mensili (MAU)
- Tasso di ritorno utenti

**Contenuti:**
- Problemi pubblicati per giorno/settimana/mese
- Commenti per problema (media)
- Tasso di risposta (<1h, <24h, <7gg)
- Visualizzazioni per problema (media)

### Metriche di Qualità

**Risoluzione:**
- Tasso di risoluzione problemi (%)
- Tempo medio di risoluzione
- Problemi risolti per categoria

**Votazione:**
- Commenti con punteggio positivo (%)
- Distribuzione punteggi commenti
- Correlazione voti-soluzione

### Metriche di Community

**Partecipazione:**
- Percentuale utenti che pubblicano problemi
- Percentuale utenti che commentano
- Percentuale utenti che votano
- Ratio domande/risposte per utente

**Expertise:**
- Numero esperti per categoria
- Soluzioni per esperto (media)
- Tasso risposta esperti vs non-esperti

### Metriche di Moderazione

**Volume:**
- Segnalazioni ricevute per giorno
- Tempo medio gestione segnalazione
- Percentuale segnalazioni fondate

**Azioni:**
- Contenuti rimossi per tipo
- Sospensioni/ban effettuati
- Ricorsi gestiti

---

## Considerazioni Future

### Possibili Evoluzioni

**Funzionalità Social Avanzate:**
- Sistema di following tra utenti
- Direct messaging
- Gruppi privati per categoria
- Eventi e webinar

**Gamification:**
- Achievement system
- Leaderboard per categoria
- Sfide mensili
- Punti esperienza (XP)

**AI e Machine Learning:**
- Suggerimento categoria automatico
- Rilevamento duplicati
- Raccomandazioni problemi correlati
- Rilevamento spam automatico
- Suggerimento esperti per problema

**Integrazioni:**
- Login social (Google, GitHub, ecc.)
- Condivisione su social media
- Integrazione calendario per eventi
- API pubblica per sviluppatori

**Monetizzazione (opzionale):**
- Account premium con funzionalità extra
- Priorità supporto
- Analytics avanzate
- Rimozione pubblicità

**Mobile:**
- App nativa iOS/Android
- Notifiche push
- Modalità offline
- Fotocamera integrata per media

### Scalabilità

**Tecnica:**
- Caching aggressivo per performance
- CDN per media
- Database replication
- Microservizi per funzionalità separate

**Organizzativa:**
- Team moderazione distribuito
- Moderatori community volontari
- Sistema di appeals per decisioni moderazione
- Wiki/FAQ community-driven

---

## Conclusioni

Questo Memory Bank fornisce una visione completa e strutturata di HelpMe!, coprendo:

✅ **Visione**: Obiettivi e proposta di valore della piattaforma  
✅ **Ruoli**: Tre livelli di utenti con permessi chiari  
✅ **Concetti Chiave**: Entità principali e loro attributi  
✅ **Regole di Business**: Vincoli e logiche operative  
✅ **Flussi**: 8 processi principali documentati  
✅ **Sistemi Specializzati**: Categorie, notifiche e votazione  

La documentazione è pronta per guidare:
- **Sviluppatori**: Nell'implementazione tecnica
- **Designer**: Nella progettazione UI/UX
- **Product Manager**: Nella pianificazione feature
- **Stakeholder**: Nella comprensione del progetto

Il sistema è progettato per essere:
- **Scalabile**: Può crescere con l'utenza
- **Flessibile**: Permette evoluzioni future
- **Sicuro**: Include moderazione e anti-abuso
- **User-friendly**: Accessibile e intuitivo

**Prossimi passi consigliati:**
1. Validazione con stakeholder
2. Creazione wireframe UI
3. Definizione architettura tecnica
4. Progettazione schema database
5. Sviluppo MVP con feature core
