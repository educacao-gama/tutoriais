# Gama Academy - Transformando Talentos para o Futuro

#### Autores
- [Gleyson Sampaio](https://github.com/gleyson-gama)

MongoDB é um banco de dados de código aberto, gratuito, de alta performance, sem esquemas e orientado à documentos, lançado em fevereiro de 2009 pela empresa 10gen


Instalando o MongoDB: (windows)

```
Acesse: https://www.mongodb.com/try/download/community
```

Você deve selecionar a opção On-promisses e realizar o download conforme imagem abaixo

![](https://github.com/educacao-gama/tutoriais/blob/main/mongodb/windows/install.png)

Em seguida o famosso install com Next, Next e aceitar o termos de licença, até chegar em `Chose Setupe Type` e selecione `Complete` para realizar a instalação padrão.

Após, realizar a configuração do serviço:

![](https://github.com/educacao-gama/tutoriais/blob/main/mongodb/windows/service_config.png)

Depois habilidar o Mongo Compass

![](https://github.com/educacao-gama/tutoriais/blob/main/mongodb/windows/mongo_compass.png)

Iniciando o serviço com o Mongo Compass

![](https://github.com/educacao-gama/tutoriais/blob/main/mongodb/windows/settings.png)

Instalando o Mongo Database Tools

![](https://github.com/educacao-gama/tutoriais/blob/main/mongodb/windows/database_tools.png)

Em seguida o famosso install com Next, Next e aceitar o termos de licença and Finish.

Hora de configurar as variáveis de ambiente no Windows
1. Localize aonde está instalado o MongoDB no Windows : C:\Program Files\MongoDB\Server\5.0\bin (ver versão)
2. Localize meu computador -> propriedades -> configurações avançadas do sistema -> ABA Avançado -> Variáveis de ambiente
3. Localize a variável de SISTEMA Path, clicar em Editar e adicionar a o caminho do Mongo C:\Program Files\MongoDB\Server\5.0\bin (ver versão)
4. Agora, abra o Prompt de Comando - CMD, digite mongo e se tudo estiver OK, receberá o log abaixo:

Realize o mesmo processo de configuração para Mongo Tools nas variáveis de ambiente no Windows
1. Adicione na variável Path - C:\Program Files\MongoDB\Tools\100\bin

![](https://github.com/educacao-gama/tutoriais/blob/main/mongodb/windows/mongo-cmd.png)

