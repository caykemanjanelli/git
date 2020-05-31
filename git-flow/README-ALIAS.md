## Configurando `Alias` no [.gitconfig] para **Git Flow**

O `Alias` no Git é uma função muito pratica para melhorar a `produtividade` dos desenvolvedores, com isso criei alguns `alias` para comandos de `git flow`, o que ira facilitar muito a vida.

Caso queira saber mais sobre gitFlow, [clique aqui](README.md).

### Explicando um pouco dos comandos: 

**- git fs**

Alias para iniciar uma nova `feature`, o comando já atualiza o repositorio `local` da branch `develop` antes de abrir a `feature`. 

Exemplo do Comando que o alias ira substituir:
```sh
$ git checkout develop
$ git pull
$ git flow feature start nova-funcionalidade
```
Agora adicionando o alias no arquivo de .gitconfig:

```sh
[alias]
        fs = "!f() { git checkout develop && git pull && git flow feature start \"$1\"; }; f"
	
```
Exemplo de utilização do alias:
```sh
$ git fs nova-funcionalidade
```
**- git ff**

Alias para finalizar uma nova `feature`, o comando já atualiza o repositorio `local` da branch `develop` antes de fechar a `feature` e após fechada ira atualizar o repositorio `remoto`. 

Exemplo do Comando que o alias ira substituir:
```sh
$ git checkout develop
$ git pull
$ git flow feature finish nova-funcionalidade
$ git push
```
Agora adicionando o alias no arquivo de .gitconfig:

```sh
[alias]
        ff = "!f() { git checkout develop && git pull && git flow feature finish \"$1\" && git push; }; f"
	
```
Exemplo de utilização do alias:
```sh
$ git ff nova-funcionalidade
```
**- git rs**

Alias para iniciar uma nova `release`, o comando já atualiza o repositorio `local` da branch `develop` antes de abrir a `release`.

Exemplo do Comando que o alias ira substituir:
```sh
$ git checkout develop
$ git pull
$ git flow release start 0.0.3
```
Agora adicionando o alias no arquivo de .gitconfig:

```sh
[alias]
        rs = "!f() { git checkout develop && git pull && git flow release start \"$1\"; }; f"
	
```
Exemplo de utilização do alias:
```sh
$ git rs 0.0.3
```
**- git rf**

Alias para finalizar uma nova `release`, o comando já atualiza o repositorio `local` da branch `develop` e da branch `master` antes de fechar a `release`.  Após fechada ira atualizar os repositorios `remotos`, tanto da `develop`, `master` e empurra a `tag` para o repositorio `remoto`.

Exemplo do Comando que o alias ira substituir:
```sh
$ git checkout develop
$ git pull
$ git checkout master
$ git pull
$ git flow finish 0.0.3
$ git push
$ git checkout master
$ git push
$ git push --tag
$ git checkout develop
```
Agora adicionando o alias no arquivo de .gitconfig:

```sh
[alias]
        rf ="!f() { git checkout develop && git pull && git checkout master && git pull && git flow release finish \"$1\" && git push && git checkout master && git push && git push --tag && git checkout develop; }; f"
	
```
Exemplo de utilização do alias:
```sh
$ git rf 0.0.3
```
**- git hs**

Alias para iniciar um novo `hotfix`, o comando já atualiza o repositorio `local` da branch `develop` e da branch `master` antes de abrir o `hotfix`.

Exemplo do Comando que o alias ira substituir:
```sh
$ git checkout develop
$ git pull
$ git checkout master
$ git pull
$ git flow hotfix start 0.1.3
```
Agora adicionando o alias no arquivo de .gitconfig:

```sh
[alias]
        hs = "!f() { git checkout develop && git pull && git checkout master && git pull && git flow hotfix start \"$1\"; }; f"
	
```
Exemplo de utilização do alias:
```sh
$ git hs 0.1.3
```
**- git hf**

Alias para finalizar um novo `hotfix`, o comando já atualiza o repositorio `local` da branch `develop` e da branch `master` antes de fechar o `hotfix`.  Após fechada ira atualizar os repositorios `remotos`, tanto da `develop`, `master` e empurra a `tag` para o repositorio `remoto`.

Exemplo do Comando que o alias ira substituir:
```sh
$ git checkout develop
$ git pull
$ git checkout master
$ git pull
$ git flow finish 0.1.3
$ git push
$ git checkout master
$ git push
$ git push --tag
$ git checkout develop
```
Agora adicionando o alias no arquivo de .gitconfig:

```sh
[alias]
        hf = "!f() { git checkout develop && git pull && git checkout master && git pull && git flow hotfix finish \"$1\" && git push && git checkout master && git push && git push --tag && git checkout develop; }; f"

```
Exemplo de utilização do alias:
```sh
$ git hf 0.1.3
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
Arquivo de .gitconfig: [.gitconfig](.gitconfig)

## Referencias:
- Comandos Git Flow: https://br.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow
- 
