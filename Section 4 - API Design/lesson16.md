# REST API

## What is REST API?
La REST API è uno stile architetturale per disegnare API che sono semplici da usare e scalabili.

In confronto alla RPC, che utilizza dei metodi esposti verso il cliente e che vengono organizzati in delle interfacce (IDL), la REST API utilizza le risorse, che sono rappresentate da URL, e i metodi HTTP (GET, POST, PUT, DELETE) per operare su queste risorse.

Principale differenze quindi:
- RPC si basa su metodi
- REST si basa su risorse.

Il protocollo che viene utilizzato per le REST API è HTTP.

## Quality attributes

### Stateless
- il server è stateless, non tiene traccia dello stato del client
- ogni richiesta al server deve occuparsi solo di quella, senza dipendere da quelle precedenti
- è possibile scalare orizzontalmente, aggiungendo più server per gestire le richieste (essendo stateless)

### Cacheable
Il server può indicare se una risposta è cacheable o no, in modo che il client possa decidere se memorizzarla o meno. Questo può migliorare le prestazioni, evitando di dover fare richieste al server per ogni operazione. La cache può essere presente sia lato client (browser), sia in mezzo a client e server (nel proxy), sia lato server (es. Redis).

## Resources
Ogni risorsa è nominata tramite un URI. Può essere semplice o  complessa, e presenta una gerarchia.
Una risorsa (/users) può rappresentare una collezione di utenti, mentre una risorsa più specifica (/users/123) rappresenta un singolo utente.

## REST API Operations
Operazioni predefinite:
- Create: POST 
- Read: GET
- Update: PUT
- Delete: DELETE