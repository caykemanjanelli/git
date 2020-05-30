## Configurando `Alias` no [.gitconfig]

O Alias no Git é uma função muito pratica para melhorar a produtividade dos desenvolvedores.

### Comandos: 

**- git ca**

Comando para adicionar os arquivo alterados na stage do git e para commitar as alterações. 

Exemplo do Comando:
```sh
$ git add .
$ git commit -m "fix: Arrumando bug de conexão"
```
Agora adicionando o alias no arquivo de .gitconfig:

```sh
[alias]
        ca = !git add . && git commit -m
```
Exemplo de utilização do alias:
```sh
$ git ca "fix: Arrumando bug de conexão"
```
**- git st**

Comando para exibir o status do arquivos na sua Work tree do Git, um alias. 

Exemplo do Comando:
```sh
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   configs/README.md

no changes added to commit (use "git add" and/or "git commit -a")
```
Agora adicionando o alias no arquivo de .gitconfig:

```sh
[alias]
        st = status -sb
```
Exemplo de utilização do alias:
```sh
$ git st
## master...origin/master
 M configs/README.mds
```

**- git cb**

Comando para criar uma branch e já realizar o checkout da branch criada. 

Exemplo do Comando:
```sh
$ git branch feature/performance
$ git checkout feature/performance
Switched to a new branch 'feature/performance'
```
Agora adicionando o alias no arquivo de .gitconfig:

```sh
[alias]
        cb = checkout -b
```
Exemplo de utilização do alias:
```sh
$ git cb feature/performance
Switched to a new branch 'feature/performance'
```

**- git lg**

Comando para listar os Logs de commit com o id mnemônico do commit, a quanto tempo foi commitado, nome do Dev, subject do commit. 
```sh
[alias]
        lg = log --pretty=format:'%Cred%h%Creset %C(bold)%cr%Creset %Cgreen<%an>%Creset %s' --max-count=30
```
Exemplo de utilização do Comando:
```sh
$ git lg

a5b4863 2 hours ago <Cayke Manjanelli > Update README.md
8db8393 24 hours ago <Cayke Manjanelli> Ajustando algumas coisas...
969cd61 2 days ago <Francisco> ajuste git esteira
```

**- git sf**

Comando exibir detalhes de um commit, de uma forma mais simples, contendo apenas os arquivos quer foram modificados no commit informado. 

Exemplo do Comando:
```sh
$ git show 911be27
commit 911be2766422e274fe438ea85a1807083154d883 (HEAD -> master)
Author: Cayke Xavier <cayke.xavier@cea.com.br>
Date:   Sat May 30 13:55:25 2020 -0300

    doc: Atualizando documentação dos alias para git

diff --git a/configs/README.md b/configs/README.md
index 9b6f010..abee03b 100644
--- a/configs/README.md
+++ b/configs/README.md
@@ -4,16 +4,87 @@ O Alias no Git é uma função muito pratica para melhorar a produtividade dos d

 ### Comandos:

+**- git ca**
+
+Comando para adicionar os arquivo alterados na stage do git e para commitar as alterações.
+
+Exemplo do Comando:
+```sh
+$ git add .
+$ git commit -m "fix: Arrumando bug de conexão"
+```
+Agora adicionando o alias no arquivo de .gitconfig:
+
+```sh
+[alias]
+        ca = !git add . && git commit -m
+```
+Exemplo de utilização do alias:
+```sh
+$ git ca "fix: Arrumando bug de conexão"
+```
```
Agora adicionando o alias no arquivo de .gitconfig:

```sh
[alias]
        sf = show --name-only
```
Exemplo de utilização do alias:
```sh
$ git sf 911be27
commit 911be2766422e274fe438ea85a1807083154d883 (HEAD -> master)
Author: Cayke Xavier <cayke.xavier@cea.com.br>
Date:   Sat May 30 13:55:25 2020 -0300

    doc: Atualizando documentação dos alias para git

configs/README.md
```

**- git incoming**

Comando para listar as alterações que estão no `remoto` e ainda não foram feito `pull` para o `local`. 
```sh
[alias]
        incoming = !(git fetch --quiet && git log --pretty=format:'%C(yellow)%h %C(white)- %C(red)%an %C(white)- %C(cyan)%d%Creset %s %C(white)- %ar%Creset' ..@{u})
```
Exemplo de utilização do Comando:
```sh
$ git incoming

f0c56b4 - Diego Luisi -  (origin/develop) [openshift] reduce memory request 100 to 50 - 2 days ago

```
**- git outgoing**

Comando para listar as alterações que estão no `local` e ainda não foram feito `push` para o `remoto`. 
```sh
[alias]
        outgoing = !(git fetch --quiet && git log --pretty=format:'%C(yellow)%h %C(white)- %C(red)%an %C(white)- %C(cyan)%d%Creset %s %C(white)- %ar%Creset' @{u}..)
```
Exemplo de utilização do Comando:
```sh
$ git outgoing

70b03cc - Cayke Xavier -  (HEAD -> master) docs: Incluindo explicações dos alias usados - 6 seconds ago
```
**- git unstage**

Comando para remover um arquivo da Stage area, logo após adicionar o arquivo com o comando `git add .` caso queira remover esse arquivo da stage pois ele não precisa ir no proximo commit.  
```sh
[alias]
        unstage = reset HEAD --
```
Exemplo de utilização do Comando:
```sh
$ git unstage readme.md
Unstaged changes after reset:
M       configs/README.md
```
**- git undo**

Comando para desfazer a modificação feita no arquivo, ele volta para ultima versão do arquivo antes da modificação não `commitada`.  
```sh
[alias]
        undo = checkout --
```
Exemplo de utilização do Comando:
```sh
$ git undo README.md
```
**- git rollback**

Comando para desfazer o ultimo commit, sem remover o arquivo, o comando deixa o arquivo que esta no ultimo commit como um arquivo fora da stage no seu repositorio local. Isso pode ser utilizado caso você esqueça de colocar algum conteudo nos arquivos antes do commit, para que todas as alterações estejam no mesmo commit.  
```sh
[alias]
        rollback = reset --soft HEAD~1
```
Exemplo de utilização do Comando:
```sh
$ git rollback
```

**- git who**

Comando para listar as ultimas pessoas que alteraram o projeto e a quantidade de linhas alteradas. 
```sh
[alias]
        who = shortlog -n -s --no-merges
```
Exemplo de utilização do Comando:
```sh
$ git who
    87  Cayke Manjanelli
    24  Ricardo Silva
    13  Cayke Xavier
     6  Jefferson Costa
     5  João Carvalho
```


**Configuração:**

Para configurar os Alias no seu git local, acesse o terminal e edite o arquivo .gitconfig executando o comando abaixo:
Abra o terminal/gitBash:
```sh
$ vim ~/.gitconfig
```

```sh
[user]
        name = Seu Nome
        email = seu.email@email.com

[alias]
        ci = commit
        ca = !git add . && git commit -m
        co = checkout
        cm = checkout master
        cd = checkout develop
        cb = checkout -b
        br = branch
        st = status -sb
        sf = show --name-only
        lg = log --pretty=format:'%Cred%h%Creset %C(bold)%cr%Creset %Cgreen<%an>%Creset %s' --max-count=30
        incoming = !(git fetch --quiet && git log --pretty=format:'%C(yellow)%h %C(white)- %C(red)%an %C(white)- %C(cyan)%d%Creset %s %C(white)- %ar%Creset' ..@{u})
        outgoing = !(git fetch --quiet && git log --pretty=format:'%C(yellow)%h %C(white)- %C(red)%an %C(white)- %C(cyan)%d%Creset %s %C(white)- %ar%Creset' @{u}..)
        unstage = reset HEAD --
        undo = checkout --
        rollback = reset --soft HEAD~1
        who = shortlog -n -s --no-merges
        say = "!f() { msg=${1-Hello World}; echo $msg;  }; f"
```

[.gitconfig]: <.gitconfig>

## Referencias:
- Diego RocketSet, https://www.youtube.com/watch?v=VpeU3VpszAc 
- 
