# Principais comando para utilizar Git-Flow

>O `git flow` se trata de padrão de desenvolvimento, onde é muito utilizado por equipes que trabalham em um mesmo projeto >simultaneamente. Com isso, ao utilizar um padrão de desenvolvimento evitamos `"acidentes"` entre as `branchs` do projeto.

## Um pouco sobre a estrutura que o Git Flow segue:

### **Branchs Padrões** (develop e master)

![Branchs Padrao](/configs/git-flow/images/estrutura_base.png)

>**Master**: 
Contem todo código já testado e versionado que será entregue ao cliente.
Réplica dos objetos de produção

>**Develop**: 
Branch do Desenvolvedor, contem o código mais atual desenvolvido.
Onde as outras branchs serão ramificadas tendo ela como base no momento da criação do "ramo".

### **Branch Feature**

![Branchs Feature](/configs/git-flow/images/branch_feature.png)

>**Feature**: 
É o ramo do fluxo criado para desenvolver `novas funcionalidades` para a aplicação ou para iniciar uma modificação da aplicação. Essa branch inicia de uma copia da branch `develop` e quando é concluída, ela é mesclada na `develop` novamente.

### **Branch Release**

![Branchs Release](/configs/git-flow/images/branch_release.png)

>**Release**: 
É o ramo do fluxo criado para `novas implementações` previamente `testadas` e `validadas`. 
A release é uma das únicas branches que mescla com a `master`.

## **Branch Hotfix**

![Branchs Hotfix](/configs/git-flow/images/branch_hotfix.png)

>**Hotfix**: 
É o ramo do fluxo criado para resolver `problemas críticos` em `produção` que não podem esperar novas releases.
Criado a partir da `master` e quando concluído é mesclado com `a develop` e a `master`. Garantindo que tanto o codigo de `produção` quanto o codigo do `Desenvolvedor` possuam a mesma correção do "`Bug`" aplicada no hotfix.

## **TAG**

![Branchs Hotfix](/configs/git-flow/images/tag.png)

>**TAG**: 
Após a conclusão de uma `feature` e a criação d `release` para *implantação* do seu programa é a hora de usar uma `TAG` para controlar a versão da aplicação.
A `TAG` pode ser comparada a um “`snapshot`” do código no momento de deploy na branch de produção (*master*). A `TAG` é criada automaticamente quando se finaliza uma `release` via `git flow` e ela ira receber o mesmo nome da `release` previamente finalizada.

## Primeiros comandos: 

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
