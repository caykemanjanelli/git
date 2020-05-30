# Principais comando para utilizar Git-Flow

>O git flow se trata de padrão de desenvolvimento, onde é muito utilizado por equipes que trabalham em um mesmo projeto >simultaneamente. Com isso, ao utilizar um padrão de desenvolvimento evitamos `"acidentes"` entre as `branchs` do projeto.

## Um pouco sobre a estrutura que o Git Flow segue:

### Branchs Padrões (develop e master)

![estutura_base] (/images/estrutura_base.PNG)

### Primeiros comandos :simple_smile:: 

**Iniciando um Repositorio como Git Flow**

Abra o terminal na pasta do projeto que deseja utilizar o `git flow` e execute o comando abaixo:

```sh
$ git flow init
```
Após executar o comando a cima, o git ira apresentar um conjunto de perguntas que são utilizadas no setup do git flow. Podemos usar as configurações padroes do proprio git flow, para isso basta apenas pressinar enter para todas as perguntas.

Retorno experado ao rodar o comando **git flow init**:
```
Which branch should be used for bringing forth production releases?
   - develop
   - master
Branch name for production releases: [master]

Which branch should be used for integration of the "next release"?
   - develop
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?

Feature branches? [feature/]
Bugfix branches? [bugfix/]
Release branches? [release/]
Hotfix branches? [hotfix/]

Support branches? [support/]

Version tag prefix? []
Hooks and filters directory? [C:/Users/<path_projeto>/preco/.git/hooks]
```
>**OBS**: Em algumas situações, quando não possuimos a branch `master` na hora do setup do `git flow init` o comando automatico pode se perder ao referenciar a branch master como branch de produção no arquivo de configuração do git flow, quando isso acontece nota-se que a primeira pergunta que aparece após executar o comando `git flow init` vem sem informação entre `[]`. Para resolver isso podemos apenas escrever o nome da branch que ira corresponder ao ambiente de produção. Ficaria assim: 

```
Which branch should be used for bringing forth production releases?
   - develop
Branch name for production releases: [] master

...
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
