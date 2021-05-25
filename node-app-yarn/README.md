# Gama Academy - Transformando Talentos para o Futuro

#### Autores
- [Gleyson Sampaio](https://github.com/gleyson-gama)

Iniciando um projeto Node.JS com NPM e Yarn - No WINDOWS

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
2. Criar o arquivo `server.ts` dentro de `src`
