# Batch processing model
Lo stream di dati che la nostra applicazione riceve viene memorizzata o all'interno di un database oppure in un file system distribuito. 
Non processiamo ogni dato che ci arriva singolarmente, ma aspettiamo di accumularne una certa quantità, o di raggiungere un certo intervallo di tempo, prima di eseguire l'elaborazione. 
Questo intervallo viene chiamato batch.
Può essere utilizzato per i social o per i siti di istruzione, aiutando l'app stessa a poter consigliare contenuti pertinenti agli utenti. Stessa cosa vale per i social media.
## Vantaggi
- Semplice da implementare
- High availability
- Efficienza.
- Fault tolerance più alta.
## Svantaggi
- Non adatto per applicazioni che richiedono risposte in tempo reale.


# Real time processing model
Ogni evento viene inserito in una queue o message broker, passa poi in uno stream processor, che lo elabora e lo memorizza in un database o file system distribuito.

## Vantaggi
- Adatto per applicazioni che richiedono risposte in tempo reale.

## Svantaggi
- Più complesso da implementare ed è complicato fare analisi complesse sui dati in tempo reale.
- Impossibile fare data fusion