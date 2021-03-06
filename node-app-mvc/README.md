# Gama Academy - Transformando Talentos para o Futuro

## Node.JS - Padrão MVC

Refatorando nossa aplicação Node API de acordo com padrão MVC.

O que é MVC ?

Um padrão de desenvolvimento muito utilizado em desenvolvimento Web que divide as camadas de uma aplicação em Modelo (M), Visão (V), e Controle (C).

#### Autores
- [Gleyson Sampaio](https://github.com/gleyson-gama)

#### Requisitos
[Criando APIs simples com Node.JS](https://github.com/educacao-gama/tutoriais/tree/main/node-app-api)

Não se assuste quanto as alterações que teremos que realizar em nossa aplicação para torna-la conforme o padrão MVC, é por esta razão que é relevante conhecer de alguns padrãoes de desenvolvimento antes mesmo de implementar as funcionalidades de uma aplicação.
Então Vamos Neeessa ...

#### Vamos iniciar nossa estrutura de controle correspondente pela regra de negócio da aplicação
1. Criamos o novo diretório `src\controllers`
1. Na pasta `controllers` vamos incluir nossos Controllers iniciando pelo `CadastroController.ts` para incluir, alterar e listar os cadastros do sistema através de requisições HTTP.
 ```
   import { Request, Response } from 'express';
   export default {
       async list(req: Request, res: Response) {
           var result=[{id:1, cpf:"09329314058", nome:"JOSE DA SILVA"},{id:2, cpf:"01135196052", nome:"MARIA DE LOURDES"}];
           return res.status(200).json({ data:result});
       },
       async create(req: Request, res: Response) {
           const { nome, cpf} = req.body;
           const id=3;
           const data = {id,nome,cpf};
           return res.status(201).json({ data:data});
       },
       async update(req: Request, res: Response) {
           const { nome, cpf} = req.body;
           const dataAlteracao = '30/05/2021 16:00'
           const cadastro = {nome,cpf,dataAlteracao};
           cadastro.nome = "JOSE DA SILVA LIMA";
           return res.status(200).json({ data:cadastro});
       }
   }
   ```
 
 ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mvc/cadastro_controller.png)
 
1. Depois do nosso controle implementado precisaremos configurar uma rota para requisições HTTP, e seguindo as boas práticas de desenvolvimento iremos criar o arquivo `src\routes.ts` contendo uma rota para todos os recursos disponíveis em nossos Controllers.

 ```
  import { Router } from 'express';
  import CadastroController from './controllers/CadastroController';

   const routes = Router();

   routes.get('/cadastros', CadastroController.list);
   routes.post('/cadastros', CadastroController.create);
   routes.put('/cadastros', CadastroController.update);

   export default routes;

   ```
 ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mvc/routes-cadastro.png)
 
1. Antes de executar nossa aplicação, precisamos fazer alguns ajustes no arquivo `server.ts`.
   1. Primeiro remover a rota de teste com a mensagem de "Boas Vindas"
   1. Carregar a configuração das rotas na inicialização da aplicação.
   
   ```
   import express from 'express';

   import routes from './routes';

   const app = express();
   //depois de receber erro: TypeError: Cannot read property 'prop' of undefined 
   app.use(express.json());
   app.use(routes);
   app.listen(3000, ()=>console.log("Serviço inicializado na porta 3000"));

   ```
 ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-mvc/serverts.png)
 
 1. Tudo configurado, vamos testar a nossa API, com alguma client HTTP como Postman, Insomnia realizar as requisições abaixo:
    1. GET: http://localhost:3000/cadastros
    1. POST: http://localhost:3000/cadastros
    
       ```
       {"cpf":"18231108009","nome":"JOSE DA SILVA"}
       ```
    
    1. PUT: http://localhost:3000/cadastros

         ```
       {"cpf":"18231108009","nome":"JOSE DA SILVA LIMA"}
       ```
