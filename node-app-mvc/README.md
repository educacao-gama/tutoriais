# Gama Academy - Transformando Talentos para o Futuro

## Node.JS - Padrão MVC

Refatorando nossa aplicação Node API de acordo com padrão MVC.

O que é MVC ?

Um padrão de desenvolvimento muito utilizado em desenvolvimento Web que divide as camadas de uma aplicação em Modelo(M), Visão (V), e Controle(C).


#### Autores
- [Gleyson Sampaio](https://github.com/gleyson-gama)

#### Requisitos
[Criando APIs simples com Node.JS](https://github.com/educacao-gama/tutoriais/tree/main/node-app-api)

Não se assuste quanto as alterações que teremos que realizar em nossa aplicação para torna-la conforme o padrão MVC, é por esta razão que é relevante conhecer de alguns padrãoes de desenvolvimento antes mesmo de implementar as funcionalidades de uma aplicação.
Então Vamos Neeessa ...

#### Vamos iniciar nossa estrutura de controle correspondente pela regra de negócio da aplicação
1. Criamos o novo diretório `src\controllers`
1. Na pasta `controllers` vamos incluir nossos Controllers iniciando pelo `CadastroController.ts` para incluir, alterar e listar os cadastros do sistema através de requisições HTTP.
 %%%¨%¨% codigo
1. Depois do nosso controle implementado precisaremos configurar uma rota para requisições HTTP, e seguindo as boas práticas de desenvolvimento iremos criar o arquivo `src\routes.ts` contendo uma rota para todos os recursos disponíveis em nossos Controllers.
1. Antes de executar nossa aplicação, precisamos fazer alguns ajustes no arquivo `server.ts`.
   1. Primeiro remover a rota de teste com a mensagem de "Boas Vindas"
   1. Carregar a configuração das rotas na inicialização da aplicação.    
