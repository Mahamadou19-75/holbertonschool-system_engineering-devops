```mermaid
flowchart TD
    User["👤 User\nwww.foobar.com"]
    DNS["🌐 DNS\nwww → 8.8.8.8\n(A Record)"]

    LB["⚖️ HAProxy\nLoad Balancer\nRound Robin"]

    subgraph Server1["🖥️ SERVER 1"]
        Nginx1["🌍 Nginx"]
        App1["⚙️ App Server"]
        Code1["📁 Code Base"]
        Nginx1 --> App1 --> Code1
    end

    subgraph Server2["🖥️ SERVER 2"]
        Nginx2["🌍 Nginx"]
        App2["⚙️ App Server"]
        Code2["📁 Code Base"]
        Nginx2 --> App2 --> Code2
    end

    subgraph DB["🗄️ Database Cluster"]
        Primary[("🟢 MySQL Primary\nREAD + WRITE")]
        Replica[("🔵 MySQL Replica\nREAD only")]
        Primary -->|"Replication"| Replica
    end

    User -->|"1. DNS Query"| DNS
    DNS -->|"2. Returns 8.8.8.8"| User
    User -->|"3. HTTP Request"| LB
    LB -->|"Active-Active"| Server1
    LB -->|"Active-Active"| Server2
    App1 --> Primary
    App2 --> Primary
    App1 -.-> Replica
    App2 -.-> Replica
