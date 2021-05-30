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
   npm install --global typeorm
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

* Ao persistir com framework ORM, o mesmo prové de mecanismos de repositório que dispõe de métodos CRUD sobre a entidade declarara, com isso dentro de `src` crie a pasta `repositories` e dentro de repositories o arquivo  `ClienteRepository` com o código abaixo.

```
import {EntityRepository, Repository} from "typeorm";
import { Cliente } from "../entities/Cliente";

@EntityRepository(Cliente)
class ClienteRepository extends Repository <Cliente> {

}

export {Cliente}
```

* Tudo configurado com nossa entidade Cliente e seu repositório, partimos para a criação do controller, para isso dentro de `src` crie a pasta `controllers` e dentro de controllers o arquivo  `ClienteController` com o código abaixo.

* Para testar nosso crud de Cliente agora nos resta definir as rotas para obter os recursos HTTP criando o arquivo `src\routes.ts` com o código abaixo:
```
import { Router } from 'express';
import ClienteController from './controllers/ClienteController';

const routes = Router();

routes.get('/Clientes', ClienteController.list);
routes.get('/Clientes/:id', ClienteController.find);
routes.post('/Clientes', ClienteController.create);
routes.put('/Clientes/:id', ClienteController.update);
routes.delete('/Clientes/:id', ClienteController.delete);

export default routes;
```

Em seguida ajustando o nosso arquivo server.ts para importar e inicializar as rotas conforme codigo abaixo:
```
import express from 'express';

import routes from './routes';

const app = express();
//depois de receber erro: TypeError: Cannot read property 'prop' of undefined 
app.use(express.json());
app.use(routes);
app.listen(3000, ()=>console.log("Serviço inicializado na porta 3000"));

```
Tudo configurado, hora de iniciar a nossa aplicação com o comando

```
yarn dev
```

## Todas migrations:

###### Endereço
```
import {MigrationInterface, QueryRunner,Table} from "typeorm";

export class CreateTabEndereco1622329380884 implements MigrationInterface {

    public async up(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.createTable( 
            new Table({
                name: "tab_endereco",
                columns:[
                    {name: "id", type: "integer",isPrimary: true, isGenerated: true, generationStrategy: "increment"},
                    {name: "numero", type: "varchar", length: "5"},
                    {name: "logradouro", type: "varchar", length: "50"},
                    {name: "cidade", type: "varchar", length: "50"},
                       
                ]
            })
        )
    }

    public async down(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.dropTable( "tab_endereco")
    }
}

```

###### Cliente
```
import {MigrationInterface, QueryRunner,TableForeignKey,Table} from "typeorm";

export class CreateTabCliente1622329396710 implements MigrationInterface {

    public async up(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.createTable( 
            new Table({
                name: "tab_cliente",
                columns:[
                    {name: "id", type: "integer",isPrimary: true, isGenerated: true, generationStrategy: "increment"},
                    {name: "cpf_cnpj", type: "varchar", length: "15", isNullable:false},
                    {name: "nome", type: "varchar", length: "50",isNullable:false},
                    {name: "ativo", type: "boolean", default: true, isNullable:false},
                    {name: "dt_inclusao", type: "timestamp", default: "now()"},
                    {name: "dt_alteracao", type: "timestamp", default: "now()"},
                    {name: "cd_endereco", type: "integer", length: "5"},
                        
                ]
            })
        )
         
        await queryRunner.createForeignKey("tab_cliente", new TableForeignKey({
         columnNames: ["cd_endereco"],
         referencedColumnNames: ["id"],
         referencedTableName: "tab_endereco",
         name:"fk_cliente_endereco"
     }));
 
    }
    
    public async down(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.dropTable( "tab_cliente")
    }

}
```

###### Cliente Telefone
```
import {MigrationInterface, QueryRunner, Table} from "typeorm";

export class CreateTabClienteTelefone1622329411279 implements MigrationInterface {

    public async up(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.createTable( 
            new Table({
                name: "tab_cliente_telefone",
                columns:[
                    {name: "id", type: "integer",isPrimary: true, isGenerated: true, generationStrategy: "increment"},
                    {name: "cd_cliente", type: "integer", length: "5"},
                    {name: "tipo", type: "varchar", length: "10"},
                    {name: "ddd", type: "integer", length: "3"},
                    {name: "numero", type: "integer", length: "10"},
                ]
            })
        )
    }
    public async down(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.dropTable( "tab_cliente_telefone")
    }
}
```

###### Produto
```
import {MigrationInterface, QueryRunner, Table} from "typeorm";

export class CreateTabProduto1622329420364 implements MigrationInterface {

    public async up(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.createTable( 
            new Table({
                name: "tab_produto",
                columns:[
                    {name: "id", type: "integer",isPrimary: true, isGenerated: true, generationStrategy: "increment"},
                    {name: "cd_barras", type: "varchar", length: "15"},
                    {name: "nome", type: "varchar", length: "50"},
                    {name: "vl_unit", type: "numeric", precision: 8, scale:2},
                ]
            })
        )
    }

    public async down(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.dropTable( "tab_produto")
    }
}

```

###### Pedido
```
import {MigrationInterface, QueryRunner,Table} from "typeorm";

export class CreateTabPedido1622329431612 implements MigrationInterface {

    public async up(queryRunner: QueryRunner): Promise<void> {
        
        await queryRunner.createTable( 
            new Table({
                name: "tab_pedido",
                columns:[
                    {name: "id", type: "integer",isPrimary: true, isGenerated: true, generationStrategy: "increment"},
                    {name: "cd_cliente", type: "integer", length: "5"},
                    {name: "dh_pedido", type: "timestamp"},
                    {name: "vl_total", type: "numeric", precision: 8, scale:2},
                ]
            })
        )
    
    }

    public async down(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.dropTable( "tab_pedido")
    }

}
```

###### Pedido Item
```
import {MigrationInterface, QueryRunner, Table} from "typeorm";

export class CreateTabPedidoItem1622329439796 implements MigrationInterface {

    public async up(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.createTable( 
            new Table({
                name: "tab_pedido_item",
                columns:[
                    {name: "id", type: "integer",isPrimary: true, isGenerated: true, generationStrategy: "increment"},
                    {name: "cd_produto", type: "integer", length: "5"},
                    {name: "quant", type: "numeric", precision: 8, scale:2},
                    {name: "vl_unit", type: "numeric", precision: 8, scale:2},
                    {name: "vl_total", type: "numeric", precision: 8, scale:2},
                    {name: "cd_pedido", type: "integer", length: "5"},
                ]
            })
        )
    }

    public async down(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.dropTable( "tab_pedido_item")
    }
}
```

## Todas entidades:

###### Endereço:

```
import {Column,Entity,PrimaryGeneratedColumn, BaseEntity} from "typeorm";

@Entity("tab_endereco")
export class Endereco extends BaseEntity {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    logradouro: string;
    
    @Column()
    numero: string;

    @Column()
    cidade: string;

}

```

###### Cliente:

```
import {Entity, Column, CreateDateColumn, UpdateDateColumn, 
    BaseEntity,PrimaryGeneratedColumn, OneToOne, JoinColumn,
    OneToMany 
    } from "typeorm";
import { ClienteTelefone } from "./ClienteTelefone";
import { Endereco } from "./Endereco";

@Entity("tab_cliente")
export class Cliente extends BaseEntity{
    @PrimaryGeneratedColumn()
    id: number;

    @Column({name:"cpf_cnpj"})
    cpfCnpj: string;

    @OneToOne(()=>Endereco, {cascade: true,eager: true})
    @JoinColumn({name:"cd_endereco"})
    endereco:Endereco;

    @Column()
    nome: string;
    
    @Column()
    ativo: boolean = true;
    
    
    @CreateDateColumn({name:"dt_inclusao"})
    dataInclusao: Date

    @UpdateDateColumn({name:"dt_alteracao"})
    dataAlteracao: Date   
    
    @OneToMany(() => ClienteTelefone, tel=> tel.cliente, {cascade: true, eager: true})
    telefones: ClienteTelefone[];
}

```

###### Cliente Telefone:

```
import {Column,Entity,PrimaryGeneratedColumn, BaseEntity,ManyToOne, JoinColumn} from "typeorm";
import { Cliente } from "./Cliente";
import { TelefoneTipo } from "./TelefoneTipo";

@Entity("tab_cliente_telefone")
export class ClienteTelefone extends BaseEntity {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    ddd: number;
    
    @Column()
    numero: number;

    @Column({
        type: "enum",
        enum: TelefoneTipo,
        name:"tipo"
    })
    tipo: TelefoneTipo;

    @ManyToOne(() => Cliente, cliente => cliente.telefones)
    @JoinColumn({name:"cd_cliente"})
    cliente: Cliente;
}

```

###### Telefone Tipo:

```
export enum TelefoneTipo {
    'FIXO',
    'CELULAR',
    'WHATSAPP'
  }

```

###### Pedido:

```
import {Entity, Column, 
    BaseEntity,PrimaryGeneratedColumn,OneToMany
    } from "typeorm";

    import { PedidoItem } from "./PedidoItem";
@Entity("tab_pedido")
export class Pedido extends BaseEntity{
    @PrimaryGeneratedColumn()
    id: number;

    @Column({name:"cd_cliente"})
    cliente: number;

    @Column({name:"dh_pedido"})
    dataHora: Date;

    @Column({name:"vl_total"})
    valorTotal: number;

    @OneToMany(() => PedidoItem, item=> item.pedido, {cascade: true, eager: true})
    itens: PedidoItem[];

}
```

###### Pedido Item:

```
import {Column,Entity,PrimaryGeneratedColumn, BaseEntity,ManyToOne, JoinColumn} from "typeorm";
import { Pedido } from "./Pedido";

@Entity("tab_pedido_item")
export class PedidoItem extends BaseEntity{
    @PrimaryGeneratedColumn()
    id: number;

    @Column({name:"cd_produto"})
    produto: number;

    @Column({name:"quant"})
    quantidade: number;

    @Column({name:"vl_unit"})
    valorUnitario: number;

    @Column({name:"vl_total"})
    subTotal: number;

    @ManyToOne(() => Pedido, pedido => pedido.itens)
    @JoinColumn({name:"cd_pedido"})
    pedido: Pedido;   
}

```



