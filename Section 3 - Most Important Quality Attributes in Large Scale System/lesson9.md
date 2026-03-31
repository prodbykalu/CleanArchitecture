# Scalability
## Traffic patterns
E' ovvio che il traffico non rimane uguale sempre, seguirà diversi pattern, ad esempio:
- **Diurno**: più traffico durante il giorno, meno di notte, per esempio per un sito di notizie.
- **Stagionale**: più traffico in certi periodi dell'anno, come un sito di e-commerce durante le festività.

Se il nostro business sta andando bene, ovviamente il traffico aumenterà, e dobbiamo essere pronti a gestirlo.

## Scalability definition
La scalabilità è la capacità di un sistema di gestire un aumento del carico di lavoro o di essere facilmente ampliato per gestire tale aumento. In altre parole, un sistema scalabile può adattarsi a un aumento del traffico o delle richieste senza degradare le prestazioni.

### Vertical Scalability / Scale Up
Per vertical scalability si intende un aumento delle risorse fisiche a nostra disposizione, necessario per gestire un aumento di traffico che presumibilmente si presenterà. Ad esempio, se abbiamo un server che gestisce 1000 richieste al secondo, e prevediamo un aumento a 2000 richieste al secondo, potremmo decidere di aumentare la potenza del nostro server, ad esempio aggiungendo più CPU o RAM.

### Horizontal Scalability / Scale Out
A differenza della vertical scalability, la horizontal scalability si riferisce alla capacità di aggiungere più macchine o server al nostro sistema per gestire un aumento del traffico. Ad esempio, invece di potenziare un singolo server, potremmo decidere di aggiungere un secondo server che gestisca parte del traffico, e così via. Questo approccio è spesso più flessibile e può essere più efficiente in termini di costi a lungo termine.

### Team scalability
Per scalabilità organizzativa si intende la capacità di un'organizzazione di crescere e adattarsi a un aumento del carico di lavoro o del traffico. Questo può includere l'assunzione di più personale, l'espansione delle infrastrutture, o l'adozione di nuove tecnologie per gestire meglio il carico di lavoro.
Questo è necessario perché, inevitabilmente, con l'aumento di personale si va incontro a diversi problemi, per esempio:
- meeting troppo affollati, partecipati attivamente solo da poche persone, mentre le altre sono solo spettatori passivi, e questo non è efficiente.
- merge conflicts.
- difficoltà nei test

Per aumentare la scalabilità organizzativa, ci sono diverse strategie che possono essere adottate, come ad esempio:
- Dividere il servizio in sottoservizi più piccoli, in modo che ogni team possa concentrarsi su una parte specifica del sistema.
- dividere la propria codebase in sotto servizi.
