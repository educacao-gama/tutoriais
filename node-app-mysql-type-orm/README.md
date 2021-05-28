# Gama Academy - Transformando Talentos para o Futuro

## Node.JS - MySQL - ORM - TypeOrm

#### Autores
- [Gleyson Sampaio](https://github.com/gleyson-gama)

Melhoraremos a nossa de repositorio com o conceito de ORM com TypeOrm

#### Type ORM? [link](https://typeorm.io/#/)

Um recurso em Node.JS para disponibilizar umas das implementações do conceito ORM em conversão de dados em objetos e vice-versa .

#### Requisitos
[Exemplo de aplicação Node.JS com padrão MVC](https://github.com/educacao-gama/tutoriais/tree/main/node-app-mvc)


#### Integrando o TypeOrm na aplicação
1. Adicionamos as dependências do `typeorm` e ou do drive do banco de sua preferência, no nosso caso o  `mysql2`.

   ```
   yarn add typeorm
   yarn add reflect-metadata
   ```
   
   ```
   yarn add mysql2
   ```
   
1. Nesta parte seguiremos as intruções do próprio [site](https://typeorm.io/#/using-ormconfig) criando primeiramento o arquivo `ormconfig.json` pasta `src` 
   1. Dentro do arquivo `ormconfig.json` incluir a configuração de conexão ao banco de dados:
   ```
   {
    "type": "mysql",
    "host": "localhost",
    "port": 3306,
    "username": "root",
    "password": "root",
    "database": "xp_db"
   }
   ```
   1. Em seguida criar uma conexão com base nas configurações acima atráves do novo arquivo `index.ts` dentro da nova pasta `database` com o seguinte conteúdo:
   
   ```
   import {createConnection} from 'typeorm';

   createConnection();
   ```
   
#### Migrations ?
 
É um recurso capaz de gerenciar estrutura do banco de dados como criação de tabelas, alteração de colunas e etc. Cada migration contem 2 métodos principais que são:

Up
Dentro dele é colocado tudo o que tem que ser criado no banco de dados. Ex: tabelas, inserts, selects e tudo mais.

Down
Já o Down é ao contrário do UP, tudo o que for feito na UP é desfeito na DOWN, criei uma tabela na UP, dou drop na DOWN
   
 #### Criando uma Migration com Type ORM:

 * Dentro da pasta `database` criar a pasta `migrations`
 
 * Execute o comando:
 ```
 knex migrate:make create_tab_cadastro
 ```