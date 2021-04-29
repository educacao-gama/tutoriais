# Gama Academy - Transformando Talentos para o Futuro

#### Autores
- [Gleyson Sampaio](https://github.com/gleyson-gama)

O Git é um projeto de código aberto maduro e com manutenção ativa desenvolvido em 2005 por Linus Torvalds, o famoso criador do kernel do sistema operacional Linux. Um número impressionante de projetos de software depende do Git para controle de versão, incluindo projetos comerciais e de código-fonte aberto. Os desenvolvedores que trabalharam com o Git estão bem representados no pool de talentos de desenvolvimento de software disponíveis e funcionam bem em uma ampla variedade de sistemas operacionais e IDEs (Ambientes de Desenvolvimento Integrado).

###### https://www.atlassian.com/br/git/tutorials/what-is-git

Instalando o Git: (windows)

```
Acesse: https://git-scm.com/
```

![](https://github.com/educacao-gama/tutoriais/blob/main/git-github/git-download.png)


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

1. Precisamos adicionar os documentos (forma mais abreviada):
```
git add .
```

1. Geramos um lote (commit)  destas alterações informando uma mensagem correspondente:
```
git commit -m "incluindo o nosso arquivo file.txt"
```





