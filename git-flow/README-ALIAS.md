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
- Comandos Git Flow: https://br.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow
- 
