# Soluções para problemas comuns

O *git* é um software bem complexo de ser utilizado devido ao seu grande número de funcionalidades e à complexidade de algumas dessas funcionalidades. Portanto, é bem comum que alguns problemas apareçam durante a sua utilização como software de controle de versão em projetos da Struct. Para facilitar o trabalho dos membros da Struct, alguns dos problemas mais comuns que podem ocorrer durante o uso desse software foram detalhados abaixo junto com as soluções para esses problemas.

Para descrever esses problemas e alguns dos comandos utilizados, vamos assumir que o leitor possui um conhecimento básico de *git*. Caso esse não seja o caso, procure visitar a seção do Gitbook sobre [conceitos básicos de git](./conceitos-basicos.md).

## Problemas com o último *commit* feito

Ao criar um *commit*, nem sempre fazemos exatamente o que queríamos fazer. Às vezes o *commit* feito inclui arquivos que não deveriam ter sido incluídos, ou não possui todos os arquivos que deveriam ser incluídos. Em outras vezes, o *commit* ocorre antes da realização de um *merge* importante. E, mais raramente, queremos consertar a mensagem de *commit* que criamos. Nesses casos, o usuário possui duas opções para solucionar seus problemas: desfazer o *commit* feito ou emendar o *commit* feito.

Tenha **muito cuidado** ao desfazer ou modificar o último *commit* realizado! Caso o *commit* já tenha sido enviado em um *push* para o repositório remoto, qualquer modificação no seu histórico de *commits* pode levar a uma situação em que o conflito entre sua *branch* local e a *branch* remota tenha que ser resolvido pela criação de uma nova branch ou por um *force pull* ou *force push* \(esses dois últimos devem ser evitados sempre que possível e realizados com **muita** cautela\).

### Como desfazer o último *commit* feito

Para desfazer o último *commit* feito, utilize o comando `git reset [--soft | --mixed] HEAD~1`.

A flag `--soft` desfará o último *commit* fazendo com que as mudanças dele sejam colocadas diretamente na *staging area*. A flag `--mixed` desfará o último *commit* fazendo com que as mudanças dele sejam mantidas, mas colocadas fora da *staging area*.

*Importante:* **Não** é recomendado a utilização da flag `--hard`, pois ela **apagará definitivamente** qualquer mudança em relação ao *commit* escolhido, incluindo **possíveis mudanças não relacionadas ao _commit_ desfeito que ainda não foram salvas em um _commit_!**

### Como emendar o último *commit* feito

Emendar um *commit* é uma opção que permite ao usuário incluir no último *commit* realizado mais mudanças feitas no projeto \(adição, modificação ou deleção de arquivos\) que estão na *staging area*, ao invés de criar um novo *commit*. Dessa forma, o usuário pode adicionar ao *git* algum arquivo que tenha sido esquecido no último *commit* ou consertar erros gramaticais simples sem ter que realizar um novo *commit* exclusivamente para isso \(que nem aquele projeto com 5 commits seguidos de "Update README.md" que todos nós já escrevemos alguma vez na vida\). Além disso, a mensagem de um *commit* pode ser alterada por completo pelo usuário quando um *commit* é emendado.

Para realizar uma emenda ao commit anterior, utilize o comando `git commit --amend`. Outras *flags* utilizadas com o comando `git commit` também podem ser utilizadas com o comando de emenda, como, por exemplo: `git commit --amend [-m <mensagem nova para o commit>]`.

## Salvando modificações que não estão em um *commit* para trocar de *branch*

Algumas vezes, é necessário mudar de *branch* sem que as mudanças feitas na *branch* atual sejam colocadas em um *commit*. Talvez você esteja no meio do desenvolvimento de alguma *feature* e tenha que revisar uma *Pull Request* ou consertar um erro crítico em outra *branch*. Entretanto, se você tiver modificações feitas no projeto (adição, modificação ou deleção de arquivos) que não foram salvas em um *commit*, essas modificações poderão ser transportadas para a nova branch que você utilizar quando o *checkout* for realizado, o que é algo indesejado.

Para evitar que o usuário tenha que criar um *commit* às pressas para salvar as mudanças feitas antes de mudar de *branch*, o usuário pode utilizar o *stash* para armazenar as mudanças realizadas. O *stash* permite ao usuário salvar o estado da *branch* atual em um armazenamento interno do *git* para ser restaurado posteriormente. Dessa forma, o usuário consegue sair da *branch* atual sem levar consigo para a nova *branch* as mudanças feitas na *branch* atual que não estão salvas em um commit.

Os comandos básicos para utilizar o stash são os seguintes:

* Armazenar no *stash* todas as mudanças da *branch* que não estão em um *commit*: `git stash push -u [-m <mensagem para identificar as mudanças>]`;
* Listar todas os conjuntos de mudanças contidos no *stash*: `git stash list`;
* Inspecionar um conjunto de mudanças no *stash*: `git stash show <índice do conjunto na lista do stash>`
* Restaurar um conjunto específico de mudanças feitas que estão armazenadas no *stash*, deletando esse conjunto de mudanças do stash: `git stash pop <índice do conjunto na lista do stash>`;

É importante notar que **retirar um conjunto de mudanças do _stash_ pode levar a um conflito entre os arquivos existentes e as mudanças retiradas do _stash_**. Nesse caso, o conjunto de mudanças **não será deletado do _stash_** e o usuário deverá resolver os conflitos para depois, caso necessário, remover manualmente o conjunto de mudanças do *stash* com o comando `git stash drop <índice do conjunto na lista do stash>`.

## Como abortar um *merge* que não pode ser feito automaticamente

Quando tentamos realizar um *merge*, nem sempre será possível que ele seja realizado automaticamente, fazendo com que o usuário tenha que resolver os conflitos manualmente e realizar um *commit* para completar o *merge*. Isso nem sempre é desejável, pois pode ser que esperássemos que o *merge* fosse realizado rapidamente para terminar um *Pull Request* ou que o conflito de *merge* seja gerado porque nossa *branch* local está desatualizada em relação à *branch* do *remote*. Nesses casos, pode ser útil ao usuário abortar o *merge* para tentar novamente mais tarde.

É importante notar que **um _merge_ só pode ser abortado se o _commit_ para completar o _merge_ não tiver sido feito pelo usuário.** Para abortar um *merge* que não pôde ser feito automaticamente,  utilize o comando `git merge --abort`.

## Como mudar a URL de um *remote* do projeto

Um *remote* de um projeto *git* é o repositório online que as *branches* deste projeto acompanham. A maioria dos projetos possui apenas um *remote*, denominado *origin*, o qual geralmente aponta para a *URL* do repositório do projeto no *GitHub* ou *GitLab*. Em alguns casos, é necessário mudar o *remote* utilizado por um projeto. Isso é bem raro de ocorrer, mas pode acontecer caso o repositório do projeto no *GitHub* ou *GitLab* seja renomeado após o projeto ser clonado, por exemplo.

Você pode verificar as informações de *remotes* atuais e seus URLs com o comando `git remote -v`. Para modificar a URL referenciada por um *remote* de um projeto, utilize o seguinte comando: `git remote set-url <Nome do remote> <URL nova do remote>`.
