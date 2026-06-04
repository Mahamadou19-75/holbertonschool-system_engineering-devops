flowchart TD
    User["👤 User<br>www.foobar.com"]

    subgraph LB_Cluster["⚖️ HAProxy Cluster"]
        LB1["HAProxy 1"]
        LB2["HAProxy 2"]
        LB1 <-->|"sync"| LB2
    end

    subgraph WebServer["🖥️ Web Server"]
        Nginx["🌍 Nginx<br>Serves static files<br>Handles HTTP/HTTPS"]
    end

    subgraph AppServer["⚙️ Application Server"]
        App["🔧 App Server<br>Runs business logic<br>Processes dynamic requests"]
        Code["📁 Code Base"]
        App --> Code
    end

    subgraph DBServer["🗄️ Database Server"]
        DB[("🟢 MySQL<br>Stores & manages data")]
    end

    User -->|"HTTPS"| LB1
    User -->|"HTTPS"| LB2
    LB1 --> Nginx
    LB2 --> Nginx
    Nginx --> App
    App --> DB
