# Gama Academy - Transformando Talentos para o Futuro

## Node.JS - MySQL - KNex.JS

#### Autores
- [Gleyson Sampaio](https://github.com/gleyson-gama)

Hora de interagir com banco de dados para armazenar e obter as informações de nossa aplicação.

#### KNex.JS ?

Um módulo do Node.JS capaz de realizar interações de estrutura (DDL) e manipulação de registros  (DML) em uma base de dados relacional.

#### Requisitos
[Exemplo de aplicação Node.JS com padrão MVC](https://github.com/educacao-gama/tutoriais/tree/main/node-app-mvc)


#### Integrando o KNex na aplicação
1. Adicionamos as dependências do `knex` e ou do drive do banco de sua preferência, no nosso caso o  `mysql2`.
   ```
   yarn add knex
   ```
   
   ```
   yarn add mysql2
   ```
 1. E agora uma conferida em nossas dependências no arquivo `package.json`
 
  ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-knex/knex-mysql.png)
  
 #### Conectando ao banco de dados MySQL
 
 O Knex é compatível com qualquer banco de dados relacional conforme link [](http://knexjs.org/).
 Em nosso projeto será utilizado o MySQL com a seguinte configuração abaixo:
 
 * Criar o arquivo `knexfile.ts` no mesmo nível da pasta `src.ts`, este arquivo contém as propriedades para conectar ao banco MySQL
 
   ```
   export default {
    development: {
        client: 'mysql2',
        connection: {
            host: 'localhost',
            user: 'root',
            password: 'root',
            database: 'db_xp'
        }
    },
   };
   ```
   
 * Com o arquivo `knexfile.ts` contendo as configurações de banco, vamos iniciar a conexão ao MySQL
      1. Primeiro crie a pasta `src\database`
      2. Em seguida na pasta `src\database` o arquivo `connection.ts` com o conteúdo abaixo:
      ```
       import knex from 'knex';
       import knexFile from '../../knexfile';
       export default knex(knexFile['development']);
       console.log("Conexão realizada com sucesso !")
      ```
     
       
* Com a conexão devidamente configurada, hora de integrar o knex ao nosso Controller para interagir com a base de dados.
     1. No arquivo `src\controllers\CadastroController.ts` vamos importar o `knex connection` através da linha abaixo:
     
     ```
      import knex from '../database/connection';
     ```
     1. Tudo pronto para realizar nosso primeiro insert, update e select, mas precisamos criar nossa tabela de cadastro! É ai que entram as  `migrations`
     2. Crie a pasta `migrations` na pasta `src\database`
     3. Em seguida precisaremos incluir mais duas configurações no arquivo `knexfile.ts`
     
     ```
        migrations: {
            tableName: 'knex_migrations',
            directory: path.resolve(__dirname, 'src', 'database', 'migrations'),
        },
        seeds: {
            directory: path.resolve(__dirname, 'src', 'database', 'seeds'),
        }
     ```
    
     ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-knex/knex-migration.png)
     
 #### Migrations ?
 
   É um recurso capaz de gerenciar a pasta estrutural do banco de dados como criação de tabelas, alteração de colunas e etc. Cada migration contem 2 métodos principais que são:

   Up
   Dentro dele é colocado tudo o que tem que ser criado no banco de dados. Ex: tabelas, inserts, selects e tudo mais.

   Down
   Já o Down é ao contrário do UP, tudo o que for feito na UP é desfeito na DOWN, criei uma tabela na UP, dou drop na DOWN
