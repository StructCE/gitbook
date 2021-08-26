# Conceitos básicos

Essa seção aborda conceitos básicos relativos ao Git, como a inicialização do Git em um projeto, a realização de mudanças em arquivos utilizando o Git e alguns comandos de gerenciamento de versões. Para executarmos os comandos Git, será necessário que o *Git* esteja esteja instalado e a utilização do *terminal* ou do *Git bash*, tópicos detalhados na [página principal sobre o Git](README.md).

*Caso você ainda não tenha experiência com o Git,* é recomendável que você ao menos leia essa seção antes de trabalhar em um projeto da Struct \(confie em mim quando eu digo que existem **muitos** problemas que podem ser gerados quando o Git é utilizado de forma errada\).

*Caso você já saiba como utilizar o Git,* essa seção provavelmente não lhe será muito útil, mas sinta-se livre para estudá-la, pois ela talvez te ensine algo.

## Iniciando o Git em um projeto

O primeiro passo para a utilização do Git é *iniciarmos o Git em um projeto.* Quando falamos de um *projeto*, queremos dizer todos os arquivos \(de código fonte ou não\) relativos a um programa ou trabalho. A inicialização do Git no projeto é necessária para que possamos utilizar o sistema de controle de versão Git nos arquivos do projeto.

O Git pode ser inicializado tanto em uma pasta vazia antes mesmo de escrevermos qualquer arquivo relativo ao projeto \(o que é altamente recomendado\) como em uma pasta de um projeto que já está em andamento, ou seja, com arquivos existentes. Também podemos criar um repositório \(o nome dado a um projeto online\) nos websites GitHub ou GitLab, o qual já vem com o Git inicializado \(isso vai ser *muito* útil para trabalhos em grupo ao longo do curso\).

Todas as informações necessárias para o funcionamento do Git ficam armazenadas em uma **pasta oculta** chamada `.git`, a qual é criada quando o Git é iniciado em um projeto. Dessa forma, a inicialização do Git **não modifica** os arquivos presentes em um projeto já existente.

Após o Git ser inicializado em um projeto, você poderá utilizar um *terminal* ou *Git bash* para executar **comandos do Git** no seu projeto e nos arquivos pertencentes a ele. É importante ressaltar que você precisa estar em um **subdiretório** de um projeto que tenha o git inicializado para que esses comandos sejam executados com sucesso.

Embora todos os projetos criados em *Ruby on Rails*, a framework utilizada pela Struct para o desenvolvimento de websites, já *inicializem o Git automaticamente*, vamos detalhar nesse tópico como inicializar um projeto no GitHub ou GitLab e como inicializar o Git em um projeto vazio ou existente. *Um projeto com o Git inicializado* **será necessário** *para executarmos os comandos das próximas seções!* **Recomendamos a criação de um projeto teste no GitHub ou GitLab.**

### Criando um repositório no GitHub ou GitLab

A criação de um repositório no GitHub ou no GitLab é bem simples e pode ser feita diretamente em um desses websites. Para isso, será necessário se cadastrar em um desses websites \(você provavelmente terá que fazer isso ao longo do curso mais cedo ou mais tarde\) e fazer o login com sua conta. Geralmente, um repositório pode ser criado facilmente clicando-se no botão de `+` contido no navbar desses websites e, depois, na opção `New repository` ou `New project`. É importante frisar que *os repositórios desses websites já vem com o Git inicializado.*

Após a criação de um repositório \(mesmo que seja apenas para treinar o uso do Git\), será  necessário **clonar** o repositório para o seu computador. **Clonar** um repositório significa copiar os arquivos do repositório para o seu computador e pode ser feito com um comando Git.

Para *clonar* o repositório, copie o link HTTPS do repositório \(isso pode ser feito por meio do botão `clone` na página principal do seu repositório\), abra o *terminal* ou o *Git bash* e digite o comando `git clone [link]`. Ao executar esse comando, os arquivos do repositório \(incluindo a pasta `.git`\) serão criados em uma pasta com o nome do repositório. E, com isso, **você criou um repositório com sucesso!**  

### Iniciando o git em um projeto local

Para iniciar o Git em um projeto local \(seja esse projeto uma pasta vazia ou um projeto de programação\), basta abrir um *terminal* ou *Git bash*, navegar até a pasta do projeto \(isso pode ser feito com o comando `cd [caminho até a pasta]`\), e executar o comando `git init`. Isso irá inicializar a pasta `.git` no seu projeto e, com isso, você **iniciou o git em um projeto local com sucesso!**

## Staging area

No contexto de dados, o termo *staging area* é utilizado para denominar um local de **armazenamento intermediário temporário** entre a fonte dos dados e o seu destino final. Ao utilizarmos o Git, todas as adições de arquivos, deleções de arquivos e mudanças feitas em arquivos não vão diretamente para o seu projeto, mas passam por uma *staging area*, permitindo ao programador verificar exatamente quais alterações foram realizadas nos arquivos do projeto e reverter alterações acidentais.

Nesse tópico, vamos detalhar mais sobre como verificar quais alterações de arquivos estão presentes na *staging area*, como decidir quais alterações de arquivos ficarão na *staging area* e quais serão agrupadas para se tornarem mudanças permanentes, e como escolher quais arquivos não devem ser incluídos na *staging area*.

### Verificando o que foi mudado

Para verificar quais alterações de arquivos \(arquivos adicionados, modificados ou excluídos\) estão presentes na *staging area*, basta executar o comando `git status`.

Esse comando irá imprimir várias informações na tela, incluindo os arquivos que foram alterados. É possível visualizar os nomes dos arquivos que forma alterados, o tipo de alteração feita \(criação de arquivo, modificação, renomeação e deleção\) e se essa alteração está destinada a se tornar permanente \(nomes de arquivos em verde\) ou permanecer na *staging area* \(nomes de arquivos em vermelho\).

Além das informações relativas à alteração de arquivos, o comando `git status` mostra na tela várias informações relevantes e outros comandos git que possam ser relevantes no momento, sendo um comando extremamente útil.

### Adicionando mudanças

Após verificar quais dos arquivos modificados você deseja que seja adicionado a sua *staging area*, para que eles possam ser futuramente definidos como mudanças definitivas, você deve marcar o arquivo criado ou modificado como monitorado. Você pode fazer isso usando o comando `git add <nome do arquivo>` para marcação de um único arquivo, ou usar `git add .` para marcar todos os arquivos modificados indicados pelo `git status`.

Note que esses arquivos adicionados ainda estão no armazenamento intermediário, apenas sendo registrado como definitivos após um *commit*. Além disso, caso você adicione um arquivo a *staging area* e depois modifique-o novamente antes de um *commit*, apenas as mudanças feitas até o momento da adição estarão registradas, sendo necessário um novo `git add` para as novas mudanças tomarem efeito.

### Desfazendo mudanças

Após verificar os arquivos modificados, se você acredita que alguma mudança tenha sido acidental, ou simplesmente deseja retornar algum arquivo à forma que ele estava antes da mudança, você pode utilizar o comando `git restore <nome do arquivo>` para reverter o arquivo ao seu estado anterior. 

Note que reverter uma modificação é algo definitivo, então tome muito cuidado ao usar o comando `git restore` e certifique-se que o arquivo que você está restaurando é realmente o arquivo desejado.

Caso você tenha adicionado um arquivo sem querer com o comando `git add`, você pode remover o registro dele com o comando `git restore --staged <nome do arquivo>`. Esse comando não retorna o arquivo ao seu estado anterior, apenas o remove da *staging area*, ou seja, caso deseje desfazer as mudanças nesse arquivo, terá que ser dado um outro `git restore` no fim.

### Ignorando mudanças

Por vezes, você deseja que arquivos ou pastas específicos, ou arquivos de um determinado tipo, não sejam registrados nunca pelo git, seja por conter dados pessoais como senhas ou logins ou mesmo por serem arquivos de teste, para isso, o git nos proporciona uma ferramenta para criar regras de arquivos a serem ignorados.

Todas as regras de quais arquivos devem ser ignorados devem ser registradas no arquivo `.gitignore`. Em projetos gerados pelo Rails ou React, junto com a inicialização do git, também já é criado o arquivo `.gitignore` na raiz do repositório do projeto. Caso no seu repositório ainda não tenha o arquivo, apenas crie com o nome correto.
Note que o git procura pelo arquivo `.gitignore` em todas as pastas do repositório, então se você deseja criar regras específicas para uma pasta, apenas crie um novo arquivo `.gitignore` dentro dela. As regras no arquivo da pasta raiz valem para o projeto inteiro e todas as suas pastas.

Algumas das regras que podem ser adicionadas no arquivo podem ser vistas na tabela abaixo. Mais regras podem ser vistas também na [documentação oficial do git](https://git-scm.com/docs/gitignore) (em inglês).
| Regra | Descrição |
|--|--|
| * | Ignora todos os arquivos dentro da pasta |
| arquivo.txt | Ignora qualquer arquivo de nome *arquivo.txt* na pasta ou em subpastas |
| *.jpg | Ignora todos os arquivos do formato *jpg* dentro da pasta |
| !imagem.jpg | Define o arquivo *imagem.jpg* para não ser ignorado, mesmo que ele se encaixe em regras anteriores |


## Commits

Após todos os arquivos modificados serem adicionados na *staging area*, agora temos a necessidade de registrar esse conjunto de modificações como a versão atual do nosso projeto, e fazemos isso registrando um *commit*.

Um *commit* é um registro de uma coleção de modificações no seu repositório, contendo os arquivos adicionados, removidos e modificados e uma descrição detalhando o que mudou desde a versão anterior. Ele nos permite acompanhar a evolução do nosso código de forma gradual e possibilita que retornemos para uma versão antiga caso seja necessário. 
Para visualizar o histórico de *commits* no seu terminal, use o comando `git log`. Também é possível ver o histórico de *commits* e as modificações em cada um pelo repositório no github ou gitlab.   

### Realizando um commit

Para realizar um *commit*, após ter adicionado os arquivos modificados com o comando `git add`, execute o comando `git commit`. Esse comando fará aparecer uma instância do editor de texto no terminal para que a descrição do *commit* seja escrita. Escreve, salve e saia do editor para que seu *commit* seja corretamente realizado.
Deverá aparecer, após o *commit*, uma mensagem em seu terminal com a quantidade de inserções e deleções que ocorreram, além dos arquivos modificados, criados e removidos.

Para realizar o *commit* e já escrever a descrição em uma linha, sem necessidade de abrir o editor de texto, use o comando `git commit -m "<Sua mensagem aqui>"`, com a mensagem entre parênteses.

### Mensagens de commit

A mensagem ou descrição do *commit* é uma de suas características mais importantes e serve para que outros membros de um projeto possam ver quais modificações foram feitas e, caso precisemos encontrar alguma versão mais antiga do código no futuro, podermos identificar facilmente a versão desejada.

Para isso, é importante que todas as mensagens de *commit* sejam claras, objetivas e bem descritivas sobre o que foi feito desde a versão anterior. Para boa parte das modificações, uma linha apenas com até 50 caracteres já deve ser o suficiente para descrever o que foi feito. Caso necessite da criação de um texto maior explicando o que foi modificado, comece com uma linha com até 50 caracteres resumindo as mudanças (comparando com um e-mail, esse seria seu assunto), pule uma linha e comece seu texto descrevendo suas modificações.

### Como desfazer um commit

Ás vezes pode acontecer de você necessitar voltar atrás em algum *commit* que você realizou, seja por que você esqueceu alguma coisa ou alguma coisa de errada ocorreu.

Para o caso de você ter esquecido de adicionar algum arquivo a *staging area* antes de um commit, ao invés de reverter ele você pode adicionar o arquivo esquecido com o `git add` e usar o comando `git commit --amend` para adicionar os novos arquivos na *staging area* ao último *commit* realizado, sem criar um novo *commit* para isso.

Antes de entender como realmente reverter algum *commit*, vamos ver alguns conceitos internos do git.

#### HEAD

No git, o ***HEAD***  representa a versão mais recente do seu código, ou seja, o último *commit* feito. Com isso, simulando, um histórico do git, podemos ter isso no nosso repositório:

```
$ git log --oneline

3fad532  Ultimo commit   (HEAD)
3bnaj03  Commit antes do HEAD   (HEAD~1)
vcn3ed5  Dois commits antes do HEAD   (HEAD~2)
```

Logo, o que queremos ao reverter um *commit* é sair do estado atual (*HEAD*) para o estado anterior (*HEAD~1*).

#### Soft Reset

Caso você deseje voltar ao estado anterior mas manter as mudanças feitas no atual localmente (fora da *staging area*) você pode usar o comando `git reset --soft HEAD~1`.
Esse comando é ideal quando você não quer descartar tudo que foi feito no último *commit*, podendo voltar atrás em cada arquivo modificado escolhendo o que manter e o que reverter.

#### Hard Reset

Caso você deseje não apenas voltar ao estado anterior, mas também descartar tudo feito no *HEAD*, use o comando `git reset --hard HEAD~1`. Cuidado que com esse comando tudo que foi modificado anteriormente, inclusive mudanças ainda sem *commit*, será automaticamente descartado.

#### Revert

Ao contrário dos comandos anteriores, que voltam o repositório para um estado anterior, o comando `git revert HEAD` cria um novo *commit* com as mudanças necessárias para reverter os arquivos do repositório para o estando anterior ao *HEAD*.

## Branches

### Para que servem branches

Em geral, ao trabalhar em um projeto, queremos separar o ambiente com a versão mais atual e verificada do nosso projeto de versões em desenvolvimento, ao mesmo que queremos permitir que diversas pessoas trabalhem sobre um mesmo repositório sem muitas complicações.

Para isso, o git nos disponibiliza as **branches** que são diversas ramificações do proejto em um mesmo repositório, a fim de separar diferentes linhas de desenvolvimento da versão mais estável e entre elas próprias.
Por exemplo, num projeto de um site eu estou responsável pela criação da funcionalidade de login, para isso eu crio a *branch* `login` para que meu desenvolvimento fique separado do restante do repositório até que ele tenha terminado e sido revisado por outros membros do projeto.
 
Para checar em qual *branch* você está trabalhando no momento use o comando `git branch`. Para a criação de uma nova *branch* você pode usar o comando `git branch <nome da branch>` (use um nome curto e sem espaços). Ao usar esse comando você ainda estará na *branch* que você estava antes, para se movimentar entre *branches*, então, use o comando `git checkout <nome da branch>`. Se quiser criar uma *branch* nova e já ir para ela automaticamente use o comando `git checkout -b <nome da branch>`.
Para deletar uma *branch*, use o comando `git branch -d <nome da branch>`.

### A branch master

A *branch* **master** ou **main** é a ramificação principal do seu repositório, onde deve sempre ser armazenado apenas a versão mais atual e testada do código. Deve sempre evitar realizar alterações diretamente nessa *branch*, ao invés disso sendo recomendado criar *branches* secundárias com as modificações sendo feitas nelas.

### Branches protegidas

Embora não seja uma configuração do git em si, o Github e outros sites de armazenamento de repositórios permitem que algumas *branches* sejam classificadas como protegidas, sendo criadas regras para que se possam fazer modificações nelas. 
Como exemplo, pode-se exigir que modificações em uma *branch* sejam feitas através de um *pull request* com ao menos uma aprovação. Você pode ler mais sobre as *branches* protegidas do Github e suas configurações [aqui](https://docs.github.com/pt/github/administering-a-repository/defining-the-mergeability-of-pull-requests/about-protected-branches#require-signed-commits).

## Push

### Repositório local e repositório remoto

Quando trabalhamos com git é comum armazenarmos nosso repositório não apenas no nosso computador, mas também em sites como o GitHub ou GitLab.
Com isso, nosso trabalho fica dividido entre duas versões de um mesmo repositório, o **repositório local**, que fica em seu computador e armazena localmente suas modificações e o **repositório remoto**, que fica em um servidor e age como o repositório central, conectando também outros repositórios locais de diversas pessoas trabalhando no mesmo projeto.

### Conceito de push

Após você terminar seu trabalho local, e realizar todos os seus *commits*, essas modificações estão apenas armazenadas no seu computador, ou seja, no repositório local. Para enviarmos essa modificação para o repositório remoto podemos utilizar o comando `git push`. Na maioria das configurações de repositórios remotos, será exigido uma autenticação para envio das modificações, que poderá ser fornecida pelo próprio terminal.

Quando feito o *push* de modificações em uma nova *branch* local, ainda não no repositório remoto, deverá ser utilizado o comando `git push -u origin <nome da branch>`. Ao utilizar o comando `git push` em uma *branch* ainda não presente no servidor remoto, o terminal deve sugerir o comando adequado a ser usado também.

## Merges

Quando estamos trabalhando com diversas *branches*, é normal querermos mesclar o conteúdo de uma *branch* em outra, seja para combinar duas linha de desenvolvimento em uma ou mesmo levar o desenvolvimento de uma *branch* para a **master**.

Para realizar a junção das ramificações, vá até a *branch* de destino usando o comando `git checkout` e utilize o comando `git merge <nome da branch de origem>`. Com isso, todo o conteúdo da *branch* de destino continuará nela porém serão adicionados as modificações da *branch* de origem, sendo gerado um novo *commit* automaticamente com indicando o *merge*.

### Conflitos de merge

Quando estamos realizando *merge* de duas *branches* que tiveram seu conteúdo modificado desde o último *commit* em comum entre elas, pode ocorrer conflitos na hora do *merge*. Esse conflitos ocorrem em arquivos que foram modificados nas duas *branches* e que o git não conseguiu resolver sozinho.
Nesse caso, será indicado no terminal os arquivos que tiveram um conflito e, nesses arquivos, serão adicionadas novas linhas indicando onde o conflito ocorreu. IDEs como o RubyMine e editores de texto como o VSCode ajudam a identificar onde os conflitos ocorreram e também podem auxiliar na resolução destes.

Durante a resolução do conflito, é importante que a pessoa responsável pelo *merge* leia o código reformule ele de forma que as duas modificações em conflito fiquem válidas e não quebrem o código escrito em nenhuma das duas *branches*. Em alguns casos, pode-se que querer que apenas a modificação feita por uma das *branches* permaneça no código, nesse caso, apenas exclua a que não deve estar presente.

## Pull Request (PR)

Ao fazer o *push* de uma nova *branch* para o repositório remoto, sites como o Github e GItlab permitem que seja solicitado que essa *branch* seja mesclada com alguma outra *branch*, normalmente a **master**. Nesse caso, o próprio site analisa se o *merge* pode ser dado sem conflitos e, se houver algum conflito, permite que este seja resolvido pelo próprio site, sem necessidade de resolução pelo terminal.

Ao criar um *Pull Request* (*Merge Request* no Gitlab), o usuário pode descrever todas as modificações feitas na *branch* e detalhar tudo que achar necessário. Além disso, pode ser requisitado a review de alguém em específico responsável pelo repositório, adicionar *tags* para classificar e conectar a PR com alguma issue no site, a fim de marcá-la como terminada.

### Revisando uma PR

Qualquer usuário com permissões no repositório pode avaliar uma PR no Github ou Gitlab. Esses sites oferecem telas intuitivas para analisar todos os arquivos modificados na *branch* e compará-los com os originais. É ideal que, além de ler o código, o analisador da PR também execute-o localmente em seu computador para garantir o funcionamento tanto das novas funcionalidades implementadas e também se as modificações feitas não resultaram em algum bug em uma funcionalidade antiga.

Ao terminar sua análise, esses sites permitem que você as aprove, quando tudo estiver correto, deixe algum comentário sem aprovação explicita ou requeira mudanças para o autor do código, indicando por um comentário quais problemas foram encontrados e quais as mudanças requisitadas.

Quando a PR tiver sido aprovada pela quantidade esperada de pessoas (em geral, apenas uma basta, mas combine isso com seu time com antecedência), utilize as ferramentas do próprio site para dar o *merge* da *branch*, corrigindo conflitos se houver, e delete a *branch* no repositório remoto após ao finalizar. 

## Pull e fetch

Da mesma forma que ao fazer modificações no seu repositório local você precisa solicitar que essas modificações sejam enviadas para o remoto usando o `git push`, ocasionalmente você precisa solicitar que modificações feitas remotamente sejam refletidas no seu repositório local.

Ao usar o comando `git fetch`, as referências locais do repositório são atualizadas para os dados no repositório remoto, incluindo quais *branches* novas foram criadas e novos *commits* foram feitos, mas não atualiza a *branch* que você está trabalhando com as novas modificações remotas.

O comando `git pull` por outro lado, além de realizar tudo que o `git fetch` faz, ele também atualiza os arquivos da sua *branch* com os dados mais atuais da *branch* remota, sendo o equivalente de realizar o comando `git merge FETCH_HEAD` após o *fetch*.

## Conclusão

Com as informações dessa página você deve ser capaz de realizar o básico de trabalho com o git, o que já é suficiente para a maior parte dos projetos que você participar. Para informações mais detalhadas sobre os comandos disponíveis no git a [documentação oficial](https://git-scm.com/book/en/v2) deles serve como uma boa referência. Para detalhes referentes ao Github em si, use o [guia deles](https://docs.github.com/pt) como referência.