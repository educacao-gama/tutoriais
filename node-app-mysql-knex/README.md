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
 
É um recurso capaz de gerenciar estrutura do banco de dados como criação de tabelas, alteração de colunas e etc. Cada migration contem 2 métodos principais que são:

Up
Dentro dele é colocado tudo o que tem que ser criado no banco de dados. Ex: tabelas, inserts, selects e tudo mais.

Down
Já o Down é ao contrário do UP, tudo o que for feito na UP é desfeito na DOWN, criei uma tabela na UP, dou drop na DOWN
   
 #### Criando uma Migration:

 * Execute o comando:
 ```
 knex migrate:make create_tab_cadastro
 ```
 * Se receber o erro "'knex' não é reconhecido como um comando interno" será necessário instalar o knex de forma global para depois executar o comando anterior
 ```
 npm install -g knex
 ```
 
 * Tudo rodando direitinho será criado um arquivo de nome `20210526150627_create_tab_cadastro.ts` onde o prefixo `20210526150627_` representa um valor data-hora de geração do arquivo.

![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-knex/migration-tab-cadastro.png)


 #### Uuuuufa em
 
 ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-knex/ufa2.jpg)
 
 Agora é hora de exercitar todo o domínio em estruturação da base dados para criarmos as tabelas da aplicação.
 
 * Primeiro vamos criar a tabela tab_cadastro com os campos id, cpf e nome alterando o arquivo `20210526150627_create_tab_cadastro.ts`
 ```
import { Knex } from "knex";

export async function up(knex: Knex): Promise<void> {
    return await knex.schema.createTable('tab_cadastro', (table) => {
        table.increments('id').unique();
        table.specificType('cpf', 'VARCHAR(11)').notNullable().unique();
        table.specificType('nome', 'VARCHAR(50)').notNullable();
    });
}

export async function down(knex: Knex): Promise<void> {
    return await knex.schema.dropTable('tab_cadastro');
}
 ```
 
* Hora de executar nossas migrations e validar se nossa tab_cadastro foi criada

```
yarn knex migrate:latest
```

![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-knex/migrations-run.png)

* Agora vamos executar os comandos SQL através do `Knex` em nosso `CadastroController.ts`
   1. Importe o knex no controlador.
      ```
      import knex from '../database/connection';
      ```
   1. No método `list`, altere o valor da variável `result` para:
      ```
      var result=await knex('tab_cadastro').orderBy('nome');
      ```
   1. Se preferir insira estes dados direto no banco de dados:
      ```
      INSERT INTO db_xp.tab_cadastro
      (id, cpf, nome)
      VALUES(1, '18231108009', 'JOSE DA SILVA');
      INSERT INTO db_xp.tab_cadastro
      (id, cpf, nome)
      VALUES(2, '02243950090', 'MARIA ALMEIDA');
      INSERT INTO db_xp.tab_cadastro
      (id, cpf, nome)
      VALUES(3, '82278087002', 'MARCOS PAULO SANTOS');
      INSERT INTO db_xp.tab_cadastro
      (id, cpf, nome)
      VALUES(4, '72931182010', 'FAUSTINO ANTUNES');
      ```
   1. Conforme imagem, nossa consulta de cadastros no banco de dados funcinou, hora de implementar as demais interções no banco
      ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-knex/migrations-run.png)

 #### Últimos detalhes
 
 1. No arquivo `server.ts` incluir o recurso de requisição para `json`
 ```
 app.use(express.json());
 ```
 
  1. No arquivo `routes.ts` registrar as novas rotas
 ```
 import { Router } from 'express';
import CadastroController from './controllers/CadastroController';

const routes = Router();

routes.get('/cadastros', CadastroController.list);
routes.get('/cadastros/:id', CadastroController.find);
routes.post('/cadastros', CadastroController.create);
routes.put('/cadastros/:id', CadastroController.update);
routes.delete('/cadastros/:id', CadastroController.delete);

export default routes;

 ```
 1. E claro no arquivo `CadastroController.ts` implementar as funcionalidades de CRUD para a tabela tab_cadastro
  ```
 import { Request, Response } from 'express';

import knex from '../database/connection';

export default {
    async list(req: Request, res: Response) {
        var result=await knex('tab_cadastro').orderBy('nome');
        
        return res.status(200).json({ data:result});
    },
    async find(req: Request, res: Response) {
        const { id } = req.params;
        
        const user = await knex('tab_cadastro').where({ id });
        
        return res.status(200).json(user);
    },
    async create(req: Request, res: Response) {
        const { cpf, nome} = req.body;
        const data = {cpf,nome};

        await knex('tab_cadastro').insert(data);
        
        return res.status(201).json(data);
    },
    async update(req: Request, res: Response) {
        const { id } = req.params;
        const { nome, cpf} = req.body;

        const data = {cpf,nome};

        await knex('tab_cadastro').update(data).where({ id });

        const user = await knex('tab_cadastro').where({ id });
        
        return res.status(200).json(user);
        
    },
    async delete(req: Request, res: Response) {
        const { id } = req.params;
        await knex('tab_cadastro').del().where({ id });
        return res.status(200).json({ message: 'Registro excluido com sucesso!' });
    },
}
 ```
1. Agora é testar através de algum cliente API como o insomnia (abaixo terá o import das requisições realizadas para teste)

 [insomnia-requests.json](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-knex/insomnia-api-xp-gama.json)
 ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-knex/api-client.png)
 
