# Message broker
E' un software architetturale che usa una queue per mantenere messaggi che si trovano tra il mittente e il destinatario. Il mittente invia un messaggio al message broker, che lo mette in una queue. Il destinatario legge i messaggi dalla queue e li elabora.
Questo evita il problema della sincronia tra mittente e destinatario, in quanto il mittente può inviare un messaggio al message broker anche se il destinatario non è disponibile in quel momento. Il message broker si occupa di mantenere i messaggi nella queue fino a quando il destinatario non è pronto per leggerli.

## Esempio Online Store
- Prima del message broker
   client -> load balancer -> Frontend Service -> Fulfilment Service
   In questo caso, se il Fulfilment Service è lento o non disponibile, il Frontend Service si blocca e non può rispondere alle richieste dei clienti.

- Dopo l'introduzione del message broker

   client -> load balancer -> Frontend Service -> message broker -> Fulfilment Service
   Ancora più comodo sarebbe suddividere il Fulfilment Service in più servizi, ad esempio:

   Reservation Service -> Billing Service -> Email Service
   Tutti con un message broker in mezzo.

## Esempi di message broker
RabbitMQ, Apache Kafka