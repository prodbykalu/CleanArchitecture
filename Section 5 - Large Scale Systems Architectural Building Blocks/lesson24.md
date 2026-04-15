# Content Delivery Network (CDN)
Sono dei network distribuiti globalmente, localizzati in diverse regioni strategiche, con il compito principale di fornire i contenuti richiesti dagli utenti in modo rapido ed efficiente.

## Come funziona una CDN
Fornisce un servizio utilizzando una cach del contenuto del nostro server, in modo che quando un utente richiede un contenuto, la CDN lo fornisce direttamente dalla cache più vicina a lui, riducendo così la latenza e migliorando le prestazioni. I server usati dalla CDN sono chiamati edge server, e sono distribuiti in tutto il mondo. Quando un utente richiede un contenuto, la CDN lo fornisce direttamente dall'edge server più vicino a lui.

## Content publishing strategies
- **Pull strategy**: dobbiamo dire al CDN provider cosa mantenere e quante volte la cache deve essere aggiornata. Possiamo fare ciò settando un Time To Live (TTL) per ogni contenuto, che indica per quanto tempo il contenuto deve essere mantenuto nella cache prima di essere aggiornato. Se il TTL è scaduto, la CDN richiede nuovamente il contenuto al server di origine e aggiorna la cache.
- **Push strategy**: in questo caso, è il server di origine che decide quando aggiornare la cache della CDN. Il server di origine invia una richiesta alla CDN per aggiornare la cache ogni volta che il contenuto viene modificato.