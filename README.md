# Minicurso de Git
*Bruno Habermann*

Você pode consultar também os seguintes locais para ter uma visão geral sobre o git

[Git - Primeiros Passos][first_steps]
[Git - Guia Prático][guide]

## Iniciando um projeto com o GIT

```
git init -- inicializa a pasta para usar o git
git ls-files -- arquivos controlados
git status -- status de todos os arquivos no diretório
git add . -- adiciona os arquivos alterados
git commit -m "Promeiro commit" -- versiona a alteração com um comentário

git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"

git commit -am "Segundo commit" -- aglutina os comandos "add" e "commit -m"
```

#alterações efetuadas

git whatchanged -- lista os arquivos alterados
git whatchanged -p -- lista os arquivos alterados com as linhas alteradas também

# espelhar repositório na rede e enviar arquivos

git remote -- lista os repositorios remotos
git remote add origin URL -- o nome origin é uma convenção para nomear o repositório remoto

git push origin master -- enviar | qual servidor | qual branch

# clonar um repositório pronto

git clone URL

# branches

git branch -- lista branches
git branch nome_da_branch -- cria uma nova branch
git checkout nome_da_branch -- muda para a branch

git checkout -b nome_da_branch -- cria e altera para a branch

git branch -- para confirmarmos a branch que estamos (com *)

git branch -r -- lista as branches remotas

git branch -t nome_local origin/nome_remoto -- vincula a branch local à branch remota

git branch -d nome_da_branch -- remove a branch local


# Conflitos
* Merge automático se alterado em linhas diferentes
* MErge manual se alterada a mesma linha/bloco

# Boas práticas

## Rebase

Trabalhar sempre num branch de desenvolvimento local
git checkout -b desenvolvimento -- cria e entra na branch desenvolvimeto

Efetua os trabalhos todos nesta branch local *desenvolvimento*

git checkout master -- mudar para o branch master
git pull -- atualizar com as informações do repositório
git checkout desenvolvimento -- muda para o branch desenvolvimento
git rebase master [desenvolvimento] -- quando se está na branch que receberá o rebase, o último comando é opcional
git checkout master
git merge desenvolvimento
git push

### Possíveis problemas

Pode haver algum conflito no momento de efetuar o rebase, neste caso temos que resolver este conflito, de forma semelhante ao merge com o seguinte procedimento:

git rebase master -- deu erro

Corrigimos os conflitos e continuamos

git add [arquivos com conflito resolvidos]
git rebase --continue


# Controles avançados

git checkout "arquivo" -- volta arquivo não adicionado (git add)
git reset HEAD "arquivo" -- volta arquivo já adicionado (git add)

se já tiver efetuado o comit?

git reset {HASH} -- reseta(desfaz) todos os commits até o indentificador

desfazer um commit antigo

git revert {HASH} -- reverte somente o commit passado e cria um novo commit para gravar este reverte

guardar alterações não comitadas

git stash


# Facilidades

Alias para o rebase: Basta editar o arquivo `.gitconfig` na pasta de usuário do sistema e adicionar a seção [alias] com os apelidos desejados. Por exemplo:

[alias]
	envia = !git checkout master && git pull && git checkout desenvolvimento && git rebase master && git checkout master && git merge desenvolvimento && git push







# Atlassian

# Models

Anarchy -> Today

Gatekeeper -> Cada um tem um fork e avisa ao "mantenedor" que tem uma alteração, chamada pull request

Dictator and liutenants -> Pirâmide

Centralised -> Todos em um repositório centralisado
* Geralmente usado por companhias;
* Mais fácil com Issues Trackes e Ferramentas de Integração (CI)

# Branching model
1. Product Releas -> Versão 1, 2, 3 -> Long Term Support
	1.1. *Central* Repository
	1.2. One *Branch* per feature
	1.3. One *Branch* per bugfix
	1.4. *Stable* Branches (LTS)
	1.5. *master* is Alpha / RC
	1.6. *Pull Request*

2. Continuous Delivery -> Site, sem número de versão
	Software as a services, on demand
	Obs.: staging is a name of a branch
	2.1. *master* is in production
	2.2. *staging* is the next version
	2.3. new features off *staging*

# Common git Practices
## Pull Request
 -> Code review

## Single Repository vs Remote Forks

### Pros of a Single Repo
1. Complete Visibility
2. No per Dev remotes required

### Fork
1. Manage codebase *maturity*
2. X(cross) department and 3rd parties
3. Dev to Dev interactions (without sending to center server)

# Continuos Integration

## Full integration
1. What happens to CI with git
2. An explosion of branches
3. Performance degradation of build sys

## Selected Integration
1. Build everithing is expensive
2. Automatically build stable and master
3. Manually trigger feature branch builds


# Less Friction and Automation
* Code Quaility via pre-commit hooks -> Script running background
* Branch from green builds -> with checkout
* Automatic merges for the win
	Ripple *merges*
	Server side *update* hook
	Or *tool* support

Conclusion
Colaboration Model -> Centralized
Branching Model -> Product workflow
Adopt Git Practices -> Pull request / Single Repository
Automation & CI setup -> hooks (estudar)


[first_steps]:https://gist.github.com/adammacias/bb358a90a4f4cea50b41
[guide]:http://rogerdudler.github.io/git-guide/index.pt_BR.html