# Git

O git é o software para controle de versão distribuído utilizado pela Struct em nossos projetos. Se usado de forma correta, essa poderosa ferramenta permite que mais de uma pessoa trabalhe no mesmo projeto de software simultaneamente, que as mudanças feitas no projeto sejam revisadas antes de ser aprovadas, e que o programador possua cópias locais do código para experimentar mudanças sem prejudicar o código do projeto. Entretanto, a grande quantidade de recursos oferecida pelo git pode facilmente conduzir a complicações e problemas, motivo pelo qual é essencial que sua utilização seja sempre feita de forma bem informada e norteada por boas práticas de projeto. Mais informações sobre o git podem ser encontradas no [site oficial do git](https://git-scm.com/).

## Instalação

A instalação do Git varia entre diferentes sistemas operacionais. Dependendo do sistema operacional e do ambiente de desenvolvimento, será útil instalar também um programa de interface gráfica para o uso do git.

### Windows

Para instalar o Git para Windows, visite a [página de instalação do Git para Windows](https://git-scm.com/download/win) e escolha o download apropriado. O wizard de instalação te fornecerá várias opções adicionais de instalação além do Git. Além da instalação do Git, é **recomendável** que você instale o *Git bash* para a execução de comandos do Git e o *Notepad++* para edição de mensagens de resolução de conflitos.

Caso você esteja programando em *IDEs* como o *RubyMine* ou o *CLion*, a maioria das features do Git que você precisará utilizar já estão integrados na *IDE*. Caso você programe em editores de texto, é altamente recomendável que você instale o [GitHub Desktop](https://desktop.github.com/) para ter um programa com interface gráfica para utilizar o Git. Uma última alternativa é a utilização do *Git bash*, o qual você deve ter instalado junto com a instalação do Git.

### Sistemas baseados em Linux

A grande maioria dos sistemas operacionais baseados em Linux **já possuem o git instalado por padrão.**

Para verificar se o git já está instalado, abra um terminal e rode o seguinte comando:  
`git --version`

Caso a execução desse comando retorne uma frase do tipo `git version X.YY.Z`, você já possui o git instalado. Caso a frase de retorno seja parecida com `bash: git: command not found`, você não possui o git instalado.

**Caso você não possua o git instalado**, ele provavelmente pode ser instalado diretamente pelos repositórios oficiais do sistema operacional. A [página de instalação do Git para Linux](https://git-scm.com/download/linux) possui os comandos de instalação do Git para vários sistemas baseados em Linux.

## Disciplinas do curso que abordam esse conteúdo

* Métodos de programação \(3º Semestre\)
* Técnicas de programação I \(4º Semestre\)
* Engenharia de software \(6º Semestre\)
