## Configurando `Alias` no [.gitconfig]

O Alias no Git é uma função muito pratica para melhorar a produtividade dos desenvolvedores.

### Comandos: 

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
          ### Comandos Git Flow ###
        # fs = (git checkout develop && git pull && flow feature start)
        fs = "!f() { git checkout develop && git pull && git flow feature start \"$1\"; }; f"
        # fs = (git checkout develop && git pull && flow feature finish)
        ff = "!f() { git checkout develop && git pull && git flow feature finish \"$1\" && git push; }; f"
        #rs = flow release start
        rs = "!f() { git checkout develop && git pull && git flow release start \"$1\"; }; f"
        #rf = flow release finish
        rf ="!f() { git checkout develop && git pull && git checkout master && git pull && git flow release finish \"$1\" && git push && git checkout master && git push && git push --tag && git checkout develop; }; f"
        # hs = flow hotfix start
        hs = "!f() { git checkout develop && git pull && git checkout master && git pull && git flow hotfix start \"$1\"; }; f"
        # hf = flow hotfix finish
```

[.gitconfig]: <.gitconfig>

## Referencias:
- Diego RocketSet, https://www.youtube.com/watch?v=VpeU3VpszAc 
- Comandos Git Flow: https://br.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow
- 
