# Microservices Architecture Pattern
Seguendo questo pattern, dividiamo la nostra business logic monolitica in più microservizi, ognuno dei quali viene gestito da un piccolo team diverso e viene rilasciato in modo indipendente dagli altri. Ogni microservizio è responsabile di una specifica funzionalità del sistema e comunica con gli altri microservizi tramite API.

## Vantaggi
Codice che carica più velocemente nella IDE.
Lo sviluppo diventa più veloce e facile.
Fare la build e i test è facile e veloce.

## Considerazioni 
Tutti questi vantaggi non vengono subito, bisogna stare attenti a non cadere nell'anti pattern della big ball of mud, dove si ha un'architettura disordinata e difficile da mantenere. 
Inoltre, i microservizi vengono con un alto livello di overhead e sfide.

Per evitare ciò, dobbiamo progettare il nostro progetto in modo che:
- ogni variazione avvenga solo in un unico servizio
- non coinvolge più team

Single Responsibility Principle: ogni servizio deve avere una sola responsabilità, e questa responsabilità deve essere completamente incapsulata dal servizio.

Separazione dei database: ogni servizio deve avere il proprio database, in modo da evitare dipendenze tra i servizi e garantire l'indipendenza dei dati.