# Esercizio 1 - Higly Scalable Ride-Sharing App (like Uber)

## Assegnazione dei metodi HTTP alle risorse:

### Registrazione e autenticazione
POST /users
POST /auth/login

### Corse
POST /rides
GET /rides/{rideId}
GET /rides?passengerId={passengerId}
POST /rides/{rideId}/accept
POST /rides/{rideId}/start
POST /rides/{rideId}/complete
POST /rides/{rideId}/cancel

### Driver
PUT /drivers/{driverId}/availability

### Posizione (WebSocket)
WS /position


## Schema
```mermaid
flowchart TB
    U([User])
    GW[API Gateway\nauth / rate limiting / routing]

        subgraph US_GROUP[User Service]
            US_CREATE(Create New User)
            US_LOGIN(User Login)
        end
        DB1[(SQL Database)]

        subgraph D_GROUP[Driver Service]
            D_UPDATE(Update Driver Availability)
        end
        DB3[(NoSQL Database)]

        subgraph PS_GROUP[Realtime Gateway]
            PS_UPDATE(Update Position via WebSocket)
        end
        DB4[(Redis GEO)]

        subgraph R_GROUP[Rides Service]
            R_CREATE(Create / View / Update a Ride)
            R_REVIEW(Submit Review)
        end
        DB2[(NoSQL Database)]

        subgraph KAFKA[Kafka]
            T1[[ride-created]]
            T2[[driver-assigned]]
            T3[[ride-completed]]
         end

        subgraph M_SERVICE[Matching Service]
            M_MATCH(Match Passenger with Driver)
            M_GET_DRIVERS(Get Nearby Drivers)
        end

        subgraph P_GROUP[Payment Service]
            P_PROCESS(Process Payment)
        end
        DB6[(SQL Database)]

        subgraph N_GROUP[Notification Service]
            N_PUSH(Push / SMS / WebSocket Notification)
        end

    %% User entry via API Gateway
    U --> GW

    %% Users Service
    GW --> US_CREATE & US_LOGIN
    US_GROUP -. persists .-> DB1

    %% Driver Service
    GW --> D_UPDATE
    D_UPDATE -. persists .-> DB3

    %% Realtime Gateway (WebSocket)
    U -. WebSocket .-> PS_UPDATE
    PS_UPDATE -. persists .-> DB4

    %% Rides Service
    R_GROUP -. persists .-> DB2
    GW --> R_CREATE & R_REVIEW

    %% Async event flow via Kafka
    R_CREATE -->|RideCreated| T1
    T1 -->|RideCreated| M_MATCH
    M_GET_DRIVERS --> DB4
    M_MATCH --> M_GET_DRIVERS
    M_MATCH -->|DriverAssigned| T2
    T2 -->|DriverAssigned| R_GROUP
    T2 -->|DriverAssigned| N_GROUP

    R_GROUP -->|RideCompleted| T3
    T3 -->|RideCompleted| P_PROCESS
    T3 -->|RideCompleted| N_GROUP
    P_PROCESS -. persists .-> DB6
```

## NOTE
- Il **Matching Service** è la parte più critica: trova driver vicini in millisecondi usando Redis GEO (GEOSEARCH/GEORADIUS) su milioni di driver.
- **Kafka** disaccoppia i servizi e gestisce i flussi asincroni: matching, pagamento e notifiche sono tutti event-driven.
- Il **Payment Service** è asincrono per gestire retry, idempotenza e lentezza dei gateway di pagamento esterni.
- Il **Realtime Gateway** gestisce milioni di connessioni WebSocket + Redis Pub/Sub per la posizione in tempo reale.