# Gama Academy - Transformando Talentos para o Futuro

## Node.JS e Yarn

Iniciando um projeto Node.JS com NPM e Yarn - No WINDOWS

#### Autores
- [Gleyson Sampaio](https://github.com/gleyson-gama)


Instalando o Node.JS: (windows)

```
Acesse: https://nodejs.org/en/
```

![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-yarn/node_install.png)

Para validar se o Node.JS foi instalado, no prompt de commando execute
```
node -v
```
![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-yarn/node_version.png)

Instalando o yarn
```
npm install --global yarn
```
Verificando a instalação do yarn
```
yarn --version
```
![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-yarn/yarn.png)

Iniciando nosso projeto gama-xp-app com yarn

1. Crie um diretorio gama-xp-app
1. No prompt de comando dentro da pasta {SEU_DIRETORIO}\gama-xp-app execute o comando abaixo
```
yarn init
```
Serão realizadas algumas perguntas relacionadas ao projeto como nome do projeto, version, nome do autor.

Muitas das aplicações em Node.JS trabalham com a finalidade de prover APIs, logo precisaremos instalar o express para obter alguns de seus recursos.
```
yarn add express
```
Abaixo segue imagem de estrutura do projeto

![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-yarn/gama-xp-app.png)

Vale lembrar que todos os comandos `npm` ou `yarn` manipulam o arquivo `package.json` que é o arquivo central de qualquer aplicação Node.JS

Primeiros passos para implementação do projeto:
1. Criar a pasta `src` no mesmo nível do arquivo `package.json`
1. Criar o arquivo `server.ts` dentro de `src`
1. A partir de agora toda nossa sintaxe será escrita em JavaScript com a convenção do TypeScript, para isso é necessário executar o comando
   ```
    yarn add typescript -D
   ```
   -D: dependência de desenvolvimento
1. Para que nosso projeto tenha compatibilidade com a sintaxe do TypeScript precisaremos executar o comando
    ```
    yarn tsc --init
    ```
    ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-yarn/node_typescript.png)
    
1. Para finalizar nossa configuração, precisamos adicionar recursos de inicialização e reload da aplicação em tempo de desenvolvimento.
   ```
   yarn add ts-node-dev -D
   ```
   ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-yarn/tsnode.png)


1. Criando script de incialização da aplicação com `ts-node`, incluindo a tags `scripts` no arquivo `package.json`
   ```
    "scripts": {
        "dev":"ts-node-dev src/server.ts"
     },
   ```
   ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-yarn/tsnode-scripts-dev.png)
   
1. A partir de agora vamos iniciar com a codificação baseada em nossas bibliotecas como `express`, `typescript` e etc, logo precisamos adicionar mais uma dependência.
   ```
   yarn add @types/express -D
   ```
   ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-yarn/types_express.png)
   
1. No arquivo `src\server.ts` vamos iniciar nosso algorítimo para execução uma aplicação Node na porta 3000.
    ```
   import express from 'express';

   const app = express();

   app.listen(3000, ()=>console.log("Serviço inicializado na porta 3000"));
   ```
   ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-yarn/server-ts.png)
   
1. Iniciando nosso servidor na porta 3000.
   ```
   yarn dev
   ```
    ![](https://github.com/educacao-gama/tutoriais/blob/main/node-app-yarn/yarnd-dev.png)
