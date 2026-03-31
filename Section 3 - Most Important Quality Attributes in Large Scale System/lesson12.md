# SLA, SLO, SLI

## SLA (Service Level Agreement)
Lo SLA indica il contratto legale firmato con i clienti che specifica la qualità dei servizi che la nostra azienda si impegna a fornire.
Un esempio di questi parametri da rispettare sono:
- availability 
- performance
- Data durability
- tempo di risposta sui fallimenti che il sistema ha

Descrive anche le penali e le conseguenze monetarie nel cosao in cui non si rispettano questi parametri.
Le penali possono essere:
- totale o parziale rimborso
- abbonamenti o licenze
- crediti per servizi futuri

## SLO (Service Level Objective)
Lo SLO è un obiettivo individuale che ci poniamo per il nostro sistema. Ogni SLO rappresenta un valore target che vogliamo raggiungere per un determinato parametro di qualità.
Per esempio:
- 99.9% di disponibilità
- 100ms di tempo di risposta al 90esimo percentile
- Risoluzione dei problemi entro 24 ore

Lo SLA è un contratto che racchiude gli SLO. Gli SLO però non dipendono necessariamo dallo SLA.

## SLI (Service Level Indicator)
Sono le metriche effettive che ci permettono di misurare se stiamo rispettando gli SLO e di conseguenza lo SLA.

Adesso capiamo perché gli attributi di qualità devono essere misurabili: perché in questo modo possiamo definire SLI e SLO e quindi SLA. Se non sono misurabili, non possiamo definire questi parametri e quindi non possiamo garantire la qualità del servizio ai nostri clienti.

Gli SLA vengono gestiti dal team di business e legal.
Gli SLO e gli SLI invece vengono gestiti dal team tecnico, ovvero dev e architect.

## Considerazioni importanti
- Non misurare tutto con gli SLI e di conseguenza non definire troppi SLO. Se definiamo troppi SLO, rischiamo di non riuscire a rispettarli tutti e quindi di non rispettare lo SLA.
- Promettere pochi SLO
- Definire SLO realistici e raggiungibili.
- Creare un piano di recovery per quando gli SLI mostrano che non stiamo rispettando gli SLO.