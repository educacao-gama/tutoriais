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

Após, realizar a configuração do serviço:

![](https://github.com/educacao-gama/tutoriais/blob/main/mongodb/windows/service_config.png)


Depois do git devidadamente instalado, vamos inicializar nosso primeiro repositório.

Em nosso exemplo, criamos um diretório em `C:\gama\[meu-repositorio]` e depois clicamos com o botão direito do mouse para abrirmos o `Git Bash`

![](https://github.com/educacao-gama/tutoriais/blob/main/git-github/git-bash.png)

No `Git Bash` iniciamos com o comando abaixo:

```
git init
```

Observe que dentro do diretório `C:\gama\[meu-repositorio]` será criado uma pasta oculta chamada de `.git` e no terminal além do diretório será acrescido a plavavra `(master)`

![](https://github.com/educacao-gama/tutoriais/blob/main/git-github/git-init.png)

Após este processo, vamos criar um arquivo chamado `file.txt` para testarmos a sincronização de nossos arquivos no GitHub.

PRONTO! Vamos aos comandos do git para sincronizar nossas alterações:

* Precisamos adicionar os documentos (forma mais abreviada):
```
git add .
```

* Geramos um lote (commit)  destas alterações informando uma mensagem correspondente:
```
git commit -m "incluindo o nosso arquivo file.txt"
```

* Esta seria a hora do `git push`, mas ainda precisamos criar nosso repositorio no GitHub acessando `https://github.com/`, faça o Login e depois crie o repositório com o nome de sua escolha.

> NOTA: O Github cria uma branch `main`, por isto precisamos realizar o comando que muda da branch `master` para a branch `main` e assim conseguirmos sincronizar o nosso reposítorio local com o remoto.

* Alterando branch `master` para `main` :
```
git branch -M main
```

![](https://github.com/educacao-gama/tutoriais/blob/main/git-github/branch-main.png)

* O comando abaixo determina qual repositório nossos arquivos serão sincronizados (NÃO quer dizer que já serão replicados)
```
git remote add origin https://github.com/educacao-gama/meu-repositorio.git (seu repositório)
```

* Ponto, agora é sincronizar as nossas alterações com o comando, esta fase vai ter pedir para informar o seu login e senha do GitHub.
```
git push -u origin main
```
* username

![](https://github.com/educacao-gama/tutoriais/blob/main/git-github/username.png)

* password

![](https://github.com/educacao-gama/tutoriais/blob/main/git-github/password.png)

* Validando a sincronização

![](https://github.com/educacao-gama/tutoriais/blob/main/git-github/push.png)


![](https://github.com/educacao-gama/tutoriais/blob/main/git-github/push-ok.png)

Clonando um repositório em nossa máquina: (Git bash)
```
git clone https://github.com/educacao-gama/meu-repositorio.git
```

Obtendo as alterações realizadas por outros membros do repositório: (Git bash)
```
git pull
```
NOTA: Você precisa estar no diretório que representa o seu repositório, o `Git bash` sinaliza a `branch` atual.

![](https://github.com/educacao-gama/tutoriais/blob/main/git-github/git-pull.png)




