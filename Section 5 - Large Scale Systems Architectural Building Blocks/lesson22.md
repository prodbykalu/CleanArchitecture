# API Gateway
Esempio di servizio in cui si usa un API Gateway: **Youtube**

Avere un solo servizio che si occupa di mostrare i video, i commenti, le notifiche, etc. è difficile e soggetto a grossi problemi.
Pertanto, dividere il servizio in più microservizi è un'ottima idea. Ma questo porta con se dei problemi: come fa il client a sapere dove sono i microservizi? Come fa a comunicare con loro? Come fa a gestire l'autenticazione? Ecco perché nasce l'API Gateway, un servizio che si occupa di fare da intermediario tra il client e i microservizi.

Nell'API Gateway definiamo tutte le API che il client può chiamare, e l'API Gateway si occupa di chiamare i microservizi necessari per soddisfare la richiesta del client. In questo modo, il client non deve preoccuparsi di dove sono i microservizi, come comunicare con loro, etc. L'API Gateway si occupa di tutto questo.

## Benefici dell'API Gateway
- **Semplifica il client**: il client deve comunicare solo con l'API Gateway, e non con tutti i microservizi.
- **Gestisce l'autenticazione**: l'API Gateway si occupa di gestire l'autenticazione
- **Gestisce la sicurezza**: l'API Gateway si occupa di gestire la sicurezza
- **Sfrutta il caching**: l'API Gateway può sfruttare il caching per migliorare le prestazioni
- **Monitora e alert**: l'API Gateway può monitorare le richieste e generare alert in caso di problemi

## Antipattern
- **Non deve contenere logica di business**. Si occupa solo di fare da router tra il client e i microservizi. Se contiene logica di business, diventa un punto critico di fallimento con troppo codice, un monolite, che era il problema che si voleva risolvere all'inizio.
- **Non deve diventare un single point of failure**. Se l'API Gateway va down, tutto il sistema va down. Pertanto, è importante avere più istanze dell'API Gateway e un bilanciatore di carico per distribuire le richieste tra le istanze. Questo si risolvere usando un load balancer e più istanze dell'API Gateway.
- **Non va bypassato per servizi esterni**

## Esempi di API Gateway
- AWS API Gateway
- Zuul