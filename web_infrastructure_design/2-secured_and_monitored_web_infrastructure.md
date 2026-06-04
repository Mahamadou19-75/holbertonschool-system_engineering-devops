```mermaid 
flowchart TD
    User["👤 User\nwww.foobar.com"]
    DNS["🌐 DNS\nA Record → 8.8.8.8"]

    FW1["🛡️ Firewall 1"]
    
    subgraph LB["⚖️ HAProxy — SSL Termination\n🔒 SSL Certificate"]
        Monitor0["📊 Monitoring Client"]
    end

    FW2["🛡️ Firewall 2"]
    FW3["🛡️ Firewall 3"]

    subgraph Server1["🖥️ SERVER 1"]
        Nginx1["🌍 Nginx"]
        App1["⚙️ App Server"]
        Code1["📁 Code Base"]
        DB1[("🟢 MySQL Primary")]
        Monitor1["📊 Monitoring Client"]
        Nginx1 --> App1 --> Code1
        App1 --> DB1
    end

    subgraph Server2["🖥️ SERVER 2"]
        Nginx2["🌍 Nginx"]
        App2["⚙️ App Server"]
        Code2["📁 Code Base"]
        DB2[("🔵 MySQL Replica")]
        Monitor2["📊 Monitoring Client"]
        Nginx2 --> App2 --> Code2
        App2 --> DB2
    end

    Cloud["☁️ Sumologic\nMonitoring Service"]

    User -->|"HTTPS"| DNS
    DNS --> User
    User -->|"HTTPS 443"| FW1
    FW1 --> LB
    LB -->
