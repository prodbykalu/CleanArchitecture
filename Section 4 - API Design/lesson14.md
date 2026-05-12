# Introduction to API

L'API la possiamo immaginare come una black box, che ha un comportamento e un'interfaccia ben definita.

Questa interfaccia è un contratto stipulato tra gli ingegneri che la programmano e i clienti che utilizzano tale sistema. Per questo motivo, questa interfaccia viene chiamata API, Application Programming Interface.

# Categories of API

## Public API
Sono API che vengono esposte al pubblico, che può chiamare il nostro servizio a proprio piacimento. Una delle best practice è quella di far fare il login o la registrazione da parte del cliente, in modo che possa essere tracciato e monitorato. In questo modo, se un cliente abusa del servizio, possiamo bloccarlo.

## Private API
Sono delle API che vengono utilizzate all'interno dell'azienda, per far comunicare i vari servizi tra di loro. Queste API non sono esposte al pubblico, ma sono utilizzate solo dai nostri servizi interni.

## Partner API
Sono simili alle Public API, ma sono esposte solo a partner selezionati. Queste API sono utilizzate per far comunicare i nostri servizi con quelli dei nostri partner, in modo da offrire un servizio migliore ai nostri clienti.

## Regole per una buona API
### Complete encapsulation
La API deve essere completamente incapsulata, senza che i clienti possano avere accesso alla logica interna e che non decidano mai di chiedere informazioni su come questa sia implementata. Inoltre, questo rende possibile modificare l'implementazione interna senza dover avvisare i clienti, purché l'interfaccia rimanga invariata.

### Facile, chiara, intuitiva
Non deve avere dei nomi strani.
Facile da capire.
Rispetta un determinato metodo di naming, in modo che se passo da una API all'altra so già cosa mi aspetta, a livello macro.

### Operazioni idempotenti
Un'operazione è idempotente se, indipendentemente da quante volte viene eseguita, il risultato è sempre lo stesso. Questo previene la possibilità che, se il nostro cliente manda una richiesta e questa viene persa all'interno dei canali di internet per qualsivoglia motivo, il cliente possa ritentare la richiesta senza preoccuparsi di eventuali effetti collaterali.

### Asynchronous
Le API possono essere progettate in modo sincrono o asincrono a seconda del caso d'uso. Le REST API HTTP sono sincrone per natura: il client invia una richiesta e attende la risposta. Tuttavia, il client può gestire le chiamate in modo asincrono (es. tramite `async/await` o callbacks) per non bloccare l'esecuzione. Esistono anche API nativamente asincrone (es. webhooks, message-based API) che notificano il client al termine dell'elaborazione, utili quando le operazioni richiedono molto tempo.

### Versioning
Le API vanno versionate in modo che, nel momento in cui si vuole modificare l'API, si possa creare una nuova versione senza dover modificare la vecchia. 