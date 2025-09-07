# Sobre
### Documentação do Odoo ERP
Estou estudando Odoo e a mameira mais fácil que eu achei de documentar os estudos foi construindo essa documentação paralela.

Qualquer dúvida ou sugestão é só entrar em contato com <felipexcavalcante@gmail.com> ou através da página do github deste projeto <strong style="color: red">colocar aqui o endereço do github e como contribuir</strong>

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