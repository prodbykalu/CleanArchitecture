# Processo base per la progettazione dell'architettura software
Per poter creare in maniera corretta un'architettura software, è necessario seguire alcuni passaggi fondamentali.
Domande:
- Quali sono i requisiti funzionali del sistema?
- Quali sono i requisiti non funzionali del sistema?
- Quali sono i vincoli del sistema?

- Definisci le API del sistema

- Progetta l'architettura del sistema che rispetti i requisiti funzionali
- Fai un refactoring dell'architettura per rispettare i requisiti non funzionali.

## Esercizio 1 - Highly Scalable Public Discussion Forum (like Reddit)
### Funzionalità richieste:
- Gli utenti possono creare un account
- Gli utenti possono creare post
- Gli utenti possono commentare i post
- Gli utenti possono votare i post e i commenti
- Feed per post popolari e recenti

### Domande:
- Chiunque può postare o vedere i commenti?
- Cosa può contenere un post? Solo testo o anche immagini/video?
- Cosa si intende per post popolari?
- Come è strutturata la sezione dei commenti? È una struttura ad albero o una lista piatta?

### Requisiti funzionali:
- Gli utenti devono poter creare un account e autenticarsi per poter creare post, commentare e votare.
- Un utente deve poter creare un nuovo post e contenere un titolo, un corpo e dei tag.
- Un utente deve poter commentare un post.
- I commenti devono essere ordinati in maniera cronologica secondo una lista piatta.
- Un utente può cancellare i propri post e commenti.
- Un utente può votare un post o un commento una sola volta.
- Devono essere mostrati i post più popolari delle utlime 24 ore nella hompage. (Per popolarità si intende il numero di voti positivi meno i voti negativi)

### Requisiti non funzionali:
- Scalabilità
- Performance (meno di 500ms di latenza per ogni richiesta)
- Fault Tolerance / Disponibilità (99.9%)
- Availability + Partition Tolerance (AP over CP)
- Durability

### API Definition:
REST API in quanto è una tipica web app.
4 step:
- identifica le entità
- mappa le entità sui relativi URI
- definisci la rappresentazione delle risorse 
- assegna i metodi HTTP alle risorse

#### Mapping delle entità sui relativi URI:
- /users
- /users/{userId}

- /posts
- /posts/{postId}

- /posts/{postId}/comments
- /posts/{postId}/comments/{commentId}

- /posts/{postId}/images
- /posts/{postId}/images/{imageId}

- /posts/{postId}/votes
- /posts/{postId}/comments/{commentId}/votes

#### Definizione della rappresentazione delle risorse:
- GET /posts/{postId} -> 200 OK + JSON body con i dettagli del post
- GET /posts/{postId}/comments/{commentId} -> 200 OK + JSON body con i dettagli del commento

#### Assegnazione dei metodi HTTP alle risorse:
POST /users/create per creare un nuovo account
POST /users/login per autenticarsi (si usa POST perché si inviano le credenziali nel body della richiesta. Si può vedere anche una creazione di un nuovo token)

POST /posts per creare un nuovo post
GET /posts per ottenere la lista dei post
GET /posts/{postId} per ottenere i dettagli di un post specifico
DELETE /posts/{postId} per cancellare un post

POST /posts/{postId}/comments per creare un nuovo commento
GET /posts/{postId}/comments per ottenere la lista dei commenti di un post
DELETE /posts/{postId}/comments/{commentId} per cancellare un commento

POST /posts/{postId}/vote per votare un post
POST /posts/{postId}/comments/{commentId}/vote per votare un commento

POST /posts/{postId}/images per caricare un'immagine per un post
GET /posts/{postId}/images/{imageId} per ottenere i dettagli di un'immagine specifica di un post

Nella home mostriamo solo i primi 20 post più popolari delle ultime 24 ore, quindi possiamo avere un endpoint dedicato per questo:
GET /posts?limit=20&offset=0
Stessa cosa vale per i commenti.