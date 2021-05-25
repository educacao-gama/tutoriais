# Gama Academy - Transformando Talentos para o Futuro

## Node.JS - APIs

Criando APIs simples com Node.JS

#### Autores
- [Gleyson Sampaio](https://github.com/gleyson-gama)

#### Requisitos
[Iniciando um projeto Node.JS com NPM e Yarn - No WINDOWS](https://github.com/educacao-gama/tutoriais/tree/main/node-app-yarn)

Com base no nosso projeto Node.JS com Yarn iremos criaremos rotas ou serviços APIs para gerenciamento de filmes conforme dados ilustrativos abaixo.

![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-api/filme.png)

###### Fonte: https://www.adorocinema.com/filmes/filme-268680/


Conhecendo um pouco sobre o que é API Rest.
API Rest é uma interface que possibilidade a interação entre sistemas tranferindo conteúdo em possíveis formatos como: JSON, XML, TEXT etc.
Esta interação são requisições de criação de conteúdo: POST, alteração: PUT, buscas: GET, remoção: DELETE entre outras.
Conheça um pouco mais sobre Arquitetura REST, Restfull, APIs

Criando nossa primeira rota \ serviço para retornar uma mensagem no formato `.json` com a seguinte estrutura:

1. No arquivo `src\server.ts` vamos incluir nossa rota do tipo `GET` para retornar a mensagem com a estrutura abaixo:
   ```
    import express, { request, response } from 'express';

    const app = express();

    app.listen(3000, ()=>console.log("Serviço inicializado na porta 3000"));

    app.get("/",(request, response) => {
        return response.json({mensagem:"Bem-vindes ao Gama - XP", ano:2021});
    });
   ```
   
  ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-api/get-mensagem.png)

1. Acessando a URL: `http://localhost:3000/` deverá ser apresentando a mensagem abaixo: 
   ```
   {"mensagem":"Bem-vindes ao Gama - XP","ano":2021}
   ```



