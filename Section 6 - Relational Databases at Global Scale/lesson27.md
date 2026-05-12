# Non-relational databases
Nascono dal bisogno di non mantenere in relazione i dati.

## Differenze tra relational e non-relational databases
### Struttura dei dati
Nei database relazionali, se voglio aggiungere una colonna solo per un record (es: Secondo Nome), devo aggiungere la colonna a tutta la tabella, anche se non è necessaria per tutti i record. Nei database non relazionali, invece, posso aggiungere un campo solo per quel record specifico, senza doverlo aggiungere a tutta la tabella.

### Supporto verso i linguaggi di programmazione
Nei database relazionali, si utilizzano le tabelle. Questa struttura dei dati non si mappa nativamente agli oggetti dei linguaggi di programmazione: sebbene esistano strutture come array di oggetti o DataFrame, è necessario un passaggio di conversione (spesso gestito da un ORM) per trasformare le righe in oggetti.
Nei database non relazionali, invece, si utilizzano documenti, che sono conformi ai linguaggi di programmazione, in quanto rappresentano un oggetto con campi e valori. Questo elimina la necessità di un ORM.

### Velocità
Nei database relazionali, le query sono più lente, in quanto devono eseguire join tra le tabelle per recuperare i dati. Nei database non relazionali, invece, le query sono più veloci, in quanto i dati sono memorizzati in un unico documento, eliminando la necessità di join.

## 3 tipologie di database non relazionali
- **Key-value store**: memorizzano i dati come coppie chiave-valore. Esempi: Redis, DynamoDB.
- **Document store**: memorizzano i dati come documenti, che sono oggetti con campi e valori. Esempi: MongoDB, CouchDB.
- **Graph database**: memorizzano i dati come nodi e relazioni tra di essi. Esempi: Neo4j, Amazon Neptune.

## Quando usare un database non relazionale
Quando voglio più velocità e quando vogliamo usare la cache.
Quando devo gestire dei big data in real time
Quando i dati non sono strutturati, o sono semi-strutturati, e non si adattano bene a una struttura tabellare.
Quando i record possono contenere differenti campi, e non voglio dover aggiungere campi inutili a tutta la tabella.
ES: 
- user profiles
- content management systems
- real-time analytics