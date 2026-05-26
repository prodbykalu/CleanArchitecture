# Lambda architecture
Esistono casi in cui il batch processing e il real time devono coesistere per poter rendere utile un servizio: per esempio, il log system analyzer, che deve mantenere si un database con i dati storici (come per il batch processing) che quelli in real time (come per il real time processing). In questo caso, si può adottare la lambda architecture, che prevede l'utilizzo di entrambi i paradigmi per poter fornire un servizio completo e affidabile.
Altro esempio è quello di un sistem di taxi, che deve mantenere sia i dati storici dei viaggi (per poter fare analisi e previsioni del traffico, da fornire sia agli utenti che ai driver) che quelli in real time (per poter fornire un servizio di prenotazione e gestione dei taxi in tempo reale).

## Layers
L'infrastruttura della lambda architecture è composta da tre layers.

### Batch layer
I dati vengono memorizzati sia nel batch layer che nello speed layer simultaneamente.
Serve per due compiti:
- gestire i dataset. I dati sono memorizzato in un file system ditribuito.
- eseguire dei pre calcoli sui batch views. I batch views sono il risultato dell'operazione batch che viene eseguita all'interno del batch layer sui dataset che gli vengono forniti. Si occupa di eliminare i file duplicati e di eseguire operazioni di aggregazione sui dati, per poter fornire dei risultati più veloci e precisi quando vengono richiesti dagli utenti.

### Speed layer
I dati vengono memorizzati sia nel batch layer che nello speed layer simultaneamente.
Qui viene usata la real time processing. I dati vanno nel message broker, passano nel processing job, analizza gli eventi ed aggiunge i dati al Real Time views.
Opera solo nei dati più recenti.

### Serving layer
Mergia i risultati del batch layer e dello speed layer, per poter fornire un servizio completo e affidabile agli utenti.

## Ad-Tech Industry - Example (Lambda Architecture in Action)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    CONTENT PRODUCERS                                        │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│          News Website                    Blog Website                      │
│          ┌──────────────┐                ┌──────────────┐                 │
│          │  [Browser]   │                │  [Browser]   │                 │
│          └──────────────┘                └──────────────┘                 │
│                 │                               │                         │
│                 └───────────────┬───────────────┘                         │
│                                 │                                         │
│                                 ▼ (ADS)                                  │
│                    ┌─────────────────────────┐                           │
│                    │ Digital Ads Service     │                           │
│                    │   [BATCH LAYER]         │                           │
│                    │   [SPEED LAYER]         │                           │
│                    │   [SERVING LAYER]       │                           │
│                    └─────────────────────────┘                           │
│                                 │                                         │
│                                 ▼ (WEBSITES)                             │
│                 ┌───────────────┴───────────────┐                         │
│                 │                               │                         │
│          ┌──────────────┐                ┌──────────────┐                 │
│          │ Online Store │                │  Concert     │                 │
│          └──────────────┘                └──────────────┘                 │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                          ADVERTISERS                                        │
└─────────────────────────────────────────────────────────────────────────────┘
```

In questo esempio, la lambda architecture consente al Digital Ads Service di:
- **Batch Layer**: Processare storicamente i dati degli annunci e dei siti web per analisi, previsioni e ottimizzazione
- **Speed Layer**: Gestire in tempo reale le richieste di annunci e l'interazione degli utenti
- **Serving Layer**: Fornire sia i dati storici processati che quelli real-time agli advertisers