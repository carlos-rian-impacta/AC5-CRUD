# AC5 - CRUD de Itens

## Tecnologias
- Python FastAPI - Framework Web
- Docker - Engine de virtualização para criar container
- Docker Compose - Gerenciar a criação dos containers
- PostgreSQL - Banco de dados relacional
- Nginx - Proxy reverso

---

## Backend - Estrura MVC

Dentro da pasta app a estrutura de pasta abaixo.

- config: Tem o arquivo responsável por pegar a variavel de ambiente com as informações do banco.
- controller: Tem o arquivo de item.py onde tem toda a regra de négocio.
- model: tem dois arquivos database e table, onde é criado a conexão com o banco e o mapeamento da tabela via ORM sqlalchemy.
- resource: Tem o arquivo item onde é declarado os endpoints, é usada a arquitetura de Factory para injetar os novos endpoints no app principal. Essa camada seria o V de view.
- schema: Tem os arquivos com mapeamento e validações de tipos, é comum chamar essa camada de DTO (Data Transfer Object), é uma camada que fica transitando entre as outras com os dados.

- main.py: É o arquivo de entrypoint para a aplicação, ele cria o app e monta toda a aplicação usando fatory, ou seja, vai montando cada parte da aplicação por meio das funçōes init_app.

---
## Nginx

Dentro da pasta nginx tem dois arquivos, o dockerfile que é o arquivo que irá contruir a imagem do nginx e nginx.conf que tem a configuração para onde deve ser encaminhada as requisições e esperar as respostas.


## Dockerfile

Dentro do dockerfile na raiz do projeto tem as instruções de como deve ser criado o projeto, então é instalada as dependências listadas no arquivo requirements.txt e é copiado o backend que está na pasta /app.


## Docker-compose

É o arquivo responsável por coordenar a criação dos nossos container, então nele estã descrito os 3 serviços que precisam subir.
- nginx - depende do container de app
- app - depende do container database
- database - não depende de nada

O docker compose é o responsável por conectar os containers na mesma rede e criar o link entre eles por meio da rede backedn e default, é usado tag depends_on para criar uma conexão entre os containers.
Neste caso somente o nginx e o banco dão o Expose em uma porta para o container.

## Executar os containers

1 - Execute o comando abaixo no terminal.
``` shell
docker-compose up --build
```

2 - Acesse a url abaixo pelo navegador.
``` shell
localhost:80/docs
```

3 - Veja a documentação gerada via OpenAPI.