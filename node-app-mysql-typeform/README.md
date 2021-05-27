# Gama Academy - Transformando Talentos para o Futuro

## Node.JS - MySQL - ORM - TypeOrm

Melhoraremos a nossa de repositorio com o conceito de ORM com TypeOrm

Type ORM? [link](https://typeorm.io/#/)

Um recurso em Node.JS para disponibilizar umas das implementações do conceito ORM em conversão de dados em objetos e vice-versa .

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
 
