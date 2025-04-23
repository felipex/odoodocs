# Instalação do Odoo

Há algumas formas diferentes de se instalar o Odoo, mas como nosso foco aqui é exclusivamente o desenvolvedor, vamos nos ater à instalação a partir do código fonte que está no repositório do github [https://github.com/odoo/odoo](https://github.com/odoo/odoo). O procedimento de instalação pode ser encontrado na [documentação oficial](https://www.odoo.com/documentation/18.0/pt_BR/administration/on_premise/source.html). Basicamente precisamos seguir o mesmot roteiro, mas fizemos algumas adaptações e colocamos alguns comentários a mais para tentar facilitar o entendimento pra quem vai começar do zero.


## Pré-requisitos

É preciso instalar algumas ferramentas antes de instalarmos o código fonte do Odoo para ser usado no desenvolvimento. Apesar de poder ser feito qualquer sistema operacional, recomentamos fortemente que seu ambiente de desenvolvimento seja baseado no Linux. Para não deixar esse documento muito extenso iremos nos concentrar na instalação apenas do Odoo, não trataremos da instalação das outras ferramentas das quais ele depende.

#### Python3

[Python](https://www.python.org/) é uma linguagem de programação que permite trabalhar rapidamente
e integrar sistemas de forma mais eficaz. Instalar também o pip3.

#### PostgreSQL

O [PostgreSQL](https://www.postgresql.org/) é um poderoso sistema de banco de dados relacional de objetos, de código aberto, com mais de 35 anos de desenvolvimento ativo, o que lhe rendeu uma forte reputação de confiabilidade, robustez de recursos e desempenho.

#### Git

[Git](https://git-scm.com/) é um sistema de controle de versão distribuído , gratuito e de código aberto, projetado para lidar com tudo, desde projetos pequenos até muito grandes, com rapidez e eficiência.

#### Conta no Github

Para facilitar o trabalho de desenvolvimento é ter uma conta no [github](https://github.com/) para fazer o controle de versões do projeto e facilitar as implantações.

## Instalação

Certiffique-se de estar com os pré-requisitos todos instalados e operantes.

### Criar usuário para o sistema e se logar como esse novo usuário <strong style="color:red">Essa parte é apenas para o deploy.</strong>
```
# useradd odoo
```
```
# usermod -aG sudo odoo
```
```
# su - odoo
```

### Criar usuário do banco de dados baseado no usuário do sistema
```
$ sudo -u postgres createuser -d -R -S $USER
```
### Criar banco de dados baseado no usuário do sistema
```
$ createdb $USER
```

### Faça um fork do [repostirório oficial do Odoo](https://github.com/odoo/odoo)
### Clone o projeto para sua máquina de trabalho
```
$ git clone https://github.com/odoo/odoo.git
```

### Instalar dependências
```
$ cd odoo
$ sudo ./setup/debinstall.sh
```

### Primeira execução (configuração inicial)
```
python3 odoo-bin -d $USER -i base
```

### Execução
```
python3 odoo-bin -d $USER -i base
```
No navegador
Abra http://localhost:8069/ no navegador. 

Para se logar como administrador, use as seguintes credenciais
email: admin
password: admin
