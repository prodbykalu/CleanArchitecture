# Multi-tier architecture

Organizza il software in livello logico e fisico, con ogni livello che si occupa di un aspetto specifico del software.

**Logical separation**: Consente di separare le responsabilità su tutti i livelli

**Physical separation**: Consente ogni livello di essere sviluppato, aggiornato e distribuito indipendentemente dagli altri livelli.

Quando parliamo di multi-tier architecture, intendiamo dire che ogni livello gira su un server diverso, con una separazione fisica tra i livelli.

# Restrizioni
Ogni livello può comunicare con quello adiacente. Non può saltare un livello.

```
┌─────────────────────────────────────────────────────────────┐
│                    Client                                   │
└─────────────────────────────────────────────────────────────┘
                            ↓
                        Request
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                Presentation Layer (Server)                  │
└─────────────────────────────────────────────────────────────┘
                            ↓
                        Request
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                 Business Logic Layer                        │
└─────────────────────────────────────────────────────────────┘
                            ↓
                        Request
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                    Data Access Layer                        │
└─────────────────────────────────────────────────────────────┘
                            ↓
                        Query
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                      Database                               │
└─────────────────────────────────────────────────────────────┘
```

## Three-tier architecture
```
┌─────────────────────────────────────────────────────────────┐
│                    Presentation Tier                        │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                Application Tier                             │  
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                 Data Tier                                   │
└─────────────────────────────────────────────────────────────┘
```
### Presentation Tier
Il livello più alto, che interagisce direttamente con l'utente. Si occupa di presentare i dati all'utente e di raccogliere le sue input.
Non contiene logica di business.

### Application Tier
Il livello intermedio, che contiene la logica di business. Si occupa di elaborare i dati ricevuti dal presentation tier e di interagire con il data tier per recuperare o salvare i dati.

### Data Tier  
Il livello più basso, che si occupa di gestire l'accesso ai dati. Si occupa di interagire con il database per recuperare o salvare i dati.

### Vantaggi
Il vantaggio di questa architettura è che il front end, il presentation layer, si scala da solo in quanto gira nella macchina del client senza problemi.
Mantenendo la nostra applicazione stateles, inserendo un load balancer tra il presentation layer e l'application layer, possiamo scalare l'application layer in modo indipendente, aggiungendo più server per gestire le richieste.
Infine, anche il data tier può essere soggetto a scalabilità, in quanto si può creare un dabase distribuito seguendo quello che abbiamo imparato nei capitoli precedenti.

### Svantaggi
- Struttura monolitica della business logic. CPU alta, molta memoria utilizzata, applicativo poco responsive.
- Sviluppo lento, quando diventa grande. Si può risolvere separando la business logic in sotto moduli, relazionati fra di loro

### Quando usarla
- Codebase piccola e non troppo complessa
- mantenuta da un team piccolo
- per startup all'inizio o progetti stabili che rispettano i requisiti sopra