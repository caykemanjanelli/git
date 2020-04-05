# GIT - Comandos / Dicas

### PROPÓSITO

> Compartilhar comandos e dicas faceis e rapidas.

## Dicas :
### Configurando `Alias` no .gitconfig

O Alias no Git é uma função muito pratica para melhorar a produtividade dos desenvolvedores.

**Configuração:**

Acesse o terminal e edite o arquivo .gitconfig
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

## Referencias:
