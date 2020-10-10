# Principais comando para utilizar Git-Flow

>O `git flow` se trata de padrão de desenvolvimento, onde é muito utilizado por equipes que trabalham em um mesmo projeto simultaneamente. Com isso, ao utilizar um padrão de desenvolvimento evitamos `"acidentes"` entre as `branchs` do projeto.

## Um pouco sobre a estrutura que o Git Flow segue:

### **Branchs Padrões** (develop e master)
</p>
<img src = "https://raw.githubusercontent.com/caykemanjanelli/git/master/git-flow/images/estrutura_base.jpg">
</p>

Sem html
![](https://raw.githubusercontent.com/caykemanjanelli/git/master/git-flow/images/estrutura_base.jpg)

>**Master**: 
Contem todo código já testado e versionado que será entregue ao cliente.
Réplica dos objetos de produção

>**Develop**: 
Branch do Desenvolvedor, contem o código mais atual desenvolvido.
Onde as outras branchs serão ramificadas tendo ela como base no momento da criação do "ramo".

### **Branch Feature**

</p>
<img src = "https://raw.githubusercontent.com/caykemanjanelli/git/master/git-flow/images/branch_feature.png">
</p>

>**Feature**: 
É o ramo do fluxo criado para desenvolver `novas funcionalidades` para a aplicação ou para iniciar uma modificação da aplicação. Essa branch inicia de uma copia da branch `develop` e quando é concluída, ela é mesclada na `develop` novamente.

### **Branch Release**

</p>
<img src = "https://raw.githubusercontent.com/caykemanjanelli/git/master/git-flow/images/branch_release.png">
</p>

>**Release**: 
É o ramo do fluxo criado para `novas implementações` previamente `testadas` e `validadas`. 
A release é uma das únicas branches que mescla com a `master`.

## **Branch Hotfix**

</p>
<img src = "https://raw.githubusercontent.com/caykemanjanelli/git/master/git-flow/images/branch_hotfix.png">
</p>

>**Hotfix**: 
É o ramo do fluxo criado para resolver `problemas críticos` em `produção` que não podem esperar novas releases.
Criado a partir da `master` e quando concluído é mesclado com `a develop` e a `master`. Garantindo que tanto o codigo de `produção` quanto o codigo do `Desenvolvedor` possuam a mesma correção do "`Bug`" aplicada no hotfix.

## **TAG**

</p>
<img src = "https://raw.githubusercontent.com/caykemanjanelli/git/master/git-flow/images/tag.png">
</p>

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

**`Feature` - Criando uma nova Branch para desenvolvimento**

Branch de `desenvolvimento`, uma branch aberta para desenvolver novas funcionalidades para a aplicação, quando aberta ela ira fazer uma copia da `branch develop` e quando finalizada o codigo volta via merge para a branch `develop`, para isso é preciso ter garantido que o seu git `local` esteja atualizado com a ultima versão do repositorio `remoto`.

Abra o terminal/gitbash ou qualquer gerenciador que estive usando e execute os comandos abaixo:

```sh
$ echo "Atualizando sua branch local"
$ git checkout develop
$ git pull
```
Comando para iniciar uma nova feature:

```sh
$ echo "Abrindo uma nova Feature, um novo desenvolvimento"
$ git flow feature start nova-funcionalidade
$ echo "Trabalhe no desenvolvimento e no termino do mesmo, após homologado e pronto para implantação execute o comando abaixo"
$ git add .
$ git commit -m "<Mensagem descritiva do foi desenvolvido>"
$ git flow feature finish nova-funcionalidade
```
Para garantir que a feature foi finalizada com sucesso execute o comando abaixo, o mesmo não devera retornar a feature fechada

```sh
$ git branch -a
 develop
 master
```
Não esqueça que o `git flow` é uma funcionalidade `local`, devido a isso é preciso sempre que finalizado uma branch persistir a mesma no `repositorio remoto`, com o comando abaixo:

 ```sh
$ git checkout develop
$ git push --set-upstream origin develop
```

**`Release` - Criando uma nova Branch para Deploy da Aplicação**

Branch de *`Deploy`*, uma branch aberta para implantação das novas funcionalidades. A branch `release` acaba sendo o caminho que se passa via `git flow` para implantação de um novo conjunto de funcionalidades desenvolvidas por `features` passadas que ja foram finalizadas e *mergiadas* para a `develop`.
A branch `release` ao ser aberta realiza uma `copia` da branch `develop` e ao ser finalizada ela realiza um merge com a branch `master` e `develop` novamente, criando também uma `tag` do pacote que esta sendo implantado.
Usando a mesma dinamica antes de iniciar uma feature, é preciso garantir que o seu repositorio `local` esteja com a ultima versão do codigo presente no repositorio `remoto`, para isso execute o comando abaixo:

Abra o terminal/gitbash ou qualquer gerenciador que estive usando e execute os comandos abaixo:

```sh
$ git checkout master 
$ git pull
$ git checkout develop 
$ git pull
```
Antes de abrir uma `release` pode-se validar quais foram as ultimas "`releases`" implantadas, pois como ao finalizar a release o `git flow` abre uma `tag` automaticamente com o nome que foi dada na `release`, execute o comando abaixo para validar as `tags` existentes.

```sh
$ git tag
 0.0.1
 0.0.2
```
Após validado as tags existentes, podemos seguir com a abertura da nova `release`, para isso execute os comandos abaixo: 

```sh
$ echo "Abrindo uma nova release"
$ git flow release start 0.0.3
$ git flow release finish 0.0.3
```
Agora precisamos atualizar o repositorio `remoto`, para isso execute o comando abaixo:
```sh
$ git checkout master 
$ git push --set-upstream origin master
$ git push --tag
$ git checkout develop 
$ git push
```
Para garantir que a feature foi finalizada com sucesso execute o comando abaixo, o mesmo não devera retornar a feature fechada

```sh
$ git branch -a
 develop
 master
```
**`Hotfix` - Criando uma nova Branch para correção de BUG**

Branch de `correção de Bug`, uma branch aberta para `correção` de alguma `problema` encontrado em `produção`, como se trata de algo pontual que muitas vezes não se caracteriza como uma nova funcionalidade, podemos abrir uma branch de `hotfix`, onde ela ira nascer de uma copia da branch `master` e ao finalizar ira *mergiar* com a branch `master` e `develop`, garantindo que a correção tambem esteja presente na branch do `desenvolvedor`.
Como na branch `release`, ao abrir um `hotfix` é criado uma `tag` do codigo que esta sendo implantado.
Usando a mesma dinamica anterior, é preciso garantir que o seu repositorio `local` esteja com a ultima versão do codigo presente no repositorio `remoto`, para isso execute o comando abaixo:

Abra o terminal/gitbash ou qualquer gerenciador que estive usando e execute os comandos abaixo:

```sh
$ git checkout master 
$ git pull
$ git checkout develop 
$ git pull
```
Antes de abrir um `hotfix` pode-se validar quais foram as ultimas `tags` implantadas para que com isso possamos seguir uma logica de criação das versões.

```sh
$ git tag
 0.0.1
 0.0.2
 0.0.3
```
Após atualzado o repositorio local, podemos seguir com a abertura do novo `hotfix`, para isso execute os comandos abaixo: 

```sh
$ echo "Abrindo um novo Hotfix"
$ git flow hotfix start 0.1.3
$ git flow hotfix finish 0.1.3
```
##Dicas:

Os comando de `git flow` já são um conjunto de `alias` para reduzir a quantidade de comando a serem executados para respeitar o `fluxo` proposto. Mesmo assim são muitos comandos para digitar ou até lembrar, com isso resolvi criar alguns alias dos comandos de `git flow`. 

[Alias git flow](README-ALIAS.md) 

## Referencias:
- Comandos Git Flow: https://br.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow 
