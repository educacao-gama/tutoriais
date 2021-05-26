# Gama Academy - Transformando Talentos para o Futuro

## Node.JS - MySQL - KNex.JS

Hora de interagir com banco de dados para armazenar e obter as informações de nossa aplicação.

KNex.JS ?

Um módulo do Node.JS capaz de realizar interações de estrutura (DDL) e manipulação de registros  (DML) em uma base de dados relacional.

Migrations ?
É um recurso capaz de gerenciar a pasta estrutural do banco de dados como criação de tabelas, alteração de colunas e etc. Cada migration contem 2 métodos principais que são:

Up
Dentro dele é colocado tudo o que tem que ser criado no banco de dados. Ex: tabelas, inserts, selects e tudo mais.

Down
Já o Down é ao contrário do UP, tudo o que for feito na UP é desfeito na DOWN, criei uma tabela na UP, dou drop na DOWN

#### Autores
- [Gleyson Sampaio](https://github.com/gleyson-gama)

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
 1. E agora uma conferido em nossas dependências no arquivo `package.json`
 
  ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mysql-knex/knex-mysql.png)
