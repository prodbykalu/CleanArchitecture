# Hopping window
Simile alla tumbling window.
Invece che avere le window che si susseguono, le hopping window si sovrappongono. 
Sono separate da un fix hop chiamato advance interval, che può essere più piccolo della window duration, uguale (e in questo caso si comporta come una tumbling window) o più grande.

## Esempi ASCII

### Advance interval < Window duration (overlapping windows)
```
Events:    E1  E2  E3  E4  E5  E6  E7  E8
Timeline:  |---|---|---|---|---|---|---|---|
           0   1   2   3   4   5   6   7   8

Window duration: 4, Advance interval: 2

Window 1:  [0-4)      |E1|E2|E3|E4|
Window 2:      [2-6)      |E3|E4|E5|E6|
Window 3:          [4-8)      |E5|E6|E7|E8|
```

### Advance interval == Window duration (tumbling windows)
```
Events:    E1  E2  E3  E4  E5  E6  E7  E8
Timeline:  |---|---|---|---|---|---|---|---|
           0   1   2   3   4   5   6   7   8

Window duration: 4, Advance interval: 4

Window 1:  [0-4)  |E1|E2|E3|E4|
Window 2:         [4-8)  |E5|E6|E7|E8|
```

### Advance interval > Window duration (gaps between windows)
```
Events:    E1  E2  E3  E4  E5  E6  E7  E8
Timeline:  |---|---|---|---|---|---|---|---|
           0   1   2   3   4   5   6   7   8

Window duration: 2, Advance interval: 3

Window 1:  [0-2)  |E1|E2|
Window 2:         [3-5)     |E4|E5|
Window 3:              [6-8)       |E7|E8|
```

La hopping window è utile soprattutto quando usiamo la overlapping windows, che consente di avere un discreto vantaggio tra una finestra e l'altra, ma anche tra la fine di una finestra e l'altra, rendendo così più veloce e coerente l'elaborazione dei dati.
Viene spesso utilizzata per le app di stock exchange, ma anche Error Logs, Web Analytics, ecc. perché fornisce continuamente un aggiornamento.