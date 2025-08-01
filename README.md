# ModelContextProtocol


```mermaid3
sequenceDiagram
    autonumber
    participant Host
    participant Client
    participant Server

    %% Inicialização
    Host->>Client: Initialize client
    Client->>Server: Initialize session with capabilities
    Server->>Client: Respond with supported capabilities

    %% Sessão ativa com recursos negociados
    rect rgb(60,60,60)
        Note over Host,Server: Active Session with Negotiated Features
    end

    %% Loop de requisições do cliente
    loop [Client Requests]
        Host->>Client: User- or model-initiated action
        Client->>Server: Request (tools/resources)
        Server->>Client: Response
        Client->>Host: Update UI or respond to model
    end

    %% Loop de requisições do servidor
    loop [Server Requests]
        Server->>Client: Request (sampling)
        Client->>Host: Forward to AI
        Host->>Client: AI response
        Client->>Server: Response
    end

    %% Loop de notificações
    loop [Notifications]
        Server-->>Client: Resource updates
        Server-->>Client: Status changes
    end

    %% Encerramento de sessão
    Host->>Client: Terminate
    Client->>Server: End session

```
