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

### Desfazendo mudanças

### Ignorando mudanças

## Commits

### Realizando um commit

### Mensagens de commit

### Como desfazer um commit

## Push

### Repositório local e repositório remoto

### Conceito de push

## Branches

### Para que servem branches

### A branch master

### Branches protegidas

## Merges

### Quando realizar um merge

### Conflitos de merge

## Pull request (PR)

### Revisando uma PR

## Pull e fetch

### Copiando localmente uma branch na origem

## Conclusão
