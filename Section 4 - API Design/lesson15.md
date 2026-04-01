# Remote Procedure Call (RPC)
## How it works
Sostanzialmente, il client è in grado di fare una chiamata a una subroutine presente in un server, che successivamente restituisce un risultato al client.
La cosa bella è che questo avviene come se fosse una normale funzione locale.
Inoltre, RPC supporta diversi linguaggio di programmazione.

La API RPC e i data type usati da tale API sono definiti in un file chiamato **Interface Definition Language (IDL)**.
Avendo questa IDL, possiamo generare due parti di codice separate: una per il client e una per il server.
La parte nel server si chiama **server stub**, mentre quella nel client si chiama **client stub**.
Gli oggetti generati automaticamente dagli stub (a partire dall'IDL) rappresentano i tipi di messaggio scambiati tra client e server. Sono concettualmente simili ai DTO (Data Transfer Object), ma vengono più precisamente chiamati **generated message types** (o message classes), e vengono inseriti nella parte di codice compilata.
Simulazione di una chiamata RPC:
Client -> Client Stub -> Marshalling -> Transport Layer -> Demarshalling -> Server Stub -> Server

Dopo che il server fa le sue operazione, abbiamo la risposta che torna indietro:
Server -> Server Stub -> Marshalling -> Transport Layer -> Demarshalling -> Client Stub -> Client

## Benefits
- Gli sviluppatori del client possono comunicare con il server facendo una chiamata alle funzioni senza troppe preoccupazioni, in quanto lavorano alla stessa maniera di una normale funzione locale.
- La comunicazione e i data type sono definiti in un file IDL, che è indipendente dal linguaggio di programmazione usato.
- Gli errori o i problemi vengono segnalati in modo chiaro e rispettando il linguaggio di programmazione usato dal client.

## Drawbacks
A differenza dei metodi locali, le chiamate RPC sono più lente, in quanto devono essere serializzate, inviate attraverso la rete e deserializzate. La latenza di rete e il costo di serializzazione rimangono intrinseci al protocollo. Per mitigare l'impatto sul chiamante, è possibile usare metodi asincroni: non riducono la latenza, ma evitano di bloccare il client durante l'attesa della risposta del server.

Per evitare che ci siano problemi di chiarezza tra client e server, ovvero che non si sa se l'operazione sia andata a buon fine o meno, è necessario creare il più possibile delle operazioni idempotenti, ovvero che se vengono eseguito più volte, il risultato non cambia. In questo modo, se il client non riceve una risposta dal server, può semplicemente ripetere la chiamata senza preoccuparsi di eventuali effetti collaterali.

## Quando usare RPC?
- Comunicazione tra due sistemi backend
- API fornita a una company diversa, invece che un utente finale
- Comunicazione tra due diversi componenti di un sistema, ad esempio tra due microservizi
