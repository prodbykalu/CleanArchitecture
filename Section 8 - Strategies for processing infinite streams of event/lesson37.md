# Event-Stream processing
Per processare un flusso infinito di eventi, si possono suddividere tutti gli eventi in sotto gruppi.

Fondamentale per i seguenti processi:
- anomaly detection: identificare eventi che si discostano dal comportamento normale.
- pattern recognition: identificare schemi ricorrenti nei dati.
- fraud detection: identificare attività fraudolente o sospette.
- recommendation services: fornire raccomandazioni personalizzate basate sui dati degli utenti.

# Tumbling window strategy
In questa strategia, il flusso di eventi viene suddiviso in finestre di tempo fisse, chiamate "tumbling windows". Ogni finestra contiene un insieme di eventi che si verificano all'interno di un intervallo di tempo specifico. Ad esempio, si potrebbe avere una finestra di 5 minuti che raccoglie tutti gli eventi che si verificano in quel periodo. Una volta che la finestra è completa, viene elaborata e i risultati vengono prodotti.