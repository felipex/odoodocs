# Sobre
### Documentação do Odoo ERP
Estou estudando Odoo e a mameira mais fácil que eu achei de documentar os estudos foi construindo essa documentação paralela.

Qualquer dúvida ou sugestão é só entrar em contato com <felipexcavalcante@gmail.com> ou através da página do github deste projeto <strong style="color: red">colocar aqui o endereço do github e como contribuir</strong>

```mermaid
graph TD
subgraph "Cliente"
    A[Navegador do Cliente]
end

subgraph "Sua Plataforma Web"
    B[Frontend Web]
    C[Backend/API]
    D[Orquestrador (K8s API)]
end

subgraph "Infraestrutura Hetzner"
    subgraph "Cluster Kubernetes"
        E(Ingress Controller)
        subgraph "Namespace Cliente 1"
            F[Contêiner Odoo]
        end
        subgraph "Namespace Cliente 2"
            G[Contêiner Odoo]
        end
    end
    subgraph "Serviço de BD Gerenciado"
        H[Banco de Dados Cliente 1]
        I[Banco de Dados Cliente 2]
    end
end

A --> |HTTPS| E
E --> |Roteamento K8s| F & G
C --> |Chamada API Helm/K8s| D
D --> |Deploy de Contêiner| F & G
F --> H
G --> I

style A fill:#bbf,stroke:#333,stroke-width:2px;
style B fill:#bbf,stroke:#333,stroke-width:2px;
style C fill:#bbf,stroke:#333,stroke-width:2px;
style D fill:#bbf,stroke:#333,stroke-width:2px;
style F fill:#f9f,stroke:#333,stroke-width:2px;
style G fill:#f9f,stroke:#333,stroke-width:2px;
style E fill:#9cf,stroke:#333,stroke-width:2px;
style H fill:#f9f,stroke:#333,stroke-width:2px;
style I fill:#f9f,stroke:#333,stroke-width:2px;
```

```mermaid
C4Container
title Diagrama de Contêineres - Solução Exequível

Person(person_cliente, "Cliente")
Person(app_cliente, "App Cliente")

System_Boundary(boundary_plataforma, "Plataforma de Implantação") {
    Container(c_frontend, "Frontend Web", "Aplicação SPA", "HTML, CSS, JavaScript")
    Container(c_backend, "Backend API", "API REST", "Python (FastAPI/Flask)")
    Container(c_automacao, "Motor de Automação", "Scripts de provisionamento", "Python")
}

System_Boundary(boundary_vps, "VPS do Cliente") {
    Container(c_nginx, "Nginx Proxy Manager", "Proxy Reverso, SSL", "Docker")
    Container(c_odoo, "Contêiner Odoo", "Aplicação Odoo", "Docker")
    Container(c_postgres, "Contêiner PostgreSQL", "Banco de Dados", "Docker")
}

Rel(person_cliente, c_frontend, "Usa para interagir com a plataforma")
Rel(c_frontend, c_backend, "Chama a API para fazer requisições")
Rel(c_backend, c_automacao, "Aciona script para iniciar o provisionamento")

Rel(c_automacao, c_nginx, "Configura rotas via API")
Rel(c_automacao, c_odoo, "Provisiona ambiente (SSH, Docker Compose)")
Rel(c_automacao, c_postgres, "Provisiona banco de dados (SSH, Docker Compose)")


Rel(person_cliente, c_nginx, "Acessa a instância do Odoo")
Rel(app_cliente, c_nginx, "Acessa a instância do Odoo")
Rel_Back(c_nginx, c_odoo, "Roteia tráfego para a aplicação")
Rel(c_odoo, c_postgres, "Conecta ao banco de dados")
```