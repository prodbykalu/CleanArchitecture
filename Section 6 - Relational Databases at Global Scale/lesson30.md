# Brewer's (CAP) Theorem
Quando è presente una network partition, un database distribuito può scegliere solo di essere o disponibile o consistente, mai entrambi.

Questo teorema NON si applica ai database che non contengo una network partition, in quanto comunque questi si aggiornano a vicenda.

ESEMPIO:
|-----|     |-----| Questi due database si possono aggiornare a vicenda, quindi non c'è una network partition.
| DB1 |     | DB2 |
|     |     |     |
| C=1 |     | C=1 |
|-----|     |-----|

--------------NETWORK PARTITION-----------------
|-----|
| DB3 | Questo database è isolato dagli altri, quindi c'è una network partition e il valore di C non potrà essere aggiornato.
|     | Se un servizio fa richiesta a questo db, abbiamo due scelte:
| C=9 | - Rendere il servizio non disponibile, scegliendo quindi la consistenza e non tornando un risultato errato (consistency)
|-----| - Rendere il servizio disponibile, scegliendo quindi la disponibilità e tornando un risultato errato. (availability)

# CAP Definitions

## Consistency
Tutti i db, al momento di una richiesta read da un servizio, ritornano o il valore più recente oppure un errore.

## Availability
Ogni richiesta da un servizio riceve una risposta, anche se non è il valore più recente.

## Partition Tolerance
Il sistema continua a lavorare anche se ci sono state delle perdite di dati o messaggi tra i nodi.

# Scelte obbligatorie
CA - No partition tolerance. 
   In questo caso si usa un database centralizzato. Se scegliamo di usare un database distribuito, è inevitabile che ci sia una network partition, quindi questa scelta non è possibile.
CP - No availability
   In questo caso, scegliamo di perdere la disponibilità. Un esempio può essere uno store online, dove se due client fanno una richiesta di acquisto dello stesso prodotto, è meglio che uno dei due riceva un messaggio di errore se tale prodotto è esaurito, piuttosto che entrambi ricevano un messaggio di successo e poi scoprire che il prodotto è esaurito.
AP - No consistency
   In questo caso, scegliamo di perdere la consistenza. Un esempio può essere un social network, dove se due utenti fanno una richiesta di aggiornamento dello stesso post, è meglio che entrambi ricevano un messaggio di successo e poi scoprire che il post è stato aggiornato in modo errato, piuttosto che uno dei due riceva un messaggio di errore.