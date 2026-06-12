# Design Problem: Building a Scalable E-commerce Platform (like Amazon)

Sempre il solito processo step by step:
- ottieni i requisiti, funzionali e non funzionali
- Definisci le API di sistema
- Fai un diagramma ad alto livello per i requisiti funzionali
- Fai un diagramma ad alto livello per i requisiti non funzionali

## Ottieni i requisiti, funzionali e non funzionali
2 soggetti:
- **Merchant**: Vende prodotti sulla piattaforma.
- **Customer**: Acquista prodotti sulla piattaforma.

### Merchant
- Che tipo di prodotti vende? Fisici o digitali? Entrambi?
- Che informazioni fornisce per ogni prodotto? (es. nome, descrizione, prezzo, immagini)
- Che dati dobbiamo fornire riguardo al merchant?
- Che operazioni può fare il merchant? (es. aggiungere, modificare, rimuovere prodotti)

### Customer
- Chiunque può accedere al sito o solo chi è registrato?
- Può fare dei rating/recensioni sui prodotti?
- Che cosa può cercare?
- Dobbiamo gestire l'aggiunta al carrello, il pagamento e la gestione degli ordini?
- Che UI offriamo? Solo web o anche mobile?

### Requisiti funzionali
- **Prodotti**: vendiamo prodotti fisici. Ogni prodotto ha un nome, una descrizione, categorie, immagini, attributi opzionali.
- **Merchant**: forniamo un product management system (PMS) per i merchant, che consente loro accedere al sito, di aggiungere, modificare e rimuovere prodotti. Inoltre, nella dashboard del merchant, forniamo statistiche sulle vendite e sui prodotti.
- **Customer**: nello storefront (che può essere sia web che mobile), i clienti possono cercare prodotti, visualizzare i dettagli dei prodotti, aggiungere prodotti al carrello, effettuare il checkout. Non è necessario gestire la registrazione degli utenti o le recensioni dei prodotti. Per il checkout, l'utente può accedervi, guardare quanto ammonta il pagamento compreso di tasse. Può completare l'ordine fornendo i dati di pagamento e spedizione. Dopo il checkout, l'utente può visualizzare lo stato dell'ordine tramite mail o notifiche push. Non dobbiamo occparci del shopping cart, del processo di pagamento o della gestione degli ordini.

### Requisiti non funzionali
#### Merchants
- Scalabilità: ci si aspettano sui 100 merchants, traffico basso, 1k di prodotti.
- Performance: response time di 1 secondo al 50esimo percentile
- Consistency vs Availability: CP
- High availability: 99.5% uptime

#### Customers
- Scalabilità: 10-100 milion di utenti giornalieri, servizio disponibile in più stati, trafffico elevato nei momenti di punta (es. Black Friday)
- Performance: 
   product response time di 200ms al 50esimo percentile, sotto 500ms al 99esimo percentile
   checkout response time di 1 secondo al 99esimo percentile
- Consistency vs Availability: 
   Storefront: AP
   Checkout: CP
- High availability: 99.99% uptime