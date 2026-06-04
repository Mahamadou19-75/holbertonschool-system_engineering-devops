```mermaid
graph TD
    %% Définition des styles globaux
    classDef default fill:#1e1e1e,stroke:#fff,stroke-width:1px,color:#fff;
    classDef orangeZone fill:#c77d60,stroke:#none,color:#fff;
    classDef transparent fill:none,stroke:none,color:#fff;

    %% Nœuds extérieurs
    Browser["💻 User browser<br>Requests www.foobar.com"]
    DNS["🌐 DNS resolver<br>www &rarr; A record &rarr; 8.8.8.8"]

    %% Zone de sous-graphe pour le serveur (Fond orange)
    subgraph ServerZone["🖥️ Server — IP: 8.8.8.8"]
        Nginx["Nginx — web server<br>Handles HTTP, serves static files"]
        AppServer["Application server<br>Executes business logic"]
        Codebase["Application codebase<br>Your app files (PHP, Python...)"]
        DB[("MySQL database<br>Stores persistent data")]
    end

    %% Connexions et flux de données
    Browser -->|1. DNS query| DNS
    DNS -->|2. Returns IP 8.8.8.8| Browser
    Browser -->|3. HTTP/HTTPS request| Nginx
    Nginx -->|4. HTTP response| Browser

    Nginx -->|forwards dynamic requests| AppServer
    AppServer -->|uses| Codebase
    AppServer -->|SQL queries| DB

    %% Application des styles
    style ServerZone fill:#c77d60,stroke:#none,color:#00daff
    style Browser fill:#1e1e1e,stroke:#666,stroke-width:1px
    style DNS fill:#1e1e1e,stroke:#666,stroke-width:1px
    style Nginx fill:#1e1e1e,stroke:#666,stroke-width:1px
    style AppServer fill:#1e1e1e,stroke:#666,stroke-width:1px
    style Codebase fill:#1e1e1e,stroke:#666,stroke-width:1px
    style DB fill:#1e1e1e,stroke:#666,stroke-width:1px
