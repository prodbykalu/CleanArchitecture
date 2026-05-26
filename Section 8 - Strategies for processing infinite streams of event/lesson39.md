# Sliding Window
Prendiamo per esempio un servizio di fraud detection.
Se per esempio un utente effettua 10 transazioni in un minuto, è probabile che stia commettendo una frode.
Se usiamo la tumbling window, potremmo perdere alcune di queste transazioni, perché potrebbero essere distribuite su due finestre diverse, non rilevando così la frode.

### Tumbling Window (non rileva la frode)
```
Timeline:    00:00  00:30  01:00  01:30  02:00
             |      |      |      |      |
Transazioni: T1 T2 T3|T4 T5 T6|T7 T8 T9|T10

Finestra 1:  [=========] 6 transazioni
Finestra 2:             [=========] 4 transazioni

Risultato: Non vede i 10 eventi concentrati!
```

Se usiamo invece la hopping window, possiamo essere fortunati e rilevare la frode, ma ci sono anche casi in cui i 10 eventi possono essere separati: un po' prima e un po' dopo la finestra, e quindi la frode non viene rilevata.

### Hopping Window (può non rilevare la frode)
```
Timeline:      00:00      00:20      00:40      01:00
               |          |          |          |
Transazioni:   T1 T2 T3 T4 T5 T6     |          T7 T8 T9 T10
               [6 eventi]            [4 eventi]

Finestra 1:    [==== 30 sec ====]    6 transazioni
               (00:00 - 00:30)

Finestra 2:                  [==== 30 sec ====]   5 transazioni
                             (00:20 - 00:50)      (T4, T5, T6, T7, T8)

Finestra 3:                           [==== 30 sec ====]  4 transazioni
                                      (00:40 - 01:10)    (T7, T8, T9, T10)

Risultato: Nessuna finestra vede i 10 eventi insieme!
           La frode non viene rilevata perché gli eventi sono troppo distribuiti.
```

Questo può essere risolto riducendo l'advance interval, ma questo comporta un aumento del numero di finestre da elaborare, aumentando così il carico computazionale, soprattutto di notte, quando ci sono meno eventi.

Per questo motivo, esiste la sliding window.

### Sliding Window (rileva la frode)
Abbiamo un windows size di 30 secondi, che si apre ogni volta che arriva un evento, quindi ogni evento apre una nuova finestra di 30 secondi.
L'advance interval risulta quindi dinamico, e dipende dagli eventi che arrivano.
Ottimo per quando arrivano degli eventi in modo irregolare.