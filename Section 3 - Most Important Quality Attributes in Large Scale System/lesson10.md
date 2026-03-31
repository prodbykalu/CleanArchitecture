# Availability

## Importanza e rischi
Ha un grosso impatto sia verso gli utenti che verso il nostro business

Per esempio, se un sito di e-commerce è offline, non solo perde vendite, ma anche la fiducia dei clienti. Se un sito di notizie è offline, gli utenti potrebbero cercare informazioni altrove, e potrebbero non tornare più.

Esempio di disservizio lato business:
- **Amazon**: nel 2017, Amazon ha subito un'interruzione nel nodo North Virginia di circa 40 minuti, causando una perdita stimata di 150 milioni di dollari

## Definizione
Per availability si intende la frazione ti tempo che il nostro servizio si operativo e disponibile per gli utenti. 

$\text{Availability} = \frac{\text{Uptime}}{\text{Uptime} + \text{Downtime}} \times 100\%$

$\text{Uptime}$: Tempo di disponibilità del nostro sistema

$\text{Downtime}$: Tempo in cui il nostro sistema è offline o non disponibile per gli utenti.

## Altra formula per calcolare l'Availability
$\text{Availability} = \frac{\text{MTBF}}{\text{MTBF} + \text{MTTR}} \times 100\%$

$\text{MTBF Mean Time Between Failures}$

Sarebbe sostanzialmente il tempo di uptime.

Rappresenta il tempo medio tra un guasto e l'altro. Indica quanto tempo, in media, il nostro sistema funziona correttamente prima di subire un guasto.

$\text{MTTR Mean Time To Repair}$

Sarebbe il tempo di downtime

Rappresenta il tempo medio necessario per riparare un guasto e riportare il sistema in uno stato operativo. Indica quanto tempo, in media, ci vuole per risolvere un problema e far tornare il sistema online.

### Note
Più aumenta il MTTR, più diminuisce l'Availability, poiché il sistema rimane offline per un periodo più lungo. Al contrario, più aumenta il MTBF, più aumenta l'Availability, poiché il sistema funziona correttamente per periodi più lunghi prima di subire un guasto.