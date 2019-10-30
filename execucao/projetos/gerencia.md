# Gerência de projetos

O gerente de um projeto possui funções essenciais à qualidade de vida de um projeto, como a criação do projeto em si, a gerência das sprints do projeto e a comunicação dos detalhes do projeto para os outros membros de equipe nas reuniões gerais. Em suma, o gerente do projeto conduz a execução do projeto, tomando as medidas necessárias para que seu desenvolvimento seja bem sucedido.

Está pagina contém as informações necessárias para se gerenciar um projeto de maneira adequada.

## Início do projeto

O primeiro passo em um projeto de software consiste na criação e configuração do repositório em que o projeto será desenvolvido. Isso inclui criar o repositório do projeto, as estruturas de pastas para abrigar o código fonte e outros recursos e configurar adequadamente os arquivos de controle de versão, os arquivos de documentação do projeto, a utilização de bibliotecas externas \(gems\), o banco de dados do projeto e a geração de imagem do projeto \(docker\).

Embora isso pareça ser muita coisa, iremos detalhar melhor cada passo nas seções abaixo.

### Projeto Rails

O primeiro passo na inicialização do projeto é a criação do projeto na framework [*Ruby on Rails*](../ruby-on-rails/README.md). Para isso, vamos escolher, utilizando o RVM ou Rbenv, uma versão de Ruby esteja um *minor release* atrás da última versão \(ou seja, se a última versão de Ruby é a 2.x, utilize a versão 2.x-1 para o projeto\). Na dúvida, utilize a versão de Ruby utilizada no último projeto. Isso evita que tenhamos que lidar com os bugs inerentes à versão mais nova do Ruby e das gems que o acompanham. Caso algum dos membros do projeto não tenha um gerenciador de versão de Ruby instalado \(como RVM e Rbenv\), ajude ele com a instalação \(esse tipo de software é praticamente essecial para se trabalhar em vários projetos, cada um com uma versão diferente de Ruby\).

Após escolher a versão de Ruby desejada, será necessário realizar a instalação de algumas gems \(que são as bibliotecas do Ruby\). Para instalar uma gem, basta rodar o comando `gem install nome_da_gem`. Com isso em mente, instale as gems *rails* \(framework de desenvolvimento de websites e serviços web\), *mysql2* e *pg* \(gems para o MySQL e PostgreSQL respectivamente, os sistemas gerenciadores de bancos de dados, ou SGBDs, mais utilizados\). Além dessas gems, será necessário instalar os SGBDs MySQL e PostgreSQL em seu sistema operacional \(assunto que **não** será coberto nessa página\).

Após instalar as gems e os SGBDs em seu computador, caberá a você, como gerente de projetos, decidir qual SGBD utilizar no projeto. O MySQL é mais amigável para iniciantes e possui uma melhor forma de visualizar e manipular diretamente o banco de dados, mas requer mais tempo para ser configurado e a utilização de uma gem \([*figaro*](######figaro)\) para gerenciar os credenciais de login. Já o PostgreSQL pode ser utilizado com quase nenhuma configuração adicional, mas possui uma instalação mais complicada e não permite que o usuário manipule o banco de dados com facilidade. Caso seja sua primeira vez gerenciando um projeto, fale com o diretor de projetos ou com um membro mais experiente para pedir uma recomendação \(eu, pessoalmente, recomendaria o MySQL\).

Após escolher o SGBD a ser utilizado, chegou a hora de criar o projeto. Para isso, rode o comando `rails new nome_do_projeto_em_snake_case -d {mysql | postgresql}`, escolhendo o último argumento para coincidir com o SGBD desejado. O framework cuidará da criação de pastas e arquivos para o desenvolvimento do projeto.

Caso você tenha escolhido o MySQL, configure a gem [*figaro*](######figaro) para gerenciar credenciais e, caso você **não** queira utilizar o usuário *root* no projeto, crie as tabelas de desenvolvimento e testes e um usuário com permissão de acesso a elas. Caso você tenha escolhido o PostgreSQL, preencha o arquivo `config/database.yml` com os credenciais do SGBD \(em sistemas operacionais com o *kernel* Linux, você pode preencher apenas o seu nome de usuário e apagar o campo de senha caso você tenha optado, na instalação do PostgreSQL, por utilizar sua conta de usuário do sistema operacional como um usuário do SGBD\).

Por fim, tente executar o projeto utilizando o comando `rails s`. Caso a execução do projeto não gere alguma mensagem de erro, adicione todos os arquivos gerados ao controle de versão sob o nome 'Commit inicial'. Caso contrário, corrija os erros do projeto **antes** de realizar o commit inicial.

### Repositório

A criação do repositório para o projeto deve ser feita no grupo da Struct do GitLab. O nome do repositório geralmente segue o padrão `projeto_nome` ou `projeto_codinome` \(como gerente de projeto, sinta-se livre para criar um codinome épico para o projeto :grinning:\). Configure o repositório como privado e **não** inicialize ele com um README, pois o Rails já gerá esse arquivo para você. Após criar o repositório, faça o upload dos arquivos gerados pelo projeto de Rails para o repositório.

### Segundo commit

Após a criação do repositório, você deverá fazer um segundo commit na branch master que faça todas as configurações necessárias no projeto. Esse segundo commit deve colocar no README informações básicas do projeto, colocar no projeto arquivos padrão que devem estar presentes em qualquer projeto da Struct e configurar as gems que o projeto irá utilizar. Mais detalhes são fornecidos nas subseções abaixo. Após executar **todos** os passos de **cada** subseção, realize um commit com o nome "Estrutura inicial" adicionando as mudanças que você fez.

#### README

O README deve conter as dependências do projeto \(versão do Ruby, banco de dados, etc...\) e os dados do projeto em si, os quais incluem a especificação do projeto \(bem resumida, em uma única frase\), o codinome do projeto \(se existir\), a data de assinatura do contrato, o prazo de desenvolvimento do projeto e a data prevista de entrega do projeto.

Não utilize o README como uma lista de tarefas, pois isso pode ser feito por meio de *issues*.

#### Arquivos padrão

No momento, existem 2 arquivos padrão que devem estar presentes no projeto: o `.gitignore` e o script `start.sh`.

##### Arquivo .gitignore

Como sabemos, o `.gitignore` é utilizado para impedir que arquivos locais sejam acidentalmente adicionados ao repositório. Arquivos que geralmente devem ser ignorados incluem arquivos de configurações pessoais \(`.bundle`, `.vscode`, `.idea`, `.DS_store`\), pastas de caches \(`tmp` e `storage`\), logs \(arquivos `*.log` e pasta `log`\) e módulos do *node js* \(a pasta `node_modules`\).

**Nunca** coloque arquivos que afetam o desenvolvimento do projeto \(como `Gemfile`\) no `.gitignore`.

É **essencial** que a configuração do `.gitignore` seja feita no **início** do projeto, pois problemas relacionados a esse arquivo são um pesadelo para serem resolvidos.

Segue, abaixo, um template de arquivo `.gitignore`:

```
# Environment normalization:
*.DS_Store
.idea
.rvmrc
.vscode
/.bundle
/vendor/bundle

# Ignore all logfiles and tempfiles:
/log/*
/tmp/*
!/log/.keep
!/tmp/.keep

# Ignore uploaded files in development:
/storage/*
!/storage/.keep

# Ignore node_modules:
node_modules/

# Ignore yarn files:
/yarn-error.log
yarn-debug.log*
.yarn-integrity

# Ignore precompiled javascript packs:
/public/packs
/public/packs-test
/public/assets

# Ignore Byebug command history file:
.byebug_history

# Ignore project secrets:
/config/initializers/secret_token.rb
/config/master.key
```

##### Arquivo start.sh

O arquivo `start.sh` é um script de execução utilizado para o *Docker*, mas que também pode ser utilizado para que novos integrantes do projeto inicializem o projeto sem maiores dificuldades.

Segue, abaixo, um template de arquivo `start.sh`:

```
#!/bin/sh
rails db:migrate
bundle exec puma -C config/puma.rb
```

#### Configuração de gems

As *gems* do *Ruby on Rails* são bibliotecas externas que fornecem funcionalidades ao seu projeto. Dependendo do projeto em questão, os desenvolvedores precisarão utilizar gems que não vem configuradas por padrão em um projeto de *Ruby on Rails*, de forma que cabe ao gerente de projetos o trabalho de analisar quais gems serão necessárias no decorrer do projeto, colocar essas gems no `Gemfile` e realizar qualquer outra configuração para que essas gems funcionem adequadamente \(a maioria das gems requer alguma configuração adicional para funcionar\).

Além de configurar as novas gems, o gerente de projeto também deve verificar qualquer aviso de *deprecated gem* gerado pelo Rails após a execução dos comandos `bundle install` e `rails s` e corrigir esses avisos para evitar problemas com o projeto.

Idealmente, esse processo de configuração deve ser feito no *começo* do projeto para que os desenvolvedores tenham acesso às funcionalidades adequadas para o desenvolvimento do projeto \(e para que eles não tenham que ficar rodando `bundle install` toda hora\). Lembre-se de, após configurar ou substituir uma gem, sempre tentar executar o projeto com o comando `rails s` para garantir que o funcionamento do projeto não foi afetado por alguma gem mal configurada.

Nesta seção, vamos listar as gems úteis para os projetos da Struct que devem ser configuradas manualmente e alguns casos comuns de *deprecated gems* que devem ser substituídas.

##### Gems úteis para projetos

###### Bootstrap

O Bootstrap é a framework de desenvolvimento de websites utilizado pela Struct para desenvolver. Ele deve ser utilizado em **todos** os projetos de *Ruby on Rails*.

Para configurar o Bootstrap, siga os seguintes passos:

1. Adicione o trecho de código abaixo ao arquivo `Gemfile`:

  ```
  # Bootstrap gems:
  gem 'bootstrap', '~> 4'
  gem 'bootstrap_form', '~> 4'
  gem 'bootstrap4-datetime-picker-rails'
  gem 'jquery-rails'
  ```

2. Execute o comando `bundle install` para instalar as gem adicionadas ao `Gemfile`.

3. Adicione o trecho de código abaixo ao arquivo 'app/assets/javascripts/application.js' \(Linhas de código com `//=` **não são comentários!**\):

  ```
  // Require Bootstrap:
  //= require jquery3
  //= require popper
  //= require bootstrap-sprockets

  // Require Moment:
  //= require moment-timezone-with-data
  //= require tempusdominus-bootstrap-4
  ```

4. Adicione o trecho de código abaixo ao arquivo 'app/assets/stylesheets/application.scss' \(Caso a extensão do arquivo seja '.css', **renomeie** o arquivo e **não** se preocupe com os warnings do *RubyMine*\):

  ```
  // Import Bootstrap:
  @import "bootstrap";

  // Import Bootstrap forms:
  @import "rails_bootstrap_forms";

  // Import Bootstrap datetime picker:
  @import "tempusdominus-bootstrap-4";
  ```

###### Figaro

O Figaro é uma gem utilizada para gerenciar credenciais de bancos de dados em um arquivo de configuração local. Recomenda-se sua utilização em projetos que possuam um banco de dados com o SGBD \(Sistema gerenciador de banco de dados\) MySQL ou qualquer outro SGBD que não possua um bom sistema de armazenamento de credenciais de login \(o PostgreSQL é um caso raro de SGBD que **não** precisa da gem Figaro\).

Para configurar o Figaro, siga os passos abaixo:

1. Adicione o trecho de código abaixo ao arquivo `Gemfile`:

  ```
  # Database credentials:
  gem 'figaro'
  ```

2. Execute o comando `bundle install` para instalar as gem adicionadas ao `Gemfile`.

3. Execute o comando `bundle exec figaro install` para configurar a gem.

4. Modifique o arquivo `config/database.yml` nas linhas demonstradas abaixo:

  ```
  default: &default
    # Modifique apenas as linhas abaixo e não apague ou modifique as outras linhas!
    username: <%= ENV['db_user'] %>
    password: <%= ENV['db_password'] %>
  ```

5. Adicione o trecho de código abaixo ao arquivo `config/application.yml`:

  ```
  # Database credentials:
  db_user: "seu_usuario_do_DB_entre_parentesis"
  db_password: "sua_senha_do_DB_entre_parentesis"
  ```

Após configurar a gem Figaro em seu ambiente, **avise os outros membros do projeto** que eles deveram executar os passos 2, 3 e 5 para configurar a gem em seus ambientes!

###### Font Awesome

O Font Awesome é uma biblioteca de ícones \(*icons*\) de alta qualidade para websites, os quais podem ser utilizados em um projeto de *Ruby on Rails* por meio de uma gem. Como a utilização de ícones ajuda a melhorar a percepção de qualidade do produto por parte do cliente e dos usuários, recomendamos que essa gem seja utilizada em **todos** os projetos de website da Struct.

Para configurar o Font Awesome, siga os passos abaixo:

1. Adicione o trecho de código abaixo ao arquivo `Gemfile`:

  ```
  # Font Awesome gem:
  gem 'font-awesome-rails'
  ```

2. Execute o comando `bundle install` para instalar as gem adicionadas ao `Gemfile`.

3. Adicione o trecho de código abaixo ao arquivo 'app/assets/stylesheets/application.scss' \(Caso a extensão do arquivo seja '.css', **renomeie** o arquivo e **não** se preocupe com os warnings do *RubyMine*\):

  ```
  // Font-awesome import:
  @import "font-awesome";
  ```

##### *Deprecated gems*

###### Chrome driver helper

A gem `chromedriver-helper` parou de receber suporte em Março de 2019. Substitua ela no Gemfile pela gem `webdrivers`.

###### SASS Rails

A gem `sass-rails` parou de receber suporte em Março de 2019. Substitua ela no Gemfile pela gem `sassc-rails`.

### Criação de branches padrão

Um projeto bem estruturado contém um conjunto de branches padrões e um fluxo bem definido que novas features ou mudanças em features existentes devem percorrer para serem aprovadas definitivamente e chegarem aos clientes da aplicação. O gerente de projetos é o responsável por criar e configurar as branches padrões no repositório do projeto no GitLab. Também cabe ao gerente de projetos garantir que o desenvolvimento siga o fluxo definido pelas branches padrões, evitando a utilização de atalhos e os problemas gerados pela quebra do fluxo de desenvolvimento.

Esta seção detalha as branches padrão que todo projeto da Struct deve ter, com uma breve descrição do seu propósito geral e fluxo de desenvolvimento.

#### Develop

A **develop** é a branch de desenvolvimento padrão. Ela deve ser marcada como *default* e *protected* nas configurações de branch do projeto. Todas as features desenvolvidas devem ser adicionadas primeiramente à *develop* por meio de um *Merge request*.

#### Master

A **master** é a branch da versão oficial do software para os desenvolvedores. Ela deve ser marcada como *protected* nas configurações de branch do projeto. De tempos em tempos, as features desenvolvidas na branch *develop* são levadas a branch *master* por meio de um *Merge request*, permitindo ao time de desenvolvedores revisar com mais afinco e atenção as features desenvolvidas \(tipicamente, no final da sprint\). Além disso, a *Master* pode ser utilizada para receber diretamente correções de *bugs* ou problemas críticos, sem a necessidade dessas correções urgentes se misturarem com as features novas da *Develop*, encurtando o caminho de desenvolvimento até o cliente.

#### Production

A **production** é a branch da versão oficial do software para os clientes. Ela deve ser marcada como *protected* nas configurações de branch do projeto. De tempos em tempos, as features testadas e revisadas presentes na branch *master* são levadas à branch *production* por meio de um *Merge request* para que essas mudanças cheguem efetivamente aos clientes do projeto e possam ser utilizadas ou visualizadas pelos usuários do produto. Tenha muito cuidado ao colocar mudanças nessa branch, pois qualquer falha ou erro terá **consequências reais** para o cliente e para os usuários da aplicação.

### Docker

## Sprints

### Issues

### Desenvolvimento

### Finalização

## Reuniões gerais

O gerente de um projeto também tem o trabalho de participar das reuniões gerais \(RGs\) da Struct para informar aos outros membros da empresa júnior \(em especial, o presidente e o diretor de projetos\) o estado de desenvolvimento do projeto. Nessa hora, o gerente deve destacar de forma bem resumida se o desenvolvimento do projeto está progredindo de maneira adequada, se há necessidade de mais pessoas serem alocadas no projeto e se algo de anormal está acontecendo com o projeto.

Caso o gerente de um projeto não possa comparecer à reunião geral, ele deve instruir algum outro membro do projeto que estará na RG à realizar essa função. Caso isso não seja possível, o gerente deve enviar uma mensagem breve no *Slack* que detalhe esses fatores.
