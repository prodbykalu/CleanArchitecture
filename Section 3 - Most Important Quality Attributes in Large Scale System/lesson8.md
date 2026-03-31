# Questi sono gli attributi più importanti per un sistema di larga scala:

## Performance

### Response Time
Tempo tra la richiesta fatta dal client e la risposta ricevuta dal server.

$\text{Response Time} = \text{Processing Time} + \text{Waiting Time}$

$\text{Processing Time}$ è il tempo necessario al server per elaborare la richiesta.

$\text{Waiting Time}$ è il tempo trascorso in attesa prima che il server inizi a elaborare la richiesta. E' il tempo che la richiesta trascorre in coda, in attesa di essere elaborata.
Questa variabile può essere chiamata anche latency.

$\text{Response Time}$ è invece rinominata anche End-to-End Latency.
E' molto importante per l'utenza e i tempi di risposta che questa si aspetta.

### Throughput
E' la quantità di lavoro che un sistema può gestire in un dato periodo di tempo. Ad esempio, il numero di richieste che un server può gestire al secondo.

### Important considerations

#### Distribuzione di Response Time

Avendo un sistema di server che si occupano di gestire le richieste, è importante considerare la distribuzione dei tempi di risposta. Se la maggior parte delle richieste viene gestita rapidamente, ma alcune richiedono molto tempo, potrebbe essere necessario ottimizzare il sistema per gestire meglio queste richieste più lente. 
Sistemando queste informazioni in un grafico, possiamo anche creare e capire il percentile di risposta, che ci dice quanto tempo impiega il sistema a rispondere al 90% delle richieste, al 95%, e così via. Questo è importante per capire l'esperienza dell'utente, poiché anche se la media dei tempi di risposta è bassa, se il 10% delle richieste impiega molto tempo, potrebbe causare frustrazione agli utenti.
Nel grafico, è presente anche la parte di "tail", che rappresenta le richieste che impiegano molto tempo a essere gestite. Ottimizzare questa parte è cruciale per migliorare l'esperienza dell'utente.