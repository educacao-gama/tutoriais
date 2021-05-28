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
    "database": "db_xp"
   }
   ```
   1. Em seguida criar uma conexão com base nas configurações acima atráves do novo arquivo `index.ts` dentro da nova pasta `src\database` com o seguinte conteúdo:
   
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
 
 * Altere o arquivo `ormconfig.json` definindo o(s) diretórios(s) que ficarão os arquivos criados para estruturação da base de dados
 
 ```
 "migrations":["./src/database/migrations/**.ts"],
 ```
 
 * Para criar as migrations precisaram exectar o cli do TypeOrm, basta incluir dentro de script no arquivo `package.json`:
 ```
 "typeorm":"ts-node-dev node_modules/typeorm/cli.js" 
 ```
 * Com o cli do TypeOrm configurado alteramos o arquivo `ormconfig.json` para executar a cli configurada:
 
 ```
 "cli":{
        "migrationsDir":"./src/database/migrations"
    }
 ```
 
 #### Criando uma Migration com Type ORM:
 
 Implemetando o modelo de negócio
 
 Com base eum projeto de pedidos estilo ecommerce temos um modelo de domínio e relacionamento entre tabelas que precisarão ser mapeadas e interagir com a base de dados.
 
 ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-type-orm/diagrmama.PNG)
 
 * Criando nossa primeira migration (create table tab_cliente) e obter o resultado conforme imagem
 
 ``` TERMINAL
 typeorm migration:create -n CreateTabCliente
 ```
 
  ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-type-orm/migration-tab_cliente.png)
  
  * Após o arquivo criado incluir o código que represente o DLL da tabela correspondente. NOTA: Esta fase exige bastantes noções de banco de dados e mapeamento de objetos
  
 ``` TERMINAL
 import {MigrationInterface, QueryRunner, Table} from "typeorm";

export class CreateTabCliente1622163365363 implements MigrationInterface {

   public async up(queryRunner: QueryRunner): Promise<void> {
       await queryRunner.createTable( 
           new Table({
               name: "tab_cliente",
               columns:[
                   {name: "id", type: "integer",isPrimary: true, isGenerated: true, generationStrategy: "increment"},
                   {name: "cpf_cnpj", type: "varchar", length: "15"},
                   {name: "nome", type: "varchar", length: "50"},
                   {name: "ativo", type: "boolean", default: true},
                   {name: "dt_inclusao", type: "timestamp", default: "now()"},
                   {name: "dt_alteracao", type: "timestamp", default: "now()"}   
               ]
           })
       )
   }

   public async down(queryRunner: QueryRunner): Promise<void> {
       await queryRunner.dropTable( "tab_cliente")
   }

}

 ```
 * Hora de validar se nossa tabela será criada com base nas configurações acima.
 * Criando a tabela
 ``` TERMINAL
 yarn typeorm migration:run
 ```
 
  ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-type-orm/migration-run.png)
 
 * Removendo (Revertendo) a instrução anterior
 ``` TERMINAL
 yarn typeorm migration:revert
 ```
#### Mapeando a entidade Cliente.ts:

 * Dentro de `src` crie a pasta `entities` e dentro de entitites crie o arquivo `Cliente.ts` com o código abaixo:
 
 ```
 import {Entity, Column, CreateDateColumn, UpdateDateColumn, PrimaryColumn,PrimaryGeneratedColumn } from "typeorm";

@Entity("tab_user")
class Cliente{
    @PrimaryGeneratedColumn()
    id: number;

    @Column({name:"cpf_cnpj"})
    cpfCnpj: string;
    
    @Column()
    nome: string;
    
    @Column()
    ativo: boolean;
    
    @CreateDateColumn({name:"dt_inclusao"})
    dataInclusao: Date

    @UpdateDateColumn({name:"dt_alteracao"})
    dataAlteracao: Date

    
}
export {Cliente}
 ```
 
* Mepeamento\Decorators são declarações que iniciam com `@` logo faz-se necessário habilitar duas propriedades no arquivo `tsconfi.json`
```
"experimentalDecorators": true,              /* Enables experimental support for ES7 decorators. */
"emitDecoratorMetadata": true,               /* Enables experimental support for emitting type metadata for decorators. */
```
