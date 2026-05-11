# Event Driven Architecture
Definizione di evento: un evento è uno statement immutabile che è avvenuto un cambiamento. Per esempio, un utente ha cliccato un ad, è stato aggiunto un prodotto al carrello.

Due protagonisti:
- **Event Producer**: è colui che genera l'evento. Può essere un'applicazione, un servizio o un componente che rileva un cambiamento e lo rappresenta come un evento.
- **Event Consumer**: è colui che riceve e processa l'evento. Può essere un'applicazione, un servizio o un componente che si iscrive a determinati eventi e reagisce di conseguenza.

Tra i due, c'è un **Event Broker** che funge da intermediario, facilitando la comunicazione tra i produttori e i consumatori di eventi. L'Event Broker riceve gli eventi dai produttori e li distribuisce ai consumatori interessati.