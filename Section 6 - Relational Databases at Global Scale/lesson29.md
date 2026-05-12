# Techniques to improve performance, availability, and scalability of databases

## Database indexing
Il compito principale dell'indexing è quello di velocizzare il recupero di dati da una tabella. Senza gli indici, recuperare tali dati potrebbe richiedere una scansione completa della tabella, impiegando quindi un tempo maggiore rispetto a quello impiegato dall'indice. 
Questo implica quindi un rallentamento del nostro database e quindi un peggioramento delle prestazioni notabile dal nostro utente.

Un indice è una struttura dati che contiene una copia ordinata di una o più colonne di una tabella, insieme a un puntatore alla posizione dei dati originali. La maggior parte dei database relazionali (MySQL, PostgreSQL, ecc.) implementa gli indici tramite strutture **B-tree** o **B+ tree**, che mantengono i dati ordinati e consentono ricerche, range queries e ordinamenti efficienti. Esistono anche indici di tipo hash, ma sono meno comuni e non supportano le range queries.

Gli indici si possono usare anche su più colonne, in questo caso si parla di indici composti. Questi indici sono utili quando si eseguono query che coinvolgono più colonne, in quanto possono migliorare le prestazioni di tali query.

## Database replication
Come è avvenuto per i server, che vengono moltiplicati a seconda del carico e, poi, vengono gestiti da un load balancer, anche i database possono essere replicati. La replica del database è il processo di creazione di copie di un database su più server. Questo può migliorare le prestazioni, la disponibilità e la scalabilità del database.
NB: per fare un database distribuito, bisogna avere le giuste competenze, in quanto è complesso da configurare, gestire e progettare correttamente.

## Database partitioning
Per database partitioning si intende la suddivisione di una tabella in più parti, chiamate partizioni. Ogni partizione contiene un sottoinsieme dei dati della tabella originale. Questo può migliorare le prestazioni, la disponibilità e la scalabilità del database, in quanto consente di distribuire i dati su più server e di eseguire query più efficienti su ciascuna partizione, anche in parallelo.

E' necessario un routing per indirizzare le query.

Normalmente queste 3 tecniche vengono usate insieme.