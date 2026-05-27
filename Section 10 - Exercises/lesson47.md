# Functional architecture diagram

```mermaid
flowchart LR
    U([User])
    GW[API Gateway]
    CDN[CDN]

    subgraph BACKEND[Backend Services]
        LB_US{Load Balancer}
        subgraph US_GROUP[Users Service]
            US_CREATE[Create New User]
            US_LOGIN[User Login]
        end
        DB1[(SQL Database)]

        LB_PC{Load Balancer}
        subgraph PC_GROUP[Posts & Comments Service]
            PC_POST[Create / View / Delete a Post]
            PC_COMMENT[Create / Get / Delete a Comment]
        end
        subgraph DB_PC_CLUSTER[NoSQL DB - Range Sharding on post_id+comment_id]
            SHARD1[(Shard 1)]
            SHARD2[(Shard 2)]
            SHARD3[(Shard 3)]
        end

        MB[[Message Broker\nAP - votes topic]]

        LB_R{Load Balancer}
        subgraph R_GROUP[Ranking Service]
            CQRS_CONTENT[Posts Content]
            CQRS_VOTES[Posts Votes / Popularity]
        end
        DB_RANK[(NoSQL Database)]

        LB_W{Load Balancer}
        W[Web App Service]
        Blob[(Blob Store)]

        LB_V{Load Balancer}
        subgraph V_GROUP[Votes Service]
            V_VOTE[Upvote / Downvote Post or Comment]
        end
        DB_V[(NoSQL Database)]
    end

    %% User to API Gateway
    U --> GW

    %% CDN serves static content
    GW -. HTML pages .-> CDN
    Blob -. images .-> CDN
    CDN -. cached content .-> U

    %% API Gateway routes to services via Load Balancers
    GW --> LB_US --> US_CREATE & US_LOGIN
    US_GROUP -. persists .-> DB1

    GW --> LB_PC --> PC_POST & PC_COMMENT
    PC_GROUP -. Range Sharding .-> SHARD1 & SHARD2 & SHARD3
    PC_GROUP -->|Posts| R_GROUP

    GW --> LB_R --> R_GROUP
    R_GROUP -. persists .-> DB_RANK

    GW --> LB_W --> W
    W -. stores images .-> Blob

    %% Votes flow via Message Broker (AP - eventual consistency)
    GW --> LB_V --> V_VOTE
    V_GROUP -. persists .-> DB_V
    V_GROUP -->|publishes votes| MB
    MB -->|consumes votes| PC_GROUP
    V_GROUP -->|Votes| R_GROUP
```

# NOTE
Il sistema di aggiornamento dei post più popolari deve essere implementato tramite sliding window, in quanto le 24 ore si spostano per ogni secondo che passa.

Batch processing per gestire i post popolari nelle ultime 24 ore da inserire nel Ranking Service

Il Message Broker usa AP (Availability + Partition Tolerance) per mantenere i voti aggiornati in maniera asincrona tra Votes Service e Posts & Comments Service, senza garanzie di consistenza immediata.