# Load Balancer
## Definizione
Controlla il traffico tra i vari server che abbiamo a disposizione.
La maggior parte dei load balancer possiede un livello di astrazione, denominato Single Server Abstraction, che permette al client di interagire con un singolo server, anche se in realtà ci sono più server dietro al load balancer. In questo modo, il client non deve preoccuparsi di quale server stia gestendo la richiesta, e il load balancer si occupa di distribuire le richieste in modo equo tra i vari server.

## Qualità
- Scalabilità: permette di aggiungere o rimuovere server in modo dinamico, senza dover modificare il client.
- Affidabilità: se un server si guasta, il load balancer può reindirizzare le richieste agli altri server disponibili, garantendo la continuità del servizio.
- Performance: distribuisce le richieste in modo equo tra i vari server, evitando che un server si sovraccarichi e garantendo una migliore performance complessiva del sistema.
- Manutenibilità: semplifica la gestione dei server, in quanto il load balancer si occupa di monitorare lo stato dei server e di reindirizzare le richieste in caso di guasti.

## Tipi di Load Balancer
- DNS Load Balancer: utilizza il sistema DNS per distribuire le richieste tra i vari server. Solitamente, il DNS risponde alla richiesta del client con l'indirizzo IP legato al server. Tuttavia, il DNS può anche rispondere con una lista di IP che il client può contattare. 
   - Vantaggi: 
      1. semplice da implementare, non richiede hardware dedicato. 
      2. non troppo costoso 
   - Svantaggi:
      1. Non monitora lo stato dei server
      2. Il bilanciamento è un semplice round-robin, senza considerare il carico dei server
      3. Fornisce al client una lista di IP, esponendo così i server al client, il che può essere un problema di sicurezza.

- Hardware Load Balancer: programma che gira in un dispositivo dedicato al load balancing

- Software Load Balancer: programma che gira su un computer generico e controlla il traffico tramite un software.

In entrambi questi casi, è il load balancer che chiama i server per conto del client.

- Gloabal Server Load Balancer: è un misto tra DNS e Hardware/Software Load Balancer. Utilizza il DNS per distribuire le richieste tra i vari load balancer, che a loro volta distribuiscono le richieste ai server. In questo modo, è possibile distribuire le richieste tra più data center, garantendo una maggiore scalabilità e affidabilità.

## ESEMPI
NGINX