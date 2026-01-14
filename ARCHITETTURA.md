# Architettura Concettuale - HelpMe!

## Introduzione

Questo documento descrive l'architettura concettuale di HelpMe! a livello logico, senza entrare nei dettagli implementativi. L'obiettivo è fornire una visione chiara dei componenti del sistema e delle loro interazioni.

---

## Architettura a Livelli

### Vista ad Alto Livello

```
┌─────────────────────────────────────────────────────────────┐
│                     LIVELLO PRESENTAZIONE                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │  Web Browser │  │  Mobile App  │  │   API REST   │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                     LIVELLO APPLICAZIONE                     │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Gestione   │  │   Gestione   │  │   Gestione   │      │
│  │   Problemi   │  │   Utenti     │  │  Categorie   │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Gestione   │  │   Sistema    │  │   Sistema    │      │
│  │  Commenti    │  │  Votazione   │  │  Notifiche   │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Sistema    │  │  Moderazione │  │   Ricerca    │      │
│  │    Media     │  │              │  │              │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                       LIVELLO DATI                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Database   │  │  File Store  │  │    Cache     │      │
│  │  Relazionale │  │   (Media)    │  │              │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    SERVIZI ESTERNI                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │    Email     │  │     CDN      │  │   Analytics  │      │
│  │   Service    │  │              │  │              │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
```

---

## Componenti Principali

### 1. Gestione Problemi

**Responsabilità:**
- Creazione, modifica, eliminazione problemi
- Gestione stato (Aperto/Chiuso)
- Associazione categorie
- Gestione media allegati
- Chiusura con selezione soluzione

**Interazioni:**
- Con Gestione Categorie (per validazione e associazione)
- Con Sistema Media (per upload allegati)
- Con Sistema Notifiche (per avvisi creazione/chiusura)
- Con Gestione Utenti (per permessi)

**Input:**
- Dati problema (titolo, descrizione, categorie)
- Azioni utente (crea, modifica, chiudi, riapri)

**Output:**
- Problema creato/aggiornato
- Notifiche generate
- Eventi per sistema di notifiche

### 2. Gestione Commenti

**Responsabilità:**
- Creazione, modifica, eliminazione commenti
- Associazione a problemi
- Marcatura come soluzione
- Gestione timestamp e cronologia modifiche

**Interazioni:**
- Con Gestione Problemi (collegamento)
- Con Sistema Votazione (per punteggi)
- Con Sistema Notifiche (per nuovi commenti)
- Con Sistema Media (per allegati)

**Input:**
- Testo commento
- Riferimento problema
- Media (opzionale)

**Output:**
- Commento pubblicato
- Notifica all'autore problema
- Aggiornamento contatori

### 3. Sistema Votazione

**Responsabilità:**
- Registrazione voti (positivi/negativi)
- Calcolo punteggi netti
- Prevenzione voti multipli
- Aggiornamento reputazione

**Interazioni:**
- Con Gestione Commenti (target voti)
- Con Gestione Utenti (per reputazione)
- Con Sistema Notifiche (per soglie raggiunte)

**Regole:**
- Un voto per utente per commento
- No auto-voto
- Cambio voto consentito

**Input:**
- Utente votante
- Commento target
- Tipo voto (positivo/negativo)

**Output:**
- Voto registrato
- Punteggio aggiornato
- Reputazione aggiornata

### 4. Gestione Utenti

**Responsabilità:**
- Registrazione e autenticazione
- Gestione profili
- Gestione ruoli e permessi
- Tracking reputazione
- Gestione badge esperti
- Statistiche utente

**Interazioni:**
- Con tutti i componenti (autenticazione)
- Con Gestione Categorie (iscrizioni)
- Con Sistema Notifiche (preferenze)

**Dati Gestiti:**
- Credenziali
- Profilo personale
- Statistiche contributi
- Badge e riconoscimenti

### 5. Gestione Categorie

**Responsabilità:**
- CRUD categorie
- Gestione gerarchia
- Gestione iscrizioni utenti
- Identificazione esperti
- Statistiche per categoria

**Interazioni:**
- Con Gestione Problemi (associazioni)
- Con Gestione Utenti (iscrizioni, badge esperti)
- Con Sistema Notifiche (per iscritti)

**Struttura:**
- Albero gerarchico (max 3 livelli)
- Metadati (icone, descrizioni)
- Liste iscritti ed esperti

### 6. Sistema Notifiche

**Responsabilità:**
- Generazione notifiche
- Gestione preferenze utente
- Aggregazione notifiche simili
- Invio multi-canale (in-app, email, push)
- Gestione stato (letta/non letta)

**Interazioni:**
- Con tutti i componenti (ricezione eventi)
- Con Gestione Utenti (preferenze, destinatari)
- Con Servizi Esterni (invio email/push)

**Tipi Gestiti:**
- Notifiche contenuti
- Notifiche categoria
- Notifiche sociali
- Notifiche sistema

**Flusso:**
```
Evento → Verifica Preferenze → Crea Notifica → Invia → Aggiorna Stato
```

### 7. Sistema Media

**Responsabilità:**
- Upload file (immagini, video, documenti)
- Validazione formato e dimensione
- Storage organizzato
- Generazione URL accessibili
- Ottimizzazione (resize, compressione)

**Limiti:**
- Max 10 file per problema/commento
- Max 10MB per file
- Formati: JPG, PNG, GIF, MP4, PDF

**Interazioni:**
- Con Gestione Problemi (allegati problema)
- Con Gestione Commenti (allegati commento)
- Con File Store (persistenza)
- Con CDN (distribuzione)

### 8. Sistema Ricerca

**Responsabilità:**
- Indicizzazione contenuti
- Ricerca full-text
- Filtri e ordinamento
- Suggerimenti auto-complete

**Capacità:**
- Ricerca in titoli e descrizioni
- Filtro per categoria
- Filtro per stato
- Ordinamento multiplo

**Indici:**
- Testo problemi
- Categoria
- Data
- Stato
- Autore

### 9. Sistema Moderazione

**Responsabilità:**
- Gestione segnalazioni
- Revisione contenuti
- Azioni disciplinari
- Log audit

**Funzionalità:**
- Coda segnalazioni
- Strumenti revisione
- Rimozione contenuti
- Gestione sanzioni
- Reportistica

**Azioni Disponibili:**
- Approva (falso positivo)
- Rimuovi contenuto
- Sospendi utente (temporaneo)
- Ban utente (permanente)

---

## Modello dei Dati Concettuale

### Entità Principali e Relazioni

```
┌──────────────┐
│    UTENTE    │
└──────────────┘
       │ 1
       │
       │ pubblica
       ├──────────┐
       │          ▼ *
       │     ┌──────────────┐
       │     │   PROBLEMA   │
       │     └──────────────┘
       │          │ *
       │          │ appartiene a
       │          ▼ *
       │     ┌──────────────┐
       │     │  CATEGORIA   │◄────┐
       │     └──────────────┘     │ gerarchia
       │          │ 1             │ 
       │          │ padre/figlio  │
       │          └───────────────┘
       │
       │ scrive
       ├──────────┐
       │          ▼ *
       │     ┌──────────────┐
       │     │  COMMENTO    │
       │     └──────────────┘
       │          │ *
       │          │ riferito a
       │          ▼ 1
       │     [PROBLEMA]
       │
       │ vota
       ├──────────┐
       │          ▼ *
       │     ┌──────────────┐
       │     │     VOTO     │
       │     └──────────────┘
       │          │ *
       │          │ su
       │          ▼ 1
       │     [COMMENTO]
       │
       │ segue
       ├──────────┐
       │          ▼ *
       │     [CATEGORIA]
       │
       │ riceve
       └──────────┐
                  ▼ *
             ┌──────────────┐
             │  NOTIFICA    │
             └──────────────┘
```

### Cardinalità Chiave

- **Utente → Problema**: 1 a molti (un utente pubblica molti problemi)
- **Problema → Categoria**: molti a molti (problema ha più categorie, categoria ha più problemi)
- **Problema → Commento**: 1 a molti (problema ha molti commenti)
- **Commento → Voto**: 1 a molti (commento ha molti voti)
- **Utente → Voto**: 1 a molti (utente dà molti voti)
- **Utente ↔ Categoria**: molti a molti (per iscrizioni e badge esperto)
- **Categoria → Categoria**: 1 a molti (gerarchia padre-figlio)

---

## Flussi di Interazione Componenti

### Flusso: Pubblicazione Problema

```
[Utente] → [UI] → [Gestione Problemi]
                          │
                          ├─→ [Gestione Categorie] (validazione categorie)
                          │
                          ├─→ [Sistema Media] (upload allegati)
                          │
                          ├─→ [Database] (persistenza)
                          │
                          └─→ [Sistema Notifiche]
                                     │
                                     ├─→ [Gestione Categorie] (lista iscritti)
                                     │
                                     ├─→ [Gestione Utenti] (preferenze)
                                     │
                                     └─→ [Email Service] (invio notifiche)
```

### Flusso: Votazione Commento

```
[Utente] → [UI] → [Sistema Votazione]
                          │
                          ├─→ [Gestione Commenti] (validazione)
                          │
                          ├─→ [Database] (registra voto)
                          │
                          ├─→ [Gestione Commenti] (aggiorna punteggio)
                          │
                          ├─→ [Gestione Utenti] (aggiorna reputazione)
                          │
                          └─→ [Sistema Notifiche] (se soglia raggiunta)
```

### Flusso: Ricerca Problema

```
[Utente] → [UI] → [Sistema Ricerca]
                          │
                          ├─→ [Cache] (check cache)
                          │
                          ├─→ [Database] (query)
                          │
                          ├─→ [Gestione Problemi] (filtra risultati)
                          │
                          └─→ [UI] (mostra risultati)
```

### Flusso: Moderazione

```
[Utente] → [UI] → [Segnalazione]
                       │
                       ▼
              [Sistema Moderazione]
                       │
                       ├─→ [Database] (coda segnalazioni)
                       │
[Admin] → [UI] → [Sistema Moderazione]
                       │
                       ├─→ [Gestione Problemi/Commenti] (rimozione)
                       │
                       ├─→ [Gestione Utenti] (sanzioni)
                       │
                       ├─→ [Sistema Notifiche] (avviso utente)
                       │
                       └─→ [Database] (log audit)
```

---

## Gestione Stati e Transizioni

### Stati del Problema

```
     [Iniziale]
         │
         ▼
     ┌─────────┐
     │  Bozza  │ (opzionale)
     └─────────┘
         │
         │ pubblica
         ▼
     ┌─────────┐  chiudi   ┌─────────┐
     │ Aperto  │────────────▶│ Chiuso  │
     └─────────┘            └─────────┘
         ▲                       │
         │       riapri          │
         └───────────────────────┘
```

**Trigger Transizioni:**
- Bozza → Aperto: Utente pubblica
- Aperto → Chiuso: Autore seleziona soluzione
- Chiuso → Aperto: Autore riapre problema

### Stati della Notifica

```
   [Evento]
      │
      ▼
┌──────────┐
│  Creata  │
└──────────┘
      │
      ▼
┌──────────┐  visualizza  ┌──────────┐
│ Inviata  │──────────────▶│  Letta   │
└──────────┘              └──────────┘
      │                        │
      │ +30 giorni            │ +30 giorni
      ▼                        ▼
┌──────────┐              ┌──────────┐
│Archiviata│              │Archiviata│
└──────────┘              └──────────┘
      │                        │
      │ +60 giorni            │ +60 giorni
      ▼                        ▼
  [Eliminata]              [Eliminata]
```

### Stati dell'Utente

```
┌──────────────┐
│Non Registrato│
└──────────────┘
       │
       │ registrazione
       ▼
┌──────────────┐  promozione  ┌──────────────┐
│  Registrato  │──────────────▶│Amministratore│
└──────────────┘              └──────────────┘
   │       ▲                        │
   │       │                        │
   │ 3 violazioni                   │
   ▼       │ fine sospensione       │
┌──────────────┐                    │
│   Sospeso    │                    │
└──────────────┘                    │
       │                            │
       │ 5 violazioni               │
       ▼                            ▼
┌──────────────┐              ┌──────────────┐
│   Bannato    │              │   Bannato    │
└──────────────┘              └──────────────┘
   (permanente)                  (permanente)
```

---

## Pattern di Sicurezza

### Controllo Accessi

**Livelli di Autorizzazione:**

```
┌────────────────────┬─────────┬────────────┬──────────────┐
│ Operazione         │ Visitor │ Registrato │ Admin        │
├────────────────────┼─────────┼────────────┼──────────────┤
│ Visualizza         │    ✓    │     ✓      │      ✓       │
│ Ricerca            │    ✓    │     ✓      │      ✓       │
│ Pubblica Problema  │    ✗    │     ✓      │      ✓       │
│ Commenta           │    ✗    │     ✓      │      ✓       │
│ Vota               │    ✗    │     ✓      │      ✓       │
│ Chiudi Proprio     │    ✗    │     ✓      │      ✓       │
│ Modifica Proprio   │    ✗    │ ✓ (15 min) │      ✓       │
│ Elimina Proprio    │    ✗    │     ✓      │      ✓       │
│ Modera Contenuti   │    ✗    │     ✗      │      ✓       │
│ Gestisce Categorie │    ✗    │     ✗      │      ✓       │
│ Gestisce Utenti    │    ✗    │     ✗      │      ✓       │
│ Assegna Badge      │    ✗    │     ✗      │      ✓       │
└────────────────────┴─────────┴────────────┴──────────────┘
```

### Validazione Input

**Livelli di Validazione:**

1. **Client-Side**: Validazione immediata per UX
2. **API Gateway**: Validazione formato e autenticazione
3. **Business Logic**: Validazione regole di business
4. **Database**: Constraint e integrità referenziale

**Campi Critici:**
- Titolo: Lunghezza, caratteri speciali, SQL injection
- Descrizione: XSS prevention, HTML sanitization
- Media: Tipo file, dimensione, malware scan
- Email: Formato valido, unicità

### Sanitizzazione Contenuti

**Protezioni:**
- **XSS**: Escape HTML in output
- **SQL Injection**: Prepared statements
- **CSRF**: Token validation
- **File Upload**: Type validation, virus scan
- **Rate Limiting**: Prevenzione spam e abusi

---

## Considerazioni di Scalabilità

### Strategie di Caching

**Livello 1 - Browser Cache:**
- Static assets (CSS, JS, immagini)
- TTL: 7 giorni

**Livello 2 - CDN:**
- Media files
- Contenuti pubblici frequentemente accessati
- TTL: 24 ore

**Livello 3 - Application Cache:**
- Liste categorie
- Profili utente
- Problemi popolari
- TTL: 15 minuti - 1 ora

**Livello 4 - Database Query Cache:**
- Query complesse ripetute
- TTL: 5 minuti

### Ottimizzazioni Database

**Indici:**
- Problemi: (categoria_id, data_creazione)
- Commenti: (problema_id, punteggio)
- Voti: (utente_id, commento_id)
- Notifiche: (utente_id, letta, data_creazione)

**Partitioning:**
- Problemi per data (annuale/mensile)
- Notifiche per stato (attive/archiviate)

**Denormalizzazione Selettiva:**
- Contatori (num_commenti, num_visualizzazioni)
- Punteggi aggregati
- Statistiche utente

### Load Balancing

**Distribuzione Carico:**
```
           [Load Balancer]
                 │
     ┌───────────┼───────────┐
     ▼           ▼           ▼
[App Server 1][App Server 2][App Server 3]
     │           │           │
     └───────────┼───────────┘
                 ▼
        [Database Cluster]
```

**Strategie:**
- Round-robin per traffico web
- Session affinity per websocket
- Geographic routing per CDN

---

## Monitoraggio e Observability

### Metriche da Tracciare

**Performance:**
- Tempo risposta API
- Throughput requests/sec
- Database query time
- Cache hit ratio

**Business:**
- Problemi pubblicati/ora
- Tasso risoluzione
- Utenti attivi
- Engagement rate

**Qualità:**
- Tasso errori
- Uptime
- Segnalazioni moderate
- Tempo moderazione

**Infrastruttura:**
- CPU/RAM utilization
- Disk I/O
- Network latency
- Storage capacity

### Health Checks

**Endpoint:**
- `/health`: Status generale
- `/health/db`: Connessione database
- `/health/cache`: Funzionamento cache
- `/health/external`: Servizi esterni

**Alert Conditions:**
- Response time >2s
- Error rate >1%
- Database connection pool >80%
- Disk space <10%

---

## Considerazioni di Privacy

### Dati Personali

**Pubblici:**
- Username
- Avatar
- Bio
- Statistiche pubbliche
- Contenuti pubblicati

**Privati:**
- Email
- Password (hashed)
- Preferenze notifiche
- Indirizzo IP
- Log attività

### GDPR Compliance

**Diritti Utente:**
- **Accesso**: Export dati personali
- **Rettifica**: Modifica profilo
- **Cancellazione**: Right to be forgotten
- **Portabilità**: Formato machine-readable
- **Opposizione**: Opt-out notifiche

**Gestione Cancellazione:**
- Account eliminato
- Email anonimizzata
- IP cancellati
- Contenuti: mantieni con username "[Utente Eliminato]"

---

## Backup e Disaster Recovery

### Strategia Backup

**Database:**
- Full backup: Giornaliero (3am)
- Incremental: Ogni 6 ore
- Retention: 30 giorni

**Media Files:**
- Backup: Giornaliero
- Replica geografica
- Retention: 90 giorni

**Configurazione:**
- Version control (Git)
- Backup configurazioni: Settimanale

### Recovery Procedures

**RTO (Recovery Time Objective):**
- Critical systems: <1 ora
- Non-critical: <4 ore

**RPO (Recovery Point Objective):**
- Database: <6 ore
- Media: <24 ore

---

## Conclusioni

Questa architettura concettuale fornisce:

✅ **Modularità**: Componenti indipendenti e sostituibili  
✅ **Scalabilità**: Design pronto per crescita  
✅ **Sicurezza**: Controlli multi-livello  
✅ **Manutenibilità**: Separazione chiara delle responsabilità  
✅ **Resilienza**: Strategie backup e recovery  

**Prossimi step implementativi:**
1. Scelta stack tecnologico
2. Design dettagliato database
3. Definizione API REST
4. Setup infrastruttura
5. Implementazione MVP
