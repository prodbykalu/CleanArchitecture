# Functional architecture diagram

```mermaid
flowchart LR
    U([User])

    subgraph CLIENT[Client]
        W[Web App Service]
        Blob[(Blob Store)]
    end

    subgraph BACKEND[Backend Services]
        subgraph US_GROUP[Users Service]
            US_CREATE[Create New User]
            US_LOGIN[User Login]
        end
        DB1[(SQL Database)]

        subgraph PC_GROUP[Posts & Comments Service]
            PC_POST[Create / View / Delete a Post]
            PC_COMMENT[Create / Get / Delete a Comment]
        end
        DB_PC[(NoSQL Database)]

        subgraph R_GROUP[Ranking Service]
            CQRS_CONTENT[Posts Content]
            CQRS_VOTES[Posts Votes / Popularity]
        end
        DB_RANK[(NoSQL Database)]

        subgraph V_GROUP[Votes Service]
            V_VOTE[Upvote / Downvote Post or Comment]
        end
        DB_V[(NoSQL Database)]
    end

    %% Client flows
    U -. Web Pages .-> W
    U -. Images .-> W
    W -. stores images .-> Blob
    U -->|Get Image| Blob

    %% Users Service
    U --> US_CREATE & US_LOGIN
    US_GROUP -. persists .-> DB1

    %% Posts & Comments Service
    U --> PC_POST & PC_COMMENT
    PC_GROUP -. persists .-> DB_PC
    PC_GROUP -->|Posts| R_GROUP

    %% Ranking Service
    R_GROUP -. persists .-> DB_RANK

    %% Votes Service
    U --> V_VOTE
    V_GROUP -->|Votes| R_GROUP
    V_GROUP -. persists .-> DB_V
```

# NOTE
Il sistema di aggiornamento dei post più popolari deve essere implementato tramite sliding window, in quanto le 24 ore si spostano per ogni secondo che passa.

Batch processing per gestire i post popolari nelle ultime 24 ore da inserire nel Ranking Service

## Fault tolerance
Replicazione del sito in più data center per quando uno crasha
Più db per ogni servizio

Otteniamo durability gratis facendo tutti questi accorgimenti.