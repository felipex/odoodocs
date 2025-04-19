# Visão Geral da Arquitetura do Odoo

O Odoo é uma plataforma de ERP/CRM modular, construída com uma arquitetura flexível e extensível, permitindo personalizações robustas. Sua estrutura combina tecnologias modernas para oferecer escalabilidade, modularidade e integração contínua.

---

## Arquitetura Técnica

### Modelo Cliente-Servidor
- **Backend**: Escrito em Python, responsável pela lógica de negócio, acesso ao banco de dados e processamento de requisições.
- **Frontend**: Interface web baseada em JavaScript (OWL Framework) e templates QWeb.
- **Banco de Dados**: PostgreSQL para armazenamento de dados, gerenciado via ORM do Odoo.

### Arquitetura em Camadas
1. **Camada de Banco de Dados**: Armazena dados estruturados e metadados (modelos, visões, regras de segurança).
2. **Camada de Aplicação** (Python):
   - ORM: Conecta modelos Python ao PostgreSQL.
   - Módulos: Lógica de negócio, regras e automações.
   - Serviços: Cron, filas de tarefas, APIs.
3. **Camada de Apresentação** (JavaScript/XML):
   - Visões definidas em XML, renderizadas pelo motor QWeb.
   - Componentes dinâmicos com OWL (Odoo Web Library).

### Padrão MVC Adaptado
- **Modelos (Model)**: Classes Python que definem estruturas de dados e regras de negócio.
- **Visões (View)**: Templates XML/JS para a interface do usuário.
- **Controladores (Controller)**: Gerenciam requisições HTTP e APIs externas.

---

## Frameworks Principais

### 1. ORM (Object-Relational Mapping)
- Abstração do PostgreSQL para operações CRUD.
- Suporte a campos computados, herança de modelos e constraints.
- Exemplo:
  ```python
  class Livro(models.Model):
      _name = 'biblioteca.livro'
      titulo = fields.Char(string="Título")
      autor_id = fields.Many2one('biblioteca.autor', string="Autor")/