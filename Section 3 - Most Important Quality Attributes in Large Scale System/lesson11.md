# Fault tolerance and High availability
La prima fonte di errore è l'errore umano. Questo può inserire all'interno del codice dei bug, può lanciare lo script errato, una parte di codice non correttamente testata.

Altri errori possono essere errori di software, come garbage collectors troppo grandi

Infine, anche quelli hardware, come un disco che si rompe, un cavo di rete che si stacca, o un interruttore che si guasta.

Per supportare il cosidetto fault tolerance, è necessario progettare il sistema in modo che possa continuare a funzionare anche in presenza di errori.

La **fault tolerance** gira intorno a 3 tecniche principali:
- **fault prevention**: eliminare tutti i single point of failure, come ad esempio avere più server, più dischi, più cavi di rete, più interruttori, in modo che se uno di questi si guasta, il sistema possa continuare a funzionare.
- **fault detection and isolation**: per poter rilevare e isolare i guasti è necessario monitorare il sistema, in modo da poter rilevare quando un componente si guasta e isolare il guasto.
- **fault recovery**: dopo aver rilevato e isolato il nodo non funzionante, la parte di recovery si occupa di non mandare più richieste a quel nodo, fare un restart, fare rollback.

## Strategie per redundancy e replication
- **Active-active**: tutti i nodi sono attivi e possono gestire le richieste. Se un nodo si guasta, gli altri nodi possono continuare a gestire le richieste senza interruzioni. I nodi sono sincronizzati tra loro, in modo che i dati siano sempre aggiornati su tutti i nodi.
- **Active-passive**: solo un nodo è attivo e gestisce le richieste, mentre le altre repliche si sincronizzano con la principale facendo ogni tot tempo uno snapshot dello stato attuale del nodo principale.