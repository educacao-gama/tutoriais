# Gama Academy - Transformando Talentos para o Futuro

#### Autores
- [Gleyson Sampaio](https://github.com/gleyson-gama)

MongoDB é um banco de dados de código aberto, gratuito, de alta performance, sem esquemas e orientado à documentos, lançado em fevereiro de 2009 pela empresa 10gen


Instalando o MongoDB: 
[windows](https://github.com/educacao-gama/tutoriais/tree/main/mongodb/windows)

Criando o banco de dados local com MongoDB Compass:
1. Localize o aplicativo MongoDBCompass
2. Clique em `Fill in connection fields individually` e deverá aparecer a tela abaixo, depois clique em `Connect`

![](https://github.com/educacao-gama/tutoriais/blob/main/mongodb/compass/connect.png)

3. Em seguida, criamos o banco de dados cliando no `CREATE DATABASE`, banco exemplo: `storedb`
4. Nesta etapa é necessário informar o nome do `Database` e a `Collection`
    1. databse: `storedb`
    2. collection: `products`

![](https://github.com/educacao-gama/tutoriais/blob/main/mongodb/compass/database.png)

![](https://github.com/educacao-gama/tutoriais/blob/main/mongodb/compass/collections.png)

![](https://github.com/educacao-gama/tutoriais/blob/main/mongodb/compass/sobre.png)

5. Hora de criar nossos `documents` (registros)

O cadastro de produtos serão livros e cd para demonstrar a estruturação de dados com estruturas diferentes:

LIVROS

* A ARCA DE NOÉ de Vinícius de Moraes
* A HISTÓRIA DA SOPEIRA E DA CONCHA de Michael Ende
* A RAINHA DA NEVE de Hans Christian Andersen
* CACHINHOS DE OURO de Ana Maria Machado
* CHAPEUZINHO E O LOBO MAU de Pedro Bandeira
* CONTOS DE PERRAULT de Ruth Rocha
* O GATO E O DIABO de James Joyce
* O PEQUENO VAMPIRO de Angela Sommer Bodenburg
* O SACI de Monteiro Lobato

CDS

* Xou da Xuxa de Xuxa
* Músicas para Louvar o Senhor	de Padre Marcelo Rossi
* Leandro & Leonardo de Leandro & Leonardo
* Rádio Pirata ao Vivo	de RPM	1986
* O Canto da Cidade	de Daniela Mercury
* Quatro Estações: O Show	de Sandy & Junior
* Só pra Contrariar	de Só Pra Contraria

Hora de inserir nossos livros e cds considerando a estrutura do nosso diagrama:

1. Analise o diagrama
2. Realizar a inserção de um novo documento para item de livro e cd citados acima
