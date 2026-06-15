# Sistema di gestione biblioteca

# Descrizione problema
Sistema di gestione biblioteca

Progetta un'applicazione che permetta:

Registrazione utenti
Prestito libri
Restituzione libri
Ricerca libri
Storico prestiti
Requisiti
100 utenti contemporanei
Database relazionale
Nessun requisito di alta disponibilità
Nessun requisito di scalabilità estrema

## Requisiti funzionali
- Gli utenti devono potersi registrare e accedere al sistema.
- Gli utenti possono chiedere in prestito libri disponibili.
- Gli utenti possono restituire i libri presi in prestito.
- Gli utenti possono visualizzare la lista dei libri disponibili.
- Gli utenti possono visualizzare la lista dei libri presi in prestito.

## Requisiti non funzionali
- Il sistema deve essere disponibile 24/7.
- Il sistema deve supportare almeno 100 utenti contemporaneamente.
- Deve utilizzare un database relazionale per la gestione dei dati.

## API
- POST /register: per registrare un nuovo utente.
- POST /login: per autenticare un utente esistente.

- POST /borrow: per prendere in prestito un libro.
- POST /return: per restituire un libro preso in prestito.
- GET /books/available: per visualizzare la lista dei libri disponibili.
- GET /books/borrowed: per visualizzare la lista dei libri presi in prestito.

## Rappresentazione architetturale```mermaid
flowchart TB
   U([User])

   WA[Web Application]

   US[User Service]
   BS[Book Service]
   LS[Loan Service]

   DB1[(SQL Database)]

   U --> WA 

   WA --> US & BS & LS

   US & BS & LS --> DB1
```